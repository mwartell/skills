---
name: cdd
description: 'Create or satisfy a Collaborative Development Document (CDD) — a structured session log that records user prompts and agent responses with git context. ALWAYS use this skill when the user invokes /cdd, wants to start or continue a tracked working session, or asks to satisfy a numbered prompt in a CDD file. Usage: /cdd <title> to create a new CDD; /cdd <N> to satisfy Prompt N in the attached CDD.'
---

Manage a Collaborative Development Document (CDD). A CDD is a dated markdown file that logs a working session as numbered prompts and responses — creating a versioned, human-readable record of collaborative development work.

Detect mode from the argument:

- **Number only** (e.g., `/cdd 3`) → **Satisfy mode**: process Prompt 3 in the CDD file in context
- **Text** (e.g., `/cdd implementing auth system`) → **Create mode**: scaffold a new CDD file
- **No argument** → ask: "Provide a title to create a new CDD, or a number to satisfy a prompt."

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

### Structure

Place the Response header immediately after the Prompt header — any content before it breaks the document's sequential structure and makes the log hard to scan. Use markdown links `[label](path)` for file references and code blocks for commands and code. Keep prompt/response numbers sequential. Update the topics list in the front-matter if relevant topics emerged during the work.
