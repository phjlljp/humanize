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
