---
name: spec-to-plan
description: Use when an approved written spec needs an implementation plan for the existing codebase, before product code changes.
---

# Spec to Plan

Write an implementation plan that another engineer can execute without guessing about the important decisions. The plan explains what to change and how to verify it. It does not transcribe the code.

Load `simple-english` in Plain mode and `workflow-conventions` at the start. Use `simple-english` for technical questions, trade-off discussion, progress updates, and the written plan. Keep exact names, paths, commands, and quoted text intact. Follow `workflow-conventions` for the todo list, the question format, and the self-review result.

## Checklist

Add these steps to the workflow todo list when the stage starts, and complete them in order:

1. Read the spec and the affected code.
2. Resolve technical choices with the user.
3. Choose the smallest approach.
4. Write the plan.
5. Self-review the plan.
6. Get the user's approval of the plan.
7. Hand off to `plan-to-code`.

If the codebase and spec settle every technical choice, remove step 2.

## Inputs and context

Read the approved spec first. If it is missing, contradictory, or still awaiting the user's review, resolve that before planning. Read relevant code paths end to end, their callers, existing tests, dependencies, project instructions, and accepted decisions in `docs/adrs/` when present. Find existing behavior that can be reused before proposing a new component.

Load `ponytail` at the start of planning. Apply its simplicity ladder to the proposed design and again to the completed plan, while keeping the plan format in this skill. Its purpose here is to reduce unnecessary code, dependencies, abstractions, files, and tests while preserving the spec's behavior and important safeguards.

## Resolve technical choices

Ask the user about consequential choices the codebase and spec cannot settle. Ask one question at a time in the `workflow-conventions` format, with the recommended option first. Decide routine implementation details yourself, following the repo's patterns. Do not reopen product decisions already approved in the spec. If a technical discovery changes the promised behavior, return to the spec with the user before continuing.

Before writing tasks, identify the smallest change that satisfies the spec:

1. Can an existing flow, helper, type, or dependency do the work?
2. Can the change sit at a shared point instead of being duplicated across callers?
3. Are any proposed layers, configuration, migrations, or files speculative?
4. Which existing tests already exercise the behavior? What failure would a new test catch that those tests miss?

A smaller diff is useful only when it solves the full problem at the correct boundary. Preserve security, accessibility, data safety, and explicit requirements.

## Write the plan

Save the plan at `docs/implementation-plans/YYYY-MM-DD-<topic>.md`, unless the user chooses another path. Link the approved spec at the top.

Start with the goal, the existing flow to reuse or modify, the chosen approach, and project-wide constraints from the spec. List only decisions that an implementer could not safely infer. Break work into logical tasks whose outcomes can be checked. Number the tasks and start each task heading with `[ ]`, for example `### [ ] Task 2: Save the export settings`. `plan-to-code` changes the mark to `[x]` when the task is done. Each task should say:

- The behavior or outcome to deliver.
- The existing or new files it affects, when known.
- Any interface, data rule, or dependency another task relies on.
- The smallest useful verification: an existing check, a focused new test, or another observable check.

Give exact signatures, commands, and values where they settle a real choice. Do not include full function bodies, boilerplate, or repeated requirements. Do not split a task into separate setup, test, code, and commit tasks unless those are independently useful outcomes.

## Tests and verification

Plan tests around observable behavior and meaningful failure modes. Reuse existing coverage where it already proves the change. Add a focused regression test for a bug or a new behavior that could break. Use a small number of representative cases instead of per-function suites, repeated fixtures, or tests that mirror the implementation. A trivial change covered by existing checks may need no new test; say which existing check gives confidence.

Include the relevant project lint, formatting, type, build, and test commands. Do not require every task to start with a failing test, invent a fixed number of edge cases, or add a test merely to satisfy the plan template. When a risk is important but difficult to automate, state the manual check and why it is appropriate.

Commit grouping belongs to the final commit stage. Do not create branches or worktrees, and do not put a commit step after every task.

## Self-review

Review the saved plan in three passes and edit it before showing it to the user. Read the file again before each pass:

1. **Coverage and executability:** Map each spec requirement to a task and a suitable check. Confirm file targets, interfaces, task order, and commands agree with the current codebase. Make sure that names, signatures, and types match between the task that defines them and the tasks that use them. Replace each line that decides nothing, such as "TBD", "handle edge cases", or "add validation", with the decision, or remove it. Identify any unresolved decision that would block implementation.
2. **Failure cases:** List the inputs and failure cases that the spec implies and that a user is likely to meet. If no planned check covers one, add a check to the task that owns the code. Do not add cases only to reach a number.
3. **Ponytail pass:** Reapply the simplicity ladder to each task. Remove duplicate work, speculative abstractions, avoidable dependencies, excess files, and tests that prove no distinct behavior. Keep the checks that catch realistic regressions. Make sure the plan is shorter than a transcript of the implementation.

If a pass changes a task, check the affected requirements and downstream tasks again. Do not report a green check that you did not run. Post the self-review result in the `workflow-conventions` format.

## Handoff

Show the saved plan and ask the user to review it. Incorporate corrections, repeat the relevant self-review pass, and post its result again. After the user approves the plan, ask whether to continue to `plan-to-code` in this session. If they agree, invoke it with both the spec and plan paths. The execution stage follows the current checkout; commit management happens at the final commit stage.
