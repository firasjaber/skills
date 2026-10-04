# Skills

This repository contains separate skills for building software in one conversation. Each stage finishes its own work and asks before starting the next stage.

## Flow

1. [`idea-to-spec`](skills/idea-to-spec/SKILL.md) discusses the idea and writes an approved spec in `docs/specs/`.
2. [`spec-to-plan`](skills/spec-to-plan/SKILL.md) studies the codebase and writes a small implementation plan in `docs/implementation-plans/`.
3. [`plan-to-code`](skills/plan-to-code/SKILL.md) implements the plan in the current checkout and runs the relevant checks.
4. [`review-and-simplify`](skills/review-and-simplify/SKILL.md) asks a fresh agent to review the result. It fixes material findings and removes unnecessary code and tests.
5. [`record-decisions`](skills/record-decisions/SKILL.md) writes lasting choices as architecture decision records (ADRs) in `docs/adrs/`. Smaller choices go in `docs/adrs/decision-log.md`.
6. [`commit-changes`](skills/commit-changes/SKILL.md) groups the finished work into logical local commits. It does not create a feature branch or push.

The paths under `docs/` refer to the software project where you use these skills.

## Install

The skills live together in this repository. Install the full workflow for Codex across your projects with:

```sh
npx skills add firasjaber/skills --skill '*' -g -a codex
```

The `-g` flag installs skills for your user account. The `-a codex` flag selects Codex. Omit `-g` to install into the current project instead. The GitHub repository must be accessible to the person who runs the command.

To install one skill, run its command:

```sh
npx skills add firasjaber/skills --skill idea-to-spec -g -a codex
npx skills add firasjaber/skills --skill spec-to-plan -g -a codex
npx skills add firasjaber/skills --skill plan-to-code -g -a codex
npx skills add firasjaber/skills --skill review-and-simplify -g -a codex
npx skills add firasjaber/skills --skill record-decisions -g -a codex
npx skills add firasjaber/skills --skill commit-changes -g -a codex
npx skills add firasjaber/skills --skill ponytail -g -a codex
npx skills add firasjaber/skills --skill simple-english -g -a codex
```

The full workflow needs all eight skills. To see what the CLI finds before installation, run `npx skills add firasjaber/skills --list`. Start the workflow with `$idea-to-spec`.

## Shared skills

[`ponytail`](skills/ponytail/SKILL.md) helps the planning, implementation, and review stages keep code and tests small. [`simple-english`](skills/simple-english/SKILL.md) keeps the conversation and written records clear.

The source files live in [`skills/`](skills/). [`vendor/SOURCES.md`](vendor/SOURCES.md) lists the upstream material used as a reference.
