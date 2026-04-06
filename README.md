A collection of agentic skills for use with GitHub Copilot or Claude

## installation

Install a skill using the `npx skills` CLI:

```sh
npx skills add mwartell/skills --skill cdd
```

The [npm skills package](https://github.com/vercel-labs/skills) is a standard installer that copies agentic AI skills into your local environment. A skill is a Markdown file with optional support files, and the `npx skills` command installs them locally.

By default, installation means copying them to the current workspace, but there are options to install them in a per-user location. See the package documentation for how.


## available skills

### collaborative development documentation — [cdd/SKILL.md](cdd/SKILL.md)

A [Collaborative Development Document](https://mwartell.github.io/posts/collaborative-development-docs/) is a dated markdown file that logs a working session as numbered Prompt/Response pairs — creating a versioned, human-readable record of AI-assisted development work. YAML frontmatter anchors each session to a git commit and tags it with topics; the document body captures the full investigative thread so context carries across sessions.

Create a new CDD with `/cdd short subject`. Satisfy a numbered prompt with `/cdd 3`. The skill scaffolds frontmatter, inserts response headers in the right place, and keeps prompt/response numbers sequential.

See [collaborative development docs revisited](https://mwartell.github.io/posts/cdd-revisited/) for prompting patterns that make sessions effective.
