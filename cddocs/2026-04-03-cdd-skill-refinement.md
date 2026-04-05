---
date: 2026-04-03
title: cdd skill refinement
current_head: 6c71c6b
agent: "Claude Sonnet 4.6"
session_type:
topics: []
---

# Prompt 1: apply anthropic standard

Apply the skill-creator skill and look for ways to improve cdd/SKILL.md

# Response 1: applied skill-creator standards to cdd/SKILL.md

Updated [cdd/SKILL.md](../cdd/SKILL.md) and [.agents/skills/cdd/SKILL.md](../.agents/skills/cdd/SKILL.md) with Anthropic skill-creator standards. Both files are now in sync. Next step: consider adding evals to verify the skill triggers and behaves correctly.

## Changes made

### Description — pushier and more explicit about triggering
**Before:** `'Create or satisfy a Collaborative Development Document (CDD). Use for: new CDD, start session, satisfy prompt, continue CDD work...'`

**After:** `'...ALWAYS use this skill when the user invokes /cdd, wants to start or continue a tracked working session, or asks to satisfy a numbered prompt in a CDD file...'`

Per the skill-creator standard, skills should be "a little bit pushy" to avoid undertriggering. Added `ALWAYS use this skill when...` with concrete trigger contexts.

### Added intro paragraph explaining what a CDD is
Models benefit from understanding the *purpose* of a tool, not just its mechanics. Added:
> "A CDD is a dated markdown file that logs a working session as numbered prompts and responses — creating a versioned, human-readable record of collaborative development work."

### `cdd/` → `cddocs/` in CREATE MODE
The repo source `cdd/SKILL.md` was out of sync with the installed `.agents/skills/cdd/SKILL.md` — the installed version already used `cddocs/` but the source did not. Aligned them.

### "Get git hash" → "Get the current git hash"
Minor clarity improvement.

### `### Rules` → `### Structure` with prose rationale replacing MUSTs
**Before:**
```
### Rules
- Response header MUST come immediately after the Prompt — never place work before it.
- Use markdown links `[label](path)` for file references.
- Use code blocks for commands and code snippets.
- Keep prompt/response numbering sequential.
```

**After:**
```
### Structure
Place the Response header immediately after the Prompt header — any content before it breaks the document's sequential structure and makes the log hard to scan. Use markdown links `[label](path)` for file references and code blocks for commands and code. Keep prompt/response numbers sequential.
```

Per skill-creator: "explain to the model *why* things are important in lieu of heavy-handed musty MUSTs." The prose form also consolidates the file/code-block rules into one sentence.
