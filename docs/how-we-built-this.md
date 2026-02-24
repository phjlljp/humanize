# How we built and tested an AI-humanizer plugin

A walkthrough of what we figured out building a Claude Code plugin that detects and removes AI writing patterns. Sharing because the process taught us things about prompt engineering, eval methodology, and testing AI behavior that apply way beyond this specific project.

## The starting point

We had a Claude Code plugin called Humanize with 43 documented AI writing anti-patterns (drawn from Wikipedia's "Signs of AI writing" and Grokipedia). The patterns span vocabulary tells, syntactic habits, content issues, structural formulas, formatting quirks, behavioral artifacts, and statistical signals. Each pattern has a severity tier.

The plugin worked, but the skill file (the prompt that teaches Claude what to do) had its patterns in a separate reference file, and the format was inherited from our own early design. We knew another plugin existed -- blader's Humanizer -- that covered ~24 of the same patterns with a different approach.

## The rewrite: merging two approaches

Instead of picking one plugin, we compared both side by side and took the best parts of each.

**From humanizer (blader's plugin):**
- Pattern format: "Words to watch" + "Problem" + Before/After examples. Cleaner than our "Watch for" + "Why it's a tell" + "How to fix" split.
- The two-prompt self-critique audit: "What makes the below so obviously AI generated?" then "Now make it not obviously AI generated." More effective than a generic "re-scan" instruction.
- Punchy problem descriptions that show the issue rather than explain it clinically.

**From our plugin:**
- 43 patterns vs 24. Nearly double the coverage.
- Tier system (Tier 1/2/3) for prioritization. Humanizer had no severity ranking.
- Flags system (--diff, --casual, --formal, --academic, --thorough).
- Structured output formats (detection report, diff).

**Key design decisions:**
- Inline everything. One file, no external references. Costs more context but eliminates a tool call and keeps Claude's attention focused.
- Soul first. Move the "Personality and Soul" section before the pattern catalog so Claude thinks about voice before it thinks about mechanical rules.
- Let examples teach. The before/after pairs do the heavy lifting. Problem fields explain *why* something is a tell, not *how* to fix it. The examples show the fix.

## What we learned iterating

We went through several rounds of critical self-review. Each round caught real issues:

**Round 1:** The Phase 3 audit instruction was weaker than humanizer's. We adopted their two-prompt technique.

**Round 2:** Our Problem fields were too clinical ("AI substitutes elaborate linking constructions for simple 'is'/'are'/'has'"). Rewrote all 43 to be punchier ("'Serves as' where 'is' would do. 'Features' instead of 'has.' AI avoids simple verbs because they feel too plain.").

**Round 3:** The emoji pattern example (E4) had lost its actual emojis in the rewrite, so the "before" didn't demonstrate the pattern. The full worked example's audit section didn't match the new Phase 3 technique we'd adopted. Consistency between instructions and examples matters.

The takeaway: reviewing your own prompt engineering work requires the same rigor as reviewing code. Walk through the examples. Check that instructions match demonstrations. Read it as if you've never seen it before.

## Testing AI behavior: it's not unit testing

This is where it got interesting. How do you test a plugin whose "functions" are AI behavior prompted by a skill file?

**The problem:** The plugin doesn't have functions you can call and assert on. It has a prompt (SKILL.md) that, when given to Claude with some input text, should produce a detection report and a humanized rewrite. The detection is semi-deterministic. The rewrite is not.

**What we considered:**
- **pytest + Anthropic API** -- Build a custom eval harness in Python. Works but requires writing all the infrastructure: API client, response parser, scoring, result storage.
- **W&B (Weights & Biases)** -- Industry standard for ML experiment tracking. Great dashboards. But it's SaaS, and we'd still build the test runner ourselves.
- **Firebase** -- Too general. We'd be building everything from scratch.
- **promptfoo** -- Open-source, local, purpose-built for LLM prompt eval. Has YAML test definitions, built-in assertion types, Anthropic support, a web UI, and historical tracking. Basically "pytest for LLM prompts" with a dashboard.

**What we went with:** promptfoo. It handles the infrastructure so we just write the test definitions.

## Three layers of testing

**Layer 1 -- Detection (semi-deterministic):** Given input text with known patterns, does Claude's detection report list the right pattern IDs? This is testable with `contains-all` and `not-contains` assertions at `temperature=0`.

**Layer 2 -- Transformation properties (deterministic checks on non-deterministic output):** Does the rewritten text still contain Tier 1 trigger words like "delve" or "tapestry"? Is the output shorter than the input? Custom JavaScript assertions check measurable properties without requiring exact output matching.

**Layer 3 -- Quality (LLM-graded):** Does the output actually sound human? An `llm-rubric` assertion asks a grader model to evaluate the output. This is the least deterministic but the most important.

**The insight:** You can't unit-test "sounds human." But you can layer deterministic checks (pattern IDs, trigger words) with property-based checks (length, word frequency) with LLM-graded evaluation (rubric scoring). Each layer catches different failure modes.

## The eval config

```yaml
providers:
  - id: anthropic:messages:claude-sonnet-4-5-20250929
    config:
      temperature: 0

tests:
  - description: "Remote work - heavy AI signature"
    vars:
      input: file://fixtures/remote-work.md
    assert:
      - type: contains-all
        value: ["A1:", "A2:", "A3:", "B3:", "C1:", "D1:", "F1:", "F3:"]
        metric: Detection
      - type: javascript
        value: file://assertions/no_tier1_survivors.js
        metric: Transformation
      - type: llm-rubric
        value: "The output sounds like a human wrote it."
        metric: Quality
```

Run with `promptfoo eval`, inspect with `promptfoo view`.

## What this generalizes to

If you're building anything that uses LLM prompts as a core component -- agents, skills, system prompts, RAG pipelines -- the same methodology applies:

1. **Define what "correct" means in layers.** Some things are deterministic (does the output contain X). Some are property-based (is it shorter, is it valid JSON). Some require judgment (is it good).
2. **Use temperature=0 for the deterministic layer.** It won't be perfectly reproducible but it's close enough to catch regressions.
3. **Use an eval tool, not a unit test framework.** promptfoo, Braintrust, or similar. They're built for this. pytest isn't.
4. **Test across models.** A prompt that works on Opus might fail on Haiku. Multi-model eval catches this.
5. **Track over time.** The whole point is knowing whether your prompt changes made things better or worse. Historical comparison is the feature, not an afterthought.
