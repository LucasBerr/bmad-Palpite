# Agent instructions

## As instrucoes desse projeto estao em: 
instrucoes.md

## Local BMAD skills

This repository includes project-local BMAD skills in `.agents/skills/`. Use these
skills from this repository; do not install or rely on a user-global BMAD setup.

- Use `$bmad` for BMAD guidance, setup, status, updates, repairs, module changes,
  or to decide the next BMAD workflow.
- Use `$bmad-build` when implementing a feature, story, bug fix, or other
  meaningful code change.
- Do not invoke `$bmod-core-tools` or `$bmod-method` directly. They provide
  metadata required by the BMAD skills.

When a BMAD skill is selected, read and follow its `SKILL.md` and any references
it requires. Keep changes, generated artifacts, and configuration scoped to this
repository unless the user explicitly requests otherwise.
