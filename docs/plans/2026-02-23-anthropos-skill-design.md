# Anthropos: AI Text Humanizer Skill - Design Document

**Date**: 2026-02-23
**Version**: 1.0.0
**Command**: `/anthropos`

## Purpose

A Claude Code plugin skill that transforms AI-generated text into text that does not display identified AI anti-patterns. The skill draws from two canonical sources of truth:

1. [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) (~49 patterns)
2. [Grokipedia: Signs of AI-generated writing](https://grokipedia.com/page/Signs_of_AI-generated_writing)

The skill also incorporates useful elements from the existing [Humanizer](https://github.com/blader/humanizer) skill (v2.2.0), specifically its "Personality and Soul" guidance and two-pass audit approach.

## Scope

**In scope**: All linguistic, stylistic, structural, and formatting patterns that make text *sound* AI-generated. Covers all text domains (prose, technical, creative, professional).

**Out of scope**: Platform-specific artifacts (UTM parameters, `turn0search0` tags, broken wikitext, `contentReference` bugs, `oai_citation` markup). These are copy-paste artifacts, not writing quality issues.

## Architecture

### Approach

Comprehensive pattern catalog (43 patterns across 7 categories) with internal severity tiers for prioritization. Multi-pass transformation with detection report, tiered rewriting, and audit pass. Optional diff output via `--diff` flag.

### File Structure

```
anthropos/
  SKILL.md              # Main skill definition (runtime artifact)
  README.md             # User-facing documentation
  tests/
    fixtures/
      sample-input-1.md     # Blog post with heavy AI tells
      sample-output-1.md    # Expected transformation
      sample-input-2.md     # Technical doc with subtle patterns
      sample-output-2.md    # Expected transformation
      sample-input-3.md     # Creative writing with AI patterns
      sample-output-3.md    # Expected transformation
```

### Invocation

```
/anthropos [flags] <text or file path>
```

**Flags:**
- `--diff` — Output a before/after diff showing what changed and why (pattern ID for each change)
- `--casual` / `--formal` / `--academic` — Override target register (default: match original)
- `--thorough` — Also address Tier 3 subtle patterns (default: Tier 1-2 only)

### Tools Used

`Read`, `Write`, `Edit`, `Grep`, `Glob`, `AskUserQuestion`

## Complete Pattern Catalog

### Severity Tiers

- **Tier 1 (Dead giveaways)**: Patterns that immediately signal AI origin to any reader familiar with LLM output. Always transformed.
- **Tier 2 (Strong signals)**: Patterns that create a cumulative AI impression. Transformed by default.
- **Tier 3 (Subtle signals)**: Statistical/structural patterns detectable by close reading or analysis. Transformed only with `--thorough`.

### Category A: Vocabulary & Word Choice

| ID | Pattern | Tier | Description |
|----|---------|------|-------------|
| A1 | Overused AI vocabulary | 1 | Single words that appear disproportionately in AI text: "delve", "pivotal", "crucial", "testament", "underscore", "realm", "harness", "illuminate", "nuanced", "intricate", "tapestry", "vibrant", "landscape" (abstract), "foster", "garner", "showcase", "enduring", "enhance", "interplay", "key" (adj), "valuable", "align with" |
| A2 | Overused multi-word phrases | 1 | "delve into", "dive into", "plays a pivotal role", "shed light on", "at its core", "that being said", "a key takeaway is", "provide a valuable insight", "left an indelible mark", "a stark reminder", "a nuanced understanding", "quiet confidence/growth/leadership" |
| A3 | Excessive formal connectors | 1 | "Additionally", "Moreover", "However", "Furthermore", "Indeed", "Consequently" at sentence starts. Replace with natural transitions or restructure. |
| A4 | Positive intensifiers/buzzwords | 2 | "innovative", "transformative", "cutting-edge", "game-changing", "revolutionary", "unparalleled", "invaluable", "groundbreaking", "renowned", "breathtaking" |
| A5 | Copula avoidance | 2 | Using "serves as", "stands as", "functions as", "represents", "marks" instead of "is". Using "boasts", "features", "offers" instead of "has". |
| A6 | Elegant variation | 2 | Cycling through synonyms to avoid repetition: protagonist -> main character -> central figure -> hero. Natural writing repeats words when they're the right word. |

### Category B: Syntactic Patterns

| ID | Pattern | Tier | Description |
|----|---------|------|-------------|
| B1 | Negative parallelisms | 2 | "Not only...but also", "It's not just X, it's Y", "It is not merely X, but Y". Formulaic balance/contrast constructions. |
| B2 | Rule of three | 2 | Forcing ideas into triads: "fast, reliable, and scalable". Natural writing uses the number of items the thought requires. |
| B3 | Superficial -ing analyses | 1 | Appending present participle phrases: "highlighting the significance", "ensuring a thorough understanding", "emphasizing the critical role". These add nothing. |
| B4 | False ranges | 2 | "from X to Y" where X and Y don't represent a meaningful scale or continuum. |
| B5 | Repetitive syntactic templates | 3 | Same sentence structure repeated across paragraphs. ~76% of AI syntactic templates traceable to training data vs 35% in human text. |
| B6 | Uniform sentence length | 3 | Consistent sentence lengths lacking natural variation. Human writing has high standard deviation in sentence length. |
| B7 | Excessive nominalization | 3 | Noun-heavy structures instead of active verbs. "The implementation of the system" vs "We implemented the system". |

### Category C: Content & Semantic Patterns

| ID | Pattern | Tier | Description |
|----|---------|------|-------------|
| C1 | Exaggerated significance | 1 | "marking a pivotal moment", "stands as a testament to", "indelible mark", "deeply rooted", "setting the stage for", "key turning point", "evolving landscape", "focal point". Inflating the importance of mundane subjects. |
| C2 | Promotional/advertisement tone | 2 | "boasts a", "vibrant", "rich heritage", "natural beauty", "nestled within", "in the heart of", "showcasing", "commitment to", "breathtaking". Tourism-brochure language. |
| C3 | Vague attributions/weasel words | 2 | "Experts argue", "Observers note", "Industry reports suggest", "widely regarded", "several publications indicate". Claims of consensus without specific sources. |
| C4 | Overgeneralization | 2 | Sweeping claims without specific evidence, exaggerating scope. Making broad statements that could apply to almost anything. |
| C5 | Superficial/generic analysis | 2 | Sophisticated-sounding but shallow discussion. Balanced to the point of saying nothing. Lacks original insight or engagement with specifics. |
| C6 | Undue emphasis on notability/media | 2 | Listing media outlets, "independent coverage", "profiled in", "active social media presence". Asserting importance by cataloging who covered the topic. |
| C7 | Sentiment homogeneity | 3 | Uniformly positive or neutral tone. Lacking emotional range, complexity, or the messy human quality of mixed feelings. |

### Category D: Structural Patterns

| ID | Pattern | Tier | Description |
|----|---------|------|-------------|
| D1 | Formulaic conclusions | 1 | "In conclusion", "Ultimately", "Despite challenges...the future holds promise". Vague optimistic wrap-ups that could end any article. |
| D2 | Challenges-and-recovery formula | 1 | "Despite its [positive words], [subject] faces challenges..." followed by optimistic recovery. A rigid template. |
| D3 | Inline-header vertical lists | 2 | Bullet points starting with bolded headers followed by colons. Hybrid heading/list format. |
| D4 | Rigid predictable organization | 3 | Distinct intro/body/conclusion with consistent section structure. Enumeration over narrative flow. |
| D5 | Section summaries | 2 | "In summary", "To recap", restating what was just said instead of moving forward. |
| D6 | Title-as-proper-noun leads | 2 | Defining an article/section title as a real-world entity in the first sentence. |
| D7 | Vague see-also/related sections | 3 | Broad generic topic references that add no value. |

### Category E: Formatting & Style

| ID | Pattern | Tier | Description |
|----|---------|------|-------------|
| E1 | Overuse of boldface | 2 | Mechanical emphasis of phrases, bolding every instance of key terms, "key takeaways" style. |
| E2 | Title case in headings | 2 | Capitalizing all main words in headings/subheadings when not required by context. |
| E3 | Em dash overuse | 2 | Using em dashes (--) where commas, parentheses, or colons would be more natural. Formulaic "punched up" parallelism with dashes. |
| E4 | Emoji decoration | 2 | Emojis before headings, bullet points, or used as list markers. |
| E5 | Curly quotation marks | 3 | Inconsistent smart/curly quote usage, mixing curly and straight quotes. |
| E6 | Unnecessary tables | 3 | Small tables that could be expressed as prose. |
| E7 | Non-standard heading styles | 3 | Colons after headings, skipping heading levels, inconsistent heading hierarchy. |

### Category F: Behavioral/Conversational Tells

| ID | Pattern | Tier | Description |
|----|---------|------|-------------|
| F1 | Collaborative communication | 1 | "I hope this helps", "Certainly!", "Of course!", "let me know", "Would you like...", "here is a...". Chatbot interaction artifacts in standalone text. |
| F2 | Knowledge-cutoff disclaimers | 1 | "as of [date]", "based on available information", "while specific details are limited/scarce", "not widely documented". |
| F3 | Sycophantic/servile tone | 1 | "Great question!", "That's an excellent point", unsolicited "You're not alone". Performative validation. |
| F4 | Inappropriate direct address | 2 | "you can", "if you're interested", "did you know" in non-conversational text. |
| F5 | Phrasal templates/placeholders | 1 | Unfilled [brackets], placeholder dates, template instructions left in text. |
| F6 | Didactic disclaimers | 2 | "it's important to note", "worth noting", "it's crucial to remember", "may vary". |

### Category G: Statistical/Quantitative Patterns

| ID | Pattern | Tier | Description |
|----|---------|------|-------------|
| G1 | Low lexical diversity | 3 | Smaller vocabulary size relative to text length, lower unique-word ratio. |
| G2 | Reduced sentence length variation | 3 | More uniform lengths vs. human writing's natural variety. Measurable by standard deviation. |
| G3 | Excessive hedging | 2 | Over-qualifying statements: "could potentially possibly be argued that...might". |

## Transformation Process

### Phase 1: Detection & Analysis

Scan input text against all 43 patterns. Classify each detection by category, ID, and tier. Output a diagnostic report showing:
- Total patterns found, grouped by tier
- Specific instances with the problematic text quoted
- Overall severity assessment

### Phase 2: Transformation

Rewrite text eliminating all Tier 1 and Tier 2 patterns (and Tier 3 if `--thorough`). Follow these principles:

**Preserve:**
- Core meaning and factual content
- Intended register (unless overridden by flag)
- Logical structure and argument flow
- Domain-specific terminology

**Transform by:**
- Replacing overused AI vocabulary with natural alternatives
- Simplifying copula substitutions back to "is"/"are"/"has"
- Breaking up formulaic syntactic patterns
- Varying sentence length and structure
- Removing superficial -ing analyses entirely (they add nothing)
- Replacing vague attributions with either specific citations or removal
- Converting promotional tone to neutral descriptive language
- Eliminating formulaic conclusions in favor of substantive endings

**Add (from Humanizer "Personality and Soul" guidance):**
- Sentence rhythm variation (short punchy sentences mixed with longer ones)
- Specificity over generality
- Genuine perspective where the original intended it
- Appropriate informality and natural transitions
- Complexity and ambiguity where the topic warrants it
- Strategic imperfection (not every sentence needs to be polished)

### Phase 3: Audit

Re-scan transformed text against all patterns. Ask: "If I read this cold, would I suspect AI generated it?" Fix any remaining tells. This catches patterns that survive the first pass, especially cumulative ones like sentiment homogeneity or syntactic template repetition.

### Phase 4: Output

Output the final transformed text. If `--diff` flag is set, also output a section-by-section comparison showing:
- Original text
- Transformed text
- Pattern IDs that motivated each change

## Register Adaptation

| Flag | Behavior |
|------|----------|
| (default) | Auto-detect register from input, preserve it |
| `--casual` | Shift toward conversational: contractions, shorter sentences, first/second person OK |
| `--formal` | Maintain formal register but eliminate AI tells: precise vocabulary, no contractions, third person |
| `--academic` | Academic conventions: passive voice acceptable, technical precision, hedging reduced but not eliminated |

## Evaluation from Existing Humanizer Skill

### What we keep:
- Two-pass audit approach (Phase 2 + Phase 3)
- "Personality and Soul" concept: humanizing isn't just removing bad patterns, it's adding human qualities
- Simple skill file structure (Markdown-based, no external dependencies)
- Clear before/after examples for each pattern

### What we improve:
- Pattern coverage: 43 patterns vs. Humanizer's 24
- Source grounding: Every pattern traced to canonical Wikipedia and/or Grokipedia sources
- Severity tiers: Not all patterns are equally important
- Configurable flags: Register selection, thoroughness level, diff output
- Diagnostic report: Users see what was detected and why changes were made
- Test fixtures: Verifiable input/output pairs for quality assurance

### What we drop from Humanizer:
- Nothing of substance. All 24 Humanizer patterns are included in our 43. We've corrected cases where the Humanizer's descriptions were imprecise or incomplete relative to the canonical sources.

## Test Fixtures

Three sample pairs covering different domains and severity levels:

1. **sample-input-1.md / sample-output-1.md**: Blog post saturated with Tier 1 patterns (overused vocabulary, superficial analyses, formulaic conclusion, collaborative tone)
2. **sample-input-2.md / sample-output-2.md**: Technical documentation with Tier 2 patterns (copula avoidance, inline-header lists, em dash overuse, promotional tone)
3. **sample-input-3.md / sample-output-3.md**: Creative/personal essay with Tier 3 patterns (sentiment homogeneity, uniform sentence length, elegant variation, low lexical diversity)
