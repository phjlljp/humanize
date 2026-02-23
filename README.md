# Anthropos

Make AI text sound human.

Anthropos is a Claude Code plugin that transforms AI-generated writing into text that reads like a person wrote it. It works by detecting and eliminating 43 documented AI writing anti-patterns drawn from Wikipedia's "Signs of AI writing" and Grokipedia's analysis of AI-generated text.

The patterns span 7 categories (vocabulary, syntax, content, structure, formatting, behavioral tells, and statistical signals) and are ranked into 3 severity tiers. The plugin runs a 4-phase process: detect patterns in the input, rewrite to remove them, audit the rewrite for survivors, then output the result.

## Installation

Install via the Claude Code plugin system:

```
claude plugin add anthropos
```

## Usage

```
/anthropos <text or file path>
```

Pass inline text or a path to a file. Anthropos will scan for AI patterns, rewrite, audit, and return the cleaned text.

### Examples

Basic transformation:

```
/anthropos "The company's innovative approach serves as a testament to their commitment to excellence, showcasing the transformative potential of cutting-edge technology."
```

Transform with a diff showing what changed and why:

```
/anthropos --diff "Additionally, the platform offers a comprehensive suite of tools designed to enhance productivity and foster collaboration."
```

Casual register with thorough cleanup (all tiers):

```
/anthropos --casual --thorough ./draft-blog-post.md
```

Academic register:

```
/anthropos --academic ./paper-intro.md
```

## Flags

| Flag | Description |
|------|-------------|
| `--diff` | Show a before/after comparison with pattern IDs explaining each change |
| `--casual` | Target conversational register: contractions, shorter sentences, first/second person |
| `--formal` | Target formal register: precise vocabulary, no contractions, third person |
| `--academic` | Target academic register: passive voice where conventional, technical precision, reduced hedging |
| `--thorough` | Address all 3 tiers including subtle patterns (default handles Tier 1 and Tier 2 only) |

When no register flag is provided, Anthropos auto-detects the register of the input and matches it.

## How it works

1. **Detection & analysis** -- Scan input against all 43 patterns. Produce a diagnostic report listing every detected pattern with its ID, severity tier, and the specific text that triggered it.
2. **Transformation** -- Rewrite the text to eliminate detected patterns. Tier 1 (dead giveaways) and Tier 2 (strong signals) are always addressed. Tier 3 (subtle signals) only with `--thorough`.
3. **Audit** -- Re-scan the transformed text. Ask: "If I read this cold, would I suspect AI wrote it?" Fix anything that still feels generated.
4. **Output** -- Present the final text. If `--diff` was passed, include a paragraph-by-paragraph comparison showing what changed and which pattern motivated each change.

## Pattern catalog

43 patterns across 7 categories. Tier 1 patterns are dead giveaways that immediately signal AI origin. Tier 2 patterns are strong signals that build a cumulative AI impression. Tier 3 patterns are subtle and only targeted with `--thorough`.

### A: Vocabulary and word choice

| ID | Pattern | Tier |
|----|---------|------|
| A1 | Overused AI vocabulary (delve, pivotal, tapestry, etc.) | 1 |
| A2 | Overused multi-word phrases (shed light on, at its core, etc.) | 1 |
| A3 | Excessive formal connectors (Additionally, Moreover, etc.) | 1 |
| A4 | Positive intensifiers/buzzwords (innovative, cutting-edge, etc.) | 2 |
| A5 | Copula avoidance (serves as, stands as, features, etc.) | 2 |
| A6 | Elegant variation / synonym cycling | 2 |

### B: Syntactic patterns

| ID | Pattern | Tier |
|----|---------|------|
| B1 | Negative parallelisms (not only...but also) | 2 |
| B2 | Rule of three (adjective, adjective, and adjective) | 2 |
| B3 | Superficial -ing analyses (highlighting the significance...) | 1 |
| B4 | False ranges (from X to Y with no real scale) | 2 |
| B5 | Repetitive syntactic templates | 3 |
| B6 | Uniform sentence length | 3 |
| B7 | Excessive nominalization | 3 |

### C: Content and semantic

| ID | Pattern | Tier |
|----|---------|------|
| C1 | Exaggerated significance (pivotal moment, testament to) | 1 |
| C2 | Promotional/advertisement tone (vibrant, nestled, breathtaking) | 2 |
| C3 | Vague attributions/weasel words (experts argue, widely regarded) | 2 |
| C4 | Overgeneralization (sweeping claims without evidence) | 2 |
| C5 | Superficial/generic analysis | 2 |
| C6 | Undue emphasis on notability/media coverage | 2 |
| C7 | Sentiment homogeneity | 3 |

### D: Structural

| ID | Pattern | Tier |
|----|---------|------|
| D1 | Formulaic conclusions (In conclusion, the future holds promise) | 1 |
| D2 | Challenges-and-recovery formula (Despite its...faces challenges) | 1 |
| D3 | Inline-header vertical lists (bolded headers with colons) | 2 |
| D4 | Rigid predictable organization | 3 |
| D5 | Section summaries (In summary, to recap) | 2 |
| D6 | Title-as-proper-noun leads | 2 |
| D7 | Vague see-also/related sections | 3 |

### E: Formatting and style

| ID | Pattern | Tier |
|----|---------|------|
| E1 | Overuse of boldface | 2 |
| E2 | Title case in headings | 2 |
| E3 | Em dash overuse | 2 |
| E4 | Emoji decoration | 2 |
| E5 | Curly quotation marks (inconsistent) | 3 |
| E6 | Unnecessary tables | 3 |
| E7 | Non-standard heading styles | 3 |

### F: Behavioral/conversational

| ID | Pattern | Tier |
|----|---------|------|
| F1 | Collaborative communication (I hope this helps, let me know) | 1 |
| F2 | Knowledge-cutoff disclaimers (as of [date]) | 1 |
| F3 | Sycophantic/servile tone (Great question!) | 1 |
| F4 | Inappropriate direct address (you can, did you know) | 2 |
| F5 | Phrasal templates/placeholders ([Your Name Here]) | 1 |
| F6 | Didactic disclaimers (it's important to note) | 2 |

### G: Statistical/quantitative

| ID | Pattern | Tier |
|----|---------|------|
| G1 | Low lexical diversity | 3 |
| G2 | Reduced sentence length variation | 3 |
| G3 | Excessive hedging (could potentially possibly) | 2 |

## Sources

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) -- maintained by WikiProject AI Cleanup
- [Grokipedia: Signs of AI-generated writing](https://grokipedia.com/page/Signs_of_AI-generated_writing)

## Credits

The "Personality and Soul" concept -- the idea that removing AI patterns is only half the job, and that clean but voiceless writing is just as suspect -- is adapted from the [Humanizer skill](https://github.com/blader/humanizer).

## License

MIT
