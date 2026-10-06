---
name: workflow-conventions
description: Use with every stage of the idea-to-spec workflow. Sets the shared todo list, the question format with a recommended option, the visible self-review result, and the lists that can appear in chat.
---

# Workflow Conventions

These rules apply to every workflow stage: `idea-to-spec`, `spec-to-plan`, `plan-to-code`, `review-and-simplify`, `record-decisions`, and `commit-changes`. Each stage loads this skill at its start. Where these rules disagree with the reply rules of `simple-english`, these rules win.

## Todo list

Keep one todo list for the whole workflow. The user reads it to see the current stage and step.

1. Use the todo tool of the harness, for example `update_plan` in Codex or `todowrite` in OpenCode. If the harness has no todo tool, or the tool does not work in the current mode, post the list in chat as a Markdown checklist when a stage starts and when it ends.
2. If no workflow list exists, create it before other work. Add one item for the current stage and one item for each later stage, in workflow order.
3. When a stage starts, replace its item with the steps from the checklist of the stage. Start each step with the stage name, for example `spec-to-plan: Self-review the plan`.
4. Mark a step in progress before you work on it. Mark it done when its result exists. If a step does not apply, remove it and say why in chat.
5. When a stage ends, replace its steps with one completed item for the stage.

Only the main session changes the list. A sub-agent reports its result to the main session.

## Questions

Ask one question per message. When the answer is one of a few choices, offer the choices:

1. Put the recommended option first. Mark it `(Recommended)` and give the reason in one sentence.
2. Add one or two other options. Give the trade-off of each in one sentence.
3. End with a free-text option, such as "Other: describe what you want".

Use the question tool of the harness when one is available, for example `question` in OpenCode or `request_user_input` in Codex. If the tool adds its own free-text field, do not add a second one. If no question tool is available, write the options as a numbered list so that the user can answer with a number.

Approvals and handoffs use the same format. For example, the handoff after an approved spec offers "Continue to `spec-to-plan` (Recommended)", "Stop here and keep the approved spec", and a free-text option.

Ask an open question only when the user must supply the answer, such as a goal, a name, or a fact that the code cannot show. Do not invent options to fill the format.

## Self-review result

When a stage self-reviews a saved document, read the file again from disk before each pass. Do not review it from memory. After the passes, post the result in chat before you ask the user to review the document. Write one line per pass: what the pass checked, and what you changed or "No issues found". Do not report a pass that you did not run.

## Lists in chat

The `simple-english` reply rules forbid lists, and its self-check removes them. These replies are exceptions and use short lists:

- Question options.
- The todo checklist in chat.
- The self-review result.
- Review findings, proposed decision records, and created commits.

All other text in a reply follows the `simple-english` reply rules.
