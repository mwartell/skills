---
name: cdd
description: 'Create or satisfy a Collaborative Development Document (CDD). Use for: new CDD, start session, satisfy prompt, continue CDD work. Usage: /cdd <title> to create a new CDD; /cdd <N> to satisfy Prompt N in the attached CDD.'
---


Manage a Collaborative Development Document (CDD). Detect mode from the argument:

- **Number only** (e.g., `/cdd 3`) → **Satisfy mode**: process Prompt 3 in the CDD file in context
- **Text** (e.g., `/cdd implementing auth system`) → **Create mode**: scaffold a new CDD file
- **No argument** → ask: "Provide a title to create a new CDD, or a number to satisfy a prompt."

---

## CREATE MODE

1. Ensure `cdd/` exists at the workspace root: `mkdir -p cdd`
2. Get git hash: `git rev-parse --short HEAD`
3. Create `cdd/YYYY-MM-DD-kebab-title.md` with this structure:

   ```yaml
   ---
   date: YYYY-MM-DD
   title: <title from argument>
   current_head: <hash>
   agent: "<your model name>"
   session_type:
   topics: []
   ---
   ```


   ```
   # Prompt 1:
   ```

   Leave the Prompt 1 body blank — the user writes the first prompt.

4. Report the filename created.

---

## SATISFY MODE (version 26.03.17)

1. **Execute** the requested task thoroughly.
2. **Insert** `# Response N: brief summary` immediately after the `# Prompt N:` section — no content before it.
3. **Summarize** in 2–3 sentences: what was accomplished, files changed, next steps.
4. **Follow** the summary with detailed work (code, analysis, commands).

### Rules

- Response header MUST come immediately after the Prompt — never place work before it.
- Use markdown links `[label](path)` for file references.
- Use code blocks for commands and code snippets.
- Keep prompt/response numbering sequential.

### Editing Technique

Anchor `replace_string_in_file` on the Prompt section, which is unique by construction:

```
oldString:
# Prompt N: title

[user-written prompt text]

newString:
# Prompt N: title

[user-written prompt text]

# Response N: brief summary

[response content]

```
