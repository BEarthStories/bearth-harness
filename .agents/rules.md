# Agent Rules — BEarth Stories Harness

High-signal non-negotiables for agents working on the BEarth Stories harness. Details live in
[AGENTS.md](../AGENTS.md) and the skill catalog under [.agents/skills/](.).

## Core Rules

- **Portability**: Scripts and commands must run on Windows PowerShell and WSL/Linux bash.
  Use Node's `path` resolution and avoid hard-coded separators.
- **Markdown Linting**: All markdown files must pass structure and style checks. Keep lines
  wrapped under 100 characters.
- **Skill Compliance**: Skills under `.agents/skills/` must include valid frontmatter, stay
  under the configured line budget, and use repo-specific prefixes when applicable.
- **Managed Skills**: Never edit `.agents/skills/external/` by hand — update vendored copies
  with `pnpm run skills:update` and commit them together with `skills-lock.json`.
- **No Production Operations**: Never run production database migrations or deployments
  without explicit human confirmation.
- **Harness workspace root**: Keep the agent session rooted at this harness repo. Edit
  sibling product repos by path; do not switch the workspace into them.

## Testing and Verification

- **Harness Validation**: Run `pnpm run lint` and `pnpm run check:wiki` after harness changes.
