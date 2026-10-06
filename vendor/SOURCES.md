# Upstream skill references

These are unmodified source copies for reviewing and adapting the skills in
`skills/`. Files under `vendor/` are not active skills. Keep each source's
license with its copy when publishing this repository.

| Source | Pinned commit | Included material | License |
|---|---|---|---|
| [obra/superpowers](https://github.com/obra/superpowers) | `8ca22dba9a94f28898bbce59f2537ff4d87c747d` | The original brainstorming skill and the execution, review, worktree, testing, debugging, and verification skills referenced by the planning and execution chain | MIT (`obra-superpowers/LICENSE`) |
| [riekelt/technical-writer](https://github.com/riekelt/technical-writer) | `85e53729dd959a2795d593d6769068e342cf3486` | Original `recording-decisions` skill and its `technical-writing` prerequisite | MIT (`riekelt-technical-writer/LICENSE`) |
| [obra/the-elements-of-style](https://github.com/obra/the-elements-of-style) | `05fc4f0d2b97b7c042dd9949ad658568e4a1324e` | `writing-clearly-and-concisely`, optionally referenced by the original brainstorming skill | Public domain, as stated in the upstream README and plugin manifest |
| [Nick2bad4u/git-commit-logically](https://github.com/Nick2bad4u/git-commit-logically) | `178d551100fcb28b4e8f79e3c0cb1cab00d96d65` | Candidate for local commits grouped by purpose | Unlicense (`git-commit-logically/LICENSE`) |

The active `idea-to-spec`, `spec-to-plan`, and `plan-to-code` skills adapt the
original Superpowers brainstorming, writing-plans, and executing-plans skills. The Superpowers copies
include `brainstorming`, `writing-plans`, `executing-plans`, `subagent-driven-development`,
`using-git-worktrees`, `finishing-a-development-branch`, `requesting-code-review`,
`test-driven-development`, `systematic-debugging`,
`verification-before-completion`, and `using-superpowers`, with their supporting
files. They are reference material while the local workflow is redesigned.

The active `workflow-conventions` skill adapts the checklist and todo rules of
`brainstorming` and `using-superpowers`, and the harness tool mappings in
`using-superpowers/references/`.

The active `record-decisions` skill adapts the original `recording-decisions`
skill for the ADR stage of this workflow.
The active `commit-changes` skill adapts `git-commit-logically` for the local
commit stage.
