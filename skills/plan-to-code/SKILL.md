---
name: plan-to-code
description: Use when an approved implementation plan is ready to execute in the current checkout.
---

# Plan to Code

Implement the approved plan in the current session. The spec defines the promised behavior. The plan names the chosen approach and checks. Complete the work before offering the final review.

Load `simple-english` in Plain mode for progress updates, questions, and the final handoff. Load `ponytail` for code and test choices. Preserve exact names, commands, and quoted output.

## Start

Read the approved spec and plan, project instructions, relevant code, and existing tests. Record the starting commit and any staged, unstaged, or untracked files so that you can separate this task's changes from earlier work. Check the task order and any shared interfaces before editing. Use the current checkout. Follow a different branch choice only if the user explicitly requests it.

If the plan is missing, unapproved, or conflicts with the spec, resolve that before implementation. When a technical detail is routine, choose the smallest solution that follows the codebase. Ask the user when a discovery would change the agreed behavior or leave several consequential choices open.

## Implement

Work through the plan's tasks in order. Keep going between tasks without asking for a new approval. For each task:

1. Read the relevant code path and callers. Reuse existing code before adding a helper, dependency, or file.
2. Make the smallest change that delivers the task's behavior. Preserve security, accessibility, data safety, and explicit constraints.
3. Add or update only tests that catch a distinct behavior or realistic regression. Use the existing tests and checks named in the plan where they already give confidence.
4. Run the task's relevant check, read its output, and fix failures caused by this work. Mark the task complete only when its behavior and check both hold.

The spec wins when the plan and spec disagree. Record a short note about any implementation choice that changes the plan, including why it was needed. Update the plan when the change affects later tasks or verification. Bring any change to user-visible behavior back to the user and the spec.

Keep the task progress visible in a concise running update or the available task tracker. Resume from the first unfinished task if the session is interrupted. Stage and commit only in the final commit stage.

## Verify the result

After all tasks, compare the result with every spec requirement. Run the relevant formatter, lint, type, build, and test commands from the plan and project instructions. If a formatter changes files, run the affected checks again. Read the outputs and fix failures caused by this work. Report any pre-existing failure with evidence instead of calling it green.

Check Git status and the final diff for accidental files, duplicate code, and tests that prove no distinct behavior. Keep this pass focused; the next skill performs the full review and simplification.

The implementation stage is complete when every spec requirement is present, the planned checks and relevant project checks have been run, and any remaining failure or deviation is clearly reported.

## Handoff

Summarize what changed, which checks ran, and any unresolved issue. Ask whether to continue to `review-and-simplify` in this session. If the user agrees, invoke it with the spec path, plan path, starting commit, pre-existing changes, and files changed for this task. Leave local commits for the later commit stage.
