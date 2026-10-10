# Summary

<!-- What changed and why. Link any related wiki page, issue, or skill. -->

## Local Verification

<!-- Record checks actually run. Note any skipped or failing check and why. -->

- [ ] `pnpm run test` passed
- [ ] `pnpm run lint` passed
- Other checks or exceptions:

## Intelligence Layer Checklist

This repo is the shared AI intelligence layer for every BEarth Stories repo, so
changes should keep the harness layered, shared, discoverable, and enforced.
Tick what applies and delete what does not.

- [ ] Canonical rules updated once in `.agents/rules.md` (not copied into adapters).
- [ ] Adapters (`.codex/`, `.agents/`, `.github/`) still point back to shared
      layers instead of duplicating them.
- [ ] New or changed task guidance lives in a skill under `.agents/skills/` —
      vendored `external/` copies only change via `pnpm run skills:update`.

## Correction loop

- [ ] If a repeated agent mistake produced this PR, the durable fix landed in the
      weakest layer (rule, skill, agent prompt, hook, or deterministic check) —
      not just in the generated output.
