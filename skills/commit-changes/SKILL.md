---
name: commit-changes
description: Use after decision recording, or when the user asks to stage finished work as separate logical local Git commits.
---

# Commit Changes

Turn the finished work into a series of coherent local commits. This stage follows `record-decisions` in the same session, or starts when the user directly asks to commit. The user's agreement to this handoff or direct commit request authorizes the local commits; do not ask again for each group. Use the current branch. Do not create or switch branches, merge, or push.

Load `simple-english` in Plain mode for commit messages and the final report. Load `workflow-conventions` for the todo list, the question format, and the commit list. Preserve exact code names and commands. Follow repository commit rules, including `.github/agent-commit-message-instructions.md` when present; otherwise inspect recent messages for the local style.

## Checklist

Add these steps to the workflow todo list when the stage starts, and complete them in order:

1. Set the scope.
2. Group the commits.
3. Stage and commit each group.
4. Report the result.

## Set the scope

Confirm the Git root, current branch, HEAD, and full status, including staged, unstaged, and untracked files. If HEAD is detached, ask the user where the commits belong. For a workflow handoff, read the spec and plan paths, final review result, decision records, starting commit, and pre-existing change list. Commit only the files and hunks created for this task. For a direct request, use the scope the user named. If the scope is unclear, inspect the changes and ask only about material ambiguity.

Read every candidate diff, including staged content and new files. Keep unrelated user changes in their current state. Never discard or overwrite them. If a task file also contains unrelated edits, separate the hunks safely. If their ownership cannot be determined, ask before committing that file.

## Group the commits

Group changes by purpose. Make as many separate commits as the work supports, while keeping each commit coherent and understandable. A spec, implementation plan, behavior change with its tests, decision record, and independent cleanup can be separate groups when each stands alone. Keep a test with the behavior it proves, and a lockfile or generated file with the change that requires it. Do not create an empty or artificial commit.

For each group, choose a message that states the change and reason. Use the repository's required format. If there is no rule, use a short imperative subject and add a body only when it explains a trade-off or non-obvious reason.

## Stage and commit

Stage only the paths or hunks in the current group. Account for content that was staged before this task. Use an isolated staging method if needed to keep it out of the commit. Never use a broad stage or commit command that can sweep in unrelated work.

Before each commit, read the exact staged patch and `git diff --cached --check`. Make sure that every staged line belongs to the group and that no secret, cache, build output, or accidental file is included. Commit the group locally. If a hook changes files or fails, inspect the result and resolve any task-caused failure before continuing. Run the affected checks again if content changed. Recheck status after each commit and repeat for the remaining groups.

The stage is complete when every intended task change belongs to one local commit, no unrelated change was committed, and the final status has been read. If a file remains uncommitted, explain why. Report the new commit hashes and subjects, final branch and status, and any check that a commit hook ran. Do not push.
