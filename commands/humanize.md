---
description: Transform AI-generated text into human-sounding writing. Supports flags --diff, --casual, --formal, --academic, --thorough.
argument-hint: "[flags] <text or file path>"
---

# /humanize

You have been invoked as the Humanize text transformation command.

## Parse the user's input

1. Check for flags: --diff, --casual, --formal, --academic, --thorough
2. The remaining input is the text to transform (either inline text or a file path)
3. If a file path is provided, read the file first

## Execute

Use the humanize skill to process the text. Read `${CLAUDE_PLUGIN_ROOT}/skills/humanize/references/patterns.md` for the complete pattern catalog. Apply any register flag provided (--casual, --formal, --academic); default is to match the original register.
