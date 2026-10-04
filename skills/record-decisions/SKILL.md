---
name: record-decisions
description: Use after final implementation review, or when an agreed technical decision needs an ADR or a running decision log entry for future work.
---

# Record Decisions

Record choices that future contributors and agents need to follow. Run this stage after `review-and-simplify`, using the approved spec, implementation plan, conversation, final code, and review outcome. Use an architecture decision record (ADR) for a durable rule about architecture, data, dependencies, interfaces, or operations. Use the running log for a smaller choice whose reason will help later work. Skip routine code choices and facts already clear from the code.

Load `simple-english` in Plain mode for the discussion and every record. Keep exact code names, paths, commands, and quoted evidence intact.

## Find decisions

Read accepted records and the running log in `docs/adrs/` when present. Compare the conversation and plan with the final implementation. Identify decisions that resolved a real alternative and will affect later work. Do not duplicate an existing entry. If a prior decision changed, record the new choice and link to the old one.

Show the user a short list of proposed ADRs and log entries, with each choice and why future work needs it. If there are no decisions to record, say so and proceed to the commit handoff without creating a file. Ask about a consequential choice if the conversation and implementation do not establish what the user accepted. Do not infer agreement from code alone.

## Write records

Write one ADR per file in `docs/adrs/`. Follow the repository's existing ADR numbering and layout when present. Otherwise use `NNNN-<short-topic>.md`, starting at `0001`, with this structure:

```markdown
# ADR NNNN: <decision title>

Status: Accepted
Date: YYYY-MM-DD

## Context
<The problem and constraints.>

## Decision
<The rule that future work must follow.>

## Consequences
<The benefit and the cost or limit that we accept.>

## Alternatives
<The strongest relevant alternative and why we did not choose it.>

## References
<Links to the spec, plan, code, or earlier ADRs when useful.>
```

Use the date of acceptance. Name only people who actually took part if the repository requires a decider field. State unknown facts as unknown. Keep the record short enough to answer what we chose and why. Do not turn it into a transcript or repeat the implementation plan.

For supersession, write the new ADR and update only the old record's status to point to it. Keep the old reasoning intact. Leave both records available so later work can trace the change.

Append smaller decisions to `docs/adrs/decision-log.md`. Follow an existing log format when present. Otherwise use `## YYYY-MM-DD: <short title>`, followed by `Decision:`, `Why:`, and `Instead of:` when an alternative matters. Link the spec, plan, or code when the link helps a future reader. Do not repeat an ADR in the log. If a logged decision changes, append a new entry that links to the earlier one. Keep the earlier entry intact.

## Review and handoff

Read each saved ADR and log entry as a future implementer. Make sure the choice and reason are clear, the trade-off is honest, and the references match the final code. Show the records to the user and incorporate corrections before continuing. Do not stage or commit in this stage.

Ask whether to continue to `commit-changes` in this session. If the user agrees, pass the spec and plan paths, final review result, ADR and log paths, starting commit, and pre-existing change list. If this stage wrote no decision record, say that in the handoff.
