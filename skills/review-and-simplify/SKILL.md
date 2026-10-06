---
name: review-and-simplify
description: Use when an implementation has finished its checks and needs a fresh final review against the spec, project standards, and simplicity.
---

# Review and Simplify

Review the finished change, fix material findings, and leave the code and tests as small as the approved behavior allows. This stage starts after `plan-to-code` has run the relevant project checks and before decisions and commits are recorded.

Load `simple-english` in Plain mode for review discussion and the final report. Load `ponytail` for the simplicity pass. Load `workflow-conventions` for the todo list, the question format, and the findings list. Keep exact code names, paths, commands, and quoted output intact.

## Checklist

Add these steps to the workflow todo list when the stage starts, and complete them in order:

1. Prepare the review scope.
2. Run the fresh review.
3. Fix or explain each finding.
4. Rerun the affected checks.
5. Hand off to `record-decisions`.

## Prepare the review

Read the approved spec, implementation plan, project instructions, accepted decisions in `docs/adrs/` when present, and the verification results from implementation. Resolve a missing or failing relevant check before calling the change ready for review. Report a verified pre-existing failure separately.

Identify this task's full change from the starting commit, Git status, staged and unstaged diffs, and untracked files. Use the implementation handoff's list of pre-existing changes to keep unrelated work out of scope. Read the changed files and the surrounding code paths, not only the diff.

## Fresh review

Spawn one fresh review sub-agent when available. Give it the spec path, plan path, starting commit, task file list, pre-existing change list, and check results. Ask it to inspect the current worktree without editing it. The reviewer checks three things:

1. **Spec and correctness:** Find missing, wrong, or unrequested behavior. Trace important changed paths and realistic failure cases.
2. **Project fit:** Check documented project rules, existing patterns, accepted decisions, and maintainability concerns introduced by this change.
3. **Simplicity:** Find code, files, dependencies, comments, abstractions, or tests that can be removed or reused. Remove tests that mirror implementation or add no distinct behavioral evidence; keep checks for realistic regressions.

Ask for actionable findings only. Each finding cites the relevant code location or spec requirement, the observed problem, its impact, and the smallest useful fix. The reviewer reports no findings when the change passes. If a fresh reviewer is unavailable, perform the same pass yourself and say that the review was not independent.

## Act on findings

Check each finding against the spec, code, and tests. Fix material defects and worthwhile simplifications in the task's files. Preserve useful coverage and unrelated user work. Explain briefly when evidence does not support a finding. If a proposed fix changes approved behavior, return to the user and update the spec before applying it.

Run focused checks for each affected area, then rerun every project check affected by the final changes, including formatting, lint, types, build, and tests where relevant. Read the outputs. Inspect the final diff once more for accidental files and incomplete fixes.

The review is complete when all material findings are fixed or explained, every spec requirement still holds, and the relevant checks have current results. Report any remaining failure honestly.

## Handoff

Summarize the findings, fixes, code or tests removed, and final check results. Ask whether to continue to `record-decisions` in this session. If the user agrees, pass the spec, plan, review outcome, and implementation choices. Leave staging and commits for the final commit stage.
