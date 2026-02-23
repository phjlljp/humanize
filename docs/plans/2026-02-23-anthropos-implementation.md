# Anthropos Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a Claude Code plugin that transforms AI-generated text into human-sounding text by detecting and eliminating 43 documented AI writing anti-patterns.

**Architecture:** A Claude Code plugin using the "Simple Plugin with One Skill + Command" pattern. The skill contains the complete 43-pattern catalog with severity tiers, transformation process, and personality guidance. A `/anthropos` command provides the user-facing entry point. Test fixtures validate the skill's effectiveness.

**Tech Stack:** Claude Code plugin system (Markdown-based skills + commands), no external dependencies.

---

### Task 1: Create plugin directory structure

**Files:**
- Create: `.claude-plugin/plugin.json`
- Create: `.claude-plugin/marketplace.json`

**Step 1: Create directories**

```bash
mkdir -p /Users/p/Documents/Claude/anthropos/.claude-plugin
mkdir -p /Users/p/Documents/Claude/anthropos/skills/anthropos
mkdir -p /Users/p/Documents/Claude/anthropos/skills/anthropos/references
mkdir -p /Users/p/Documents/Claude/anthropos/commands
mkdir -p /Users/p/Documents/Claude/anthropos/tests/fixtures
```

**Step 2: Write plugin.json**

Create `.claude-plugin/plugin.json`:
```json
{
  "name": "anthropos",
  "version": "1.0.0",
  "description": "Transform AI-generated text into human-sounding writing. Detects and eliminates 43 documented AI writing anti-patterns based on Wikipedia's Signs of AI Writing and Grokipedia's analysis.",
  "author": {
    "name": "anthropos"
  },
  "license": "MIT",
  "keywords": ["humanizer", "ai-writing", "text-transformation", "writing-quality"]
}
```

**Step 3: Write marketplace.json for local dev**

Create `.claude-plugin/marketplace.json`:
```json
{
  "name": "anthropos-dev",
  "description": "Development marketplace for anthropos plugin",
  "owner": {
    "name": "anthropos"
  },
  "plugins": [
    {
      "name": "anthropos",
      "description": "Transform AI text into human-sounding writing",
      "version": "1.0.0",
      "source": "./",
      "author": {
        "name": "anthropos"
      }
    }
  ]
}
```

**Step 4: Verify structure**

```bash
find /Users/p/Documents/Claude/anthropos -type d | grep -v _scratch | grep -v .DS_Store | sort
```

Expected: directories for `.claude-plugin/`, `skills/anthropos/`, `skills/anthropos/references/`, `commands/`, `tests/fixtures/`

---

### Task 2: Write the pattern catalog reference file

**Files:**
- Create: `skills/anthropos/references/patterns.md`

This file contains the complete 43-pattern catalog that SKILL.md will reference. Keeping it separate from SKILL.md keeps the main skill file focused on process while allowing the catalog to be browsed independently.

**Step 1: Write patterns.md**

Create `skills/anthropos/references/patterns.md` with the complete pattern catalog from the design document. The file should contain:

- Severity tier definitions (Tier 1, 2, 3)
- All 7 categories (A through G) with their patterns
- For each pattern: ID, name, tier, description, words/phrases to watch, before/after examples
- Transformation guidance for each pattern

