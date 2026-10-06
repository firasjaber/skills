---
name: idea-to-spec
description: Use when a product idea, feature request, or behavior change needs a written spec before implementation planning.
---

# Idea to Spec

Turn an idea into a clear, written specification through a conversation. Understand the desired behavior first. Leave file structure, APIs, algorithms, and test selection for `spec-to-plan`.

Load `simple-english` in Plain mode and `workflow-conventions` at the start. Use `simple-english` for questions, design discussion, progress updates, and the written spec. Keep exact names, paths, commands, and quoted text intact. Follow `workflow-conventions` for the todo list, the question format, and the self-review result.

## Checklist

Add these steps to the workflow todo list when the stage starts, and complete them in order:

1. Read the request and project context.
2. Choose the depth and tell the user.
3. Confirm the shared understanding.
4. Ask clarifying questions.
5. Propose approaches.
6. Present the design and get approval.
7. Write the spec.
8. Self-review the spec.
9. Get the user's approval of the spec.
10. Hand off to `spec-to-plan`.

For a bounded change with one clear approach, remove step 5. For a spike, replace the whole workflow list with the spike steps: read the context, present the question and probe, get approval, investigate, and report the result.

## Establish shared understanding

1. Read the request and relevant project context, including existing behavior, product docs, and accepted decisions. Explore only enough code to learn what already exists and what the idea would affect.
2. Summarize the intended outcome, users, constraints, and success criteria. Separate facts from assumptions and invite correction. Do not repeat questions the user already answered.
3. Ask one focused question at a time to close material gaps. Use the question format from `workflow-conventions`, with your recommended answer first. Check claims against the codebase or reliable sources when accuracy matters; identify unresolved uncertainty.

The spec must preserve this agreed understanding. A small change gets a short spec, but still gets a written spec.

## Choose the depth

Classify the request before asking questions, and tell the user which path you are taking:

- **Spike:** A feasibility question whose output is an answer, with no code kept. Present the question and a small probe, get the user's approval, investigate, and report the result. If the user then wants to build it, start a written spec through one of the paths below.
- **Bounded change:** A change to an existing flow that is already present in the repo. Ask only the questions that affect behavior, present a concise design in chat, and write a concise spec. It still goes to `spec-to-plan` after approval.
- **Architectural change:** A new project or subsystem, or a change to interfaces that other parts depend on. Explore the context, discuss meaningful alternatives, present the design in sections, and write a fuller spec.

If complexity grows, move to the architectural path. Do not use a smaller path to bypass the written spec or its review.

## Refine the idea

- Check whether the request contains independent subsystems. If so, help the user split them into buildable pieces and brainstorm the first piece. Each piece gets its own spec and plan.
- Explore two or three approaches when there are real trade-offs. Present them as options in the question format, with the recommended approach first and the reason for it. For a bounded change with one clear approach, do not invent alternatives.
- Prefer the smallest behavior that meets the user's goal. Reuse existing product concepts and avoid speculative features.
- Present the proposed behavior in short sections and ask for feedback after each meaningful section. Revise the design when the user corrects it.
- Cover the user flow, expected behavior, important edge cases, constraints, and success criteria. Include non-goals when they prevent scope confusion. Mention technical constraints only when they affect the product or feasibility.
- Keep implementation details out of this stage. The planning skill will inspect code paths, choose files and interfaces, and decide which tests are useful.

Write the spec when the user confirms the proposed behavior and no material question remains. The saved spec still needs the user's review.

## Write and review the spec

Save the spec at `docs/specs/YYYY-MM-DD-<topic>.md`, unless the user chooses another path. Create `docs/specs/` when needed. The final commit stage handles local commits.

Use the smallest structure that makes the requirements clear. State the goal, relevant context, chosen behavior, constraints, success criteria, and any rejected alternative whose rationale matters. Distinguish confirmed facts from assumptions. The final spec must not rely on chat history to explain a requirement.

Self-review the saved spec in two passes. Read the file again before each pass:

1. **Requirements pass:** Check that every agreed behavior and constraint is present, the success criteria are observable, and the scope fits one implementation plan. Remove features the user did not ask for.
2. **Clarity pass:** Check for contradictions, placeholders, ambiguous language, unsupported claims, and implementation decisions that belong in planning. Fix the document and recheck any section affected by the fixes.

Post the self-review result in the `workflow-conventions` format. Then show the saved spec to the user and ask them to review it. Incorporate corrections, repeat the relevant self-review passes, and post their result again. Do not treat approval of the chat design as approval of the saved file.

## Handoff

After the user approves the written spec, ask whether to continue to `spec-to-plan` in this session. If they agree, invoke `spec-to-plan` and pass it the spec path. If they want to stop, leave the approved spec ready for later planning. Do not start implementation from this skill.
