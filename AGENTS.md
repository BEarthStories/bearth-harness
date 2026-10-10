# BEarth Stories harness — agent instructions

This is the **BEarth Stories harness**: the shared AI intelligence layer (skills,
tooling, and multi-vendor adapters) for every BEarth Stories repo. It works across AI
coding tools (Claude Code, GitHub Copilot, Codex, Cursor, Gemini, Antigravity)
and both shells (Windows PowerShell and WSL bash).

## Setup

The harness runs qmd via `@paniolo/cli` and the `paniolo qmd` command. See the
[harness-qmd skill](.agents/skills/external/paniolo-qmd/SKILL.md) for platform setup and
launcher commands.

## Discovery first - search before you start

Use workspace-wide qmd search before reading or modifying code. The
[harness-qmd skill](.agents/skills/external/paniolo-qmd/SKILL.md) has the full search,
query, and retrieval guidance.

## Skills

Reusable task guidance lives in `.agents/skills/`. Customer harnesses may also
sync external skills from the Paniolo harness under `.agents/skills/external/`.

## Rust-first product work

New shared harness functionality belongs in the Rust products under Ranch Hand:
`paniolo scan` for static checks, `paniolo qmd` for retrieval, and `paniolo wiki`
for wiki validation. Do not add new
TypeScript, JavaScript, ESLint, markdown-lint, or hook logic to this repo unless
it is a thin adapter around a Rust binary or an explicitly scoped maintenance
change for code that has not been ported yet. When in doubt, extend the Rust
product and leave the harness as wiring.

## Agent workspace root

Keep this harness folder as the agent workspace root. Edit sibling product
repos (for example `bearthstories.com`) in place by path. Do not switch the
session into a sibling repo.

## How each tool wires this in

See the tool-specific adapter docs (for example `.cursor/README.md`,
`.claude/settings.json`, and `.github/hooks/`) for cross-tool wiring.

## Shell portability

All commands must work from both PowerShell and WSL bash. Prefer the
`pnpm run qmd -- …` launcher over calling `qmd` directly so the correct
per-platform binary and index are used. When a Windows-hosted editor terminal cwd
is a mapped `Z:` drive to `\\wsl.localhost\Ubuntu`, use `wsl --cd /home/…/harness`
for Linux-only commands, or run `pnpm run …` natively from the harness folder.

## Git commits across Windows and WSL

Three layouts are supported: native PowerShell, PowerShell against a WSL
filesystem, and WSL bash. Use cwd-independent husky launchers after
`pnpm install`; do not use `--no-verify` on UNC paths. See the
cross-platform tooling guide (Pattern 8) for details.

## Correction loop

Treat repeated agent mistakes as harness debt. Fix the weakest layer (rules,
skill, agent prompt, test, hook, or deterministic check) rather than patching
the generated output.

## Product repo paths

- `bearthstories.com`: `../bearthstories.com` (relative to this harness root)
- `midwifery-wiki`: `../midwifery-wiki` (wiki root: `wiki/`)