The content comes directly from the design doc's "Complete Pattern Catalog" section, expanded with:
- Detection heuristics (specific words/phrases to scan for)
- Transformation guidance (what to replace them with)
- Before/after examples (drawn from the canonical sources and the Humanizer skill's examples)

The 7 categories and 43 patterns:

**Category A: Vocabulary & Word Choice (6 patterns)**
- A1: Overused AI vocabulary (Tier 1) — "delve", "pivotal", "crucial", "testament", "underscore", "realm", "harness", "illuminate", "nuanced", "intricate", "tapestry", "vibrant", "landscape" (abstract), "foster", "garner", "showcase", "enduring", "enhance", "interplay", "key" (adj), "valuable", "align with"
- A2: Overused multi-word phrases (Tier 1) — "delve into", "dive into", "plays a pivotal role", "shed light on", "at its core", "that being said", "a key takeaway is", "provide a valuable insight", "left an indelible mark", "a stark reminder", "a nuanced understanding", "quiet confidence/growth/leadership"
- A3: Excessive formal connectors (Tier 1) — "Additionally", "Moreover", "However", "Furthermore", "Indeed", "Consequently" at sentence starts
- A4: Positive intensifiers/buzzwords (Tier 2) — "innovative", "transformative", "cutting-edge", "game-changing", "revolutionary", "unparalleled", "invaluable", "groundbreaking", "renowned", "breathtaking"
- A5: Copula avoidance (Tier 2) — "serves as", "stands as", "functions as", "represents", "marks" instead of "is"; "boasts", "features", "offers" instead of "has"
- A6: Elegant variation (Tier 2) — synonym cycling to avoid word repetition

**Category B: Syntactic Patterns (7 patterns)**
- B1: Negative parallelisms (Tier 2) — "Not only...but also", "It's not just X, it's Y"
- B2: Rule of three (Tier 2) — forcing ideas into triads
- B3: Superficial -ing analyses (Tier 1) — appending present participle phrases
- B4: False ranges (Tier 2) — "from X to Y" where no meaningful scale exists
- B5: Repetitive syntactic templates (Tier 3) — same sentence structure repeated
- B6: Uniform sentence length (Tier 3) — lacking natural variation
- B7: Excessive nominalization (Tier 3) — noun-heavy structures instead of active verbs

**Category C: Content & Semantic Patterns (7 patterns)**
- C1: Exaggerated significance (Tier 1) — inflating importance of mundane subjects
- C2: Promotional/advertisement tone (Tier 2) — tourism-brochure language
- C3: Vague attributions/weasel words (Tier 2) — claims without specific sources
- C4: Overgeneralization (Tier 2) — sweeping claims without evidence
- C5: Superficial/generic analysis (Tier 2) — shallow balanced discussion
- C6: Undue emphasis on notability/media (Tier 2) — listing outlets, asserting coverage
- C7: Sentiment homogeneity (Tier 3) — uniformly positive/neutral, no emotional range

**Category D: Structural Patterns (7 patterns)**
- D1: Formulaic conclusions (Tier 1) — "In conclusion", vague optimistic wrap-ups
- D2: Challenges-and-recovery formula (Tier 1) — "Despite its...faces challenges..."
- D3: Inline-header vertical lists (Tier 2) — bolded headers with colons in list items
- D4: Rigid predictable organization (Tier 3) — formulaic intro/body/conclusion
- D5: Section summaries (Tier 2) — "In summary", restating what was just said
- D6: Title-as-proper-noun leads (Tier 2) — defining titles as entities
- D7: Vague see-also/related sections (Tier 3) — broad generic topic links

**Category E: Formatting & Style (7 patterns)**
- E1: Overuse of boldface (Tier 2) — mechanical emphasis
- E2: Title case in headings (Tier 2) — capitalizing all main words
- E3: Em dash overuse (Tier 2) — excessive em dashes where commas/parens would work
- E4: Emoji decoration (Tier 2) — emojis before headings or bullets
- E5: Curly quotation marks (Tier 3) — inconsistent smart quote usage
- E6: Unnecessary tables (Tier 3) — small tables better expressed as prose
- E7: Non-standard heading styles (Tier 3) — colons after headings, skipping levels

**Category F: Behavioral/Conversational Tells (6 patterns)**
- F1: Collaborative communication (Tier 1) — "I hope this helps", "let me know"
- F2: Knowledge-cutoff disclaimers (Tier 1) — "as of [date]", "based on available information"
- F3: Sycophantic/servile tone (Tier 1) — "Great question!", "That's an excellent point"
- F4: Inappropriate direct address (Tier 2) — "you can", "did you know" in non-conversational text
- F5: Phrasal templates/placeholders (Tier 1) — unfilled [brackets], placeholder text
- F6: Didactic disclaimers (Tier 2) — "it's important to note", "worth noting"

**Category G: Statistical/Quantitative Patterns (3 patterns)**
- G1: Low lexical diversity (Tier 3) — small vocabulary relative to text length
- G2: Reduced sentence length variation (Tier 3) — uniform sentence lengths
- G3: Excessive hedging (Tier 2) — over-qualifying statements

Each pattern entry should follow this format:
```markdown
### A1: Overused AI vocabulary [Tier 1]

**Watch for:** delve, pivotal, crucial, testament, underscore, realm, ...

**Why it's a tell:** These words appear disproportionately in AI text. Studies show some phrases appear 50-269x more often in AI text than human writing.

**How to fix:** Replace with simpler, more specific alternatives. "Delve into" → "examine" or "look at". "Pivotal" → "important" or just remove. "Landscape" → name the actual domain.

**Before:**
> An enduring testament to Italian colonial influence is the widespread adoption of pasta in the local culinary landscape, showcasing how these dishes have integrated into the traditional diet.

**After:**
> Pasta dishes, introduced during Italian colonization, remain common in the south.
```

**Step 2: Verify the file is readable**

```bash
wc -l /Users/p/Documents/Claude/anthropos/skills/anthropos/references/patterns.md
```

Expected: approximately 400-600 lines

---

### Task 3: Write the main SKILL.md

**Files:**
- Create: `skills/anthropos/SKILL.md`

This is the runtime artifact — the instructions Claude follows when the skill is invoked.

**Step 1: Write SKILL.md**

Create `skills/anthropos/SKILL.md` with this structure:

```markdown
---
name: anthropos
description: |
  Transform AI-generated text into human-sounding writing. Detects and eliminates
  43 documented AI writing anti-patterns across 7 categories with severity tiers.
  Based on Wikipedia's "Signs of AI writing" and Grokipedia's analysis. Use when
  editing text to remove AI tells, or invoke via /anthropos command.
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
---
```

The SKILL.md body should contain these sections:

1. **Overview** — One paragraph explaining what this skill does
2. **Process** — The 4-phase flow:
   - Phase 1: Detection & Analysis (scan for patterns, output diagnostic report)
   - Phase 2: Transformation (rewrite eliminating Tier 1+2 patterns, or all with --thorough)
   - Phase 3: Audit (re-scan, ask "would I suspect AI?", fix remaining tells)
   - Phase 4: Output (final text, optional diff with --diff)
3. **Flags** — Document --diff, --casual, --formal, --academic, --thorough
4. **Pattern Quick Reference** — Condensed table of all 43 patterns with IDs and tiers (one line each). Tell Claude to "Read references/patterns.md for full pattern details, examples, and transformation guidance."
5. **Personality and Soul** — Adapted from Humanizer's best section. This is critical — removing AI patterns is half the job, adding human voice is the other half. Include:
   - Signs of soulless writing
   - How to add voice (opinions, varied rhythm, complexity, first person, strategic mess, specificity)
   - Before/after example of soulless-clean vs. has-a-pulse
6. **Register Adaptation** — Rules for --casual, --formal, --academic flags and default auto-detect
7. **Detection Report Format** — Template for the Phase 1 output
8. **Diff Output Format** — Template for --diff output
9. **Full Example** — Complete before/after showing all 4 phases on a sample text saturated with AI tells (adapt from Humanizer's full example but expanded to cover more patterns)

**Step 2: Verify SKILL.md frontmatter is valid**

```bash
head -20 /Users/p/Documents/Claude/anthropos/skills/anthropos/SKILL.md
```

Expected: valid YAML frontmatter with name, description, allowed-tools

---

### Task 4: Write the /anthropos command

**Files:**
- Create: `commands/anthropos.md`

This is the user-invocable slash command that triggers the skill.

**Step 1: Write commands/anthropos.md**

```markdown
---
description: Transform AI-generated text into human-sounding writing. Supports flags --diff, --casual, --formal, --academic, --thorough.
---

# /anthropos

You have been invoked as the Anthropos text transformation command.

## Parse the user's input

1. Check for flags: --diff, --casual, --formal, --academic, --thorough
2. The remaining input is the text to transform (either inline text or a file path)
3. If a file path is provided, read the file first

## Execute

Use the anthropos skill to process the text through all 4 phases:

1. **Detection & Analysis** — Scan for all 43 AI patterns, output diagnostic report
2. **Transformation** — Rewrite eliminating detected patterns (Tier 1+2 by default, all tiers with --thorough)
3. **Audit** — Re-scan output, fix remaining tells
4. **Output** — Present final text. If --diff was passed, also show before/after diff with pattern IDs

Apply register flag if provided (--casual, --formal, --academic). Default: match the original register.

Read `references/patterns.md` for the complete pattern catalog with detection heuristics, transformation guidance, and examples.
```

**Step 2: Verify the command file exists**

```bash
ls -la /Users/p/Documents/Claude/anthropos/commands/anthropos.md
```

Expected: file exists

---

### Task 5: Write test fixtures

**Files:**
- Create: `tests/fixtures/sample-input-1.md` — Blog post saturated with Tier 1 patterns
- Create: `tests/fixtures/sample-output-1.md` — Expected transformation
- Create: `tests/fixtures/sample-input-2.md` — Technical doc with Tier 2 patterns
- Create: `tests/fixtures/sample-output-2.md` — Expected transformation
- Create: `tests/fixtures/sample-input-3.md` — Creative essay with Tier 3 patterns
- Create: `tests/fixtures/sample-output-3.md` — Expected transformation

**Step 1: Write sample-input-1.md (blog post, heavy AI tells)**

Write a ~300-word blog post that is deliberately saturated with Tier 1 AI patterns. It should contain at minimum:
- 5+ overused AI vocabulary words (A1)
- 3+ overused phrases (A2)
- 2+ formal connectors at sentence starts (A3)
- 2+ superficial -ing analyses (B3)
- 1+ exaggerated significance (C1)
- 1+ formulaic conclusion (D1)
- 1+ collaborative communication artifact (F1)
- 1+ sycophantic opening (F3)
- Bold formatting overuse (E1)
- Em dash overuse (E3)

**Step 2: Write sample-output-1.md**

Write the expected humanized version of sample-input-1.md. It should:
- Eliminate all Tier 1 and Tier 2 patterns
- Preserve the core factual content
- Sound like a human wrote it (varied rhythm, specific details, natural voice)
- Be roughly the same length or shorter

**Step 3: Write sample-input-2.md (technical doc, Tier 2 patterns)**

Write a ~300-word technical documentation excerpt with Tier 2 patterns:
- Copula avoidance (A5): "serves as", "features", "offers"
- Negative parallelisms (B1): "not just...but"
- Rule of three (B2)
- Inline-header lists (D3)
- Title case headings (E2)
- Em dashes (E3)
- Didactic disclaimers (F6)

**Step 4: Write sample-output-2.md**

The humanized version, keeping technical accuracy while eliminating AI patterns.

**Step 5: Write sample-input-3.md (creative essay, Tier 3 patterns)**

Write a ~300-word personal/creative essay with subtle patterns:
- Elegant variation / synonym cycling (A6)
- Uniform sentence length (B6)
- Sentiment homogeneity (C7) — uniformly positive
- Rigid organization (D4)
- Low lexical diversity (G1)
- Excessive hedging (G3)

**Step 6: Write sample-output-3.md**

The humanized version with varied rhythm, emotional complexity, and genuine voice.

---

### Task 6: Write README.md

**Files:**
- Create: `README.md` (at plugin root)

**Step 1: Write README.md**

The README should contain:

1. **Title and tagline** — "Anthropos: Make AI text sound human"
2. **What it does** — Brief description of the 43-pattern catalog, severity tiers, 4-phase process
3. **Installation** — Instructions for installing via Claude Code plugin system
4. **Usage** — Examples of `/anthropos` with different flags
5. **Flags reference** — Table of all flags with descriptions
6. **Pattern catalog summary** — Table with all 43 patterns (ID, name, tier, one-line description)
7. **Sources** — Links to Wikipedia and Grokipedia canonical references
8. **Credits** — Acknowledgment of the Humanizer skill for the "Personality and Soul" concept

---

### Task 7: Install and smoke test

**Step 1: Install the plugin locally**

```bash
cd /Users/p/Documents/Claude/anthropos
```

Then in Claude Code:
```
/plugin marketplace add /Users/p/Documents/Claude/anthropos
/plugin install anthropos@anthropos-dev
```

**Step 2: Restart Claude Code**

Exit and restart to pick up the new plugin.

**Step 3: Smoke test the command**

Run:
```
/anthropos Here is a comprehensive overview of this topic. I hope this helps! The platform serves as a pivotal tool in today's rapidly evolving digital landscape, showcasing innovative solutions that underscore its commitment to excellence. Additionally, it fosters meaningful connections — not just between users, but between ideas and outcomes. Despite facing challenges typical of the industry, the future looks bright. Let me know if you'd like me to expand on any section!
```

Expected: Detection report identifying multiple Tier 1 patterns (A1, A2, A3, B3, C1, D1, E3, F1, F3), followed by a rewritten version that sounds human.

**Step 4: Smoke test with --diff flag**

Run the same text with `--diff` added. Verify the output includes a before/after comparison with pattern IDs annotating each change.

**Step 5: Smoke test with a file path**

```
/anthropos tests/fixtures/sample-input-1.md
```

Verify it reads the file and produces output consistent with sample-output-1.md.

---

### Task 8: Commit

**Step 1: Stage all files**

```bash
git init /Users/p/Documents/Claude/anthropos
cd /Users/p/Documents/Claude/anthropos
git add .claude-plugin/plugin.json .claude-plugin/marketplace.json
git add skills/anthropos/SKILL.md skills/anthropos/references/patterns.md
git add commands/anthropos.md
git add tests/fixtures/
git add README.md
git add docs/plans/
```

**Step 2: Commit**

```bash
git commit -m "feat: initial anthropos plugin - AI text humanizer with 43 pattern catalog

Implements /anthropos command with:
- 43 AI writing anti-patterns across 7 categories (A-G)
- 3 severity tiers for prioritized detection
- 4-phase process: detect, transform, audit, output
- Flags: --diff, --casual, --formal, --academic, --thorough
- Test fixtures for blog, technical, and creative text domains
- Based on Wikipedia Signs of AI Writing and Grokipedia analysis

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>"
```

**Step 3: Verify**

```bash
git log --oneline -1
git status
```

Expected: clean working tree, commit message visible
