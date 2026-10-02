---
name: astra-orchestration
description: Coordinate substantial work through an Astra root, a GPT-6.1 Sol/xhigh manager, and GPT-6 Luna/max workers. Use when execution benefits from multiple bounded tasks, coordinated revisions, and integrated verification, or when the user explicitly requests this hierarchy. Do not activate merely for discussion about orchestration.
---

# Astra Orchestration

Use the root to clarify the user's intent, hand off the authorized work, and
judge the final outcome. The manager owns the full execution cycle, including
planning, worker coordination, verification, and corrections. Workers perform
bounded tasks whose results can be checked within the supplied context.

## Roles and runtime

| Role | Model and effort | Responsibility |
| --- | --- | --- |
| Root | `gpt-6-astra`; retain the session's effort | Intent, requirement decisions, unresolved core blockers, and final acceptance |
| `astra_orchestration_manager` | `gpt-6.1-sol` / `xhigh` | Full execution cycle, implementation decisions, review, and integration |
| `astra_orchestration_worker` | `gpt-6-luna` / `max` | Bounded execution, relevant checks, and evidence |

Run this workflow from an Astra root session with the two named custom agents
installed in `.codex/agents/` or `~/.codex/agents/`. Their source definitions in
this repository are `codex/agents/astra_orchestration_manager.toml` and
`codex/agents/astra_orchestration_worker.toml`. The runtime must support selecting
these custom agents and allowing the manager to spawn workers.

Select the installed custom agent through the runtime's agent-selection field;
a task name or a model name in a prompt does not load its configuration. The
agent files fix the child models and efforts. If the required root model,
custom agents, or nested delegation are unavailable, report the missing
capability rather than silently substituting a different topology. This skill
does not change the root model or install configuration during ordinary use.

If you are already the delegated manager or worker, follow your assigned role
and report to your parent; do not restart the root workflow.

## Understand and hand off

- Establish the desired outcome, scope, priorities, constraints, and observable
  success conditions. Distinguish explicit user requirements from assumptions.
  Resolve material ambiguity from available context and ask the user when an
  unresolved choice would change the result. Preserve the requested scope: a
  request for analysis or a plan does not authorize implementation.
- Spawn one installed `astra_orchestration_manager` and provide the objective,
  relevant original user requirements, success conditions, constraints, known
  facts, assumptions, unresolved questions, and necessary source references.
  Reuse sufficient existing specifications and pass only necessary clarifications;
  do not duplicate their detailed plan or re-explore implementation at the root.
- Hand off exploration, planning, execution, verification, corrections, and final
  reporting as one assignment. Include requested workflow steps such as OpenSpec
  explore, propose, apply, and archive when authorized. Phase transitions do not
  require additional root approval; honor any explicit user decision gate.
- Let the manager choose task boundaries, sequencing, algorithms, internal data
  structures, module organization, test strategy, and rework within the agreed
  external behavior and constraints. The manager owns worker coordination.
- Reserve root intervention for conflicting or materially unclear requirements,
  changes beyond the agreed goal, scope, priorities, external contract,
  constraints, or success conditions, and core blockers that remain unresolved
  after investigation and feasible changes of approach and require root judgment
  or user input. The manager handles execution problems, including external
  blockers, within its authority and available means. Technical difficulty
  or the perceived significance of an internal design choice alone is not a
  reason to seek root approval.

## Wait for decisions or completion

After handoff, wait for the manager's integrated result or a decision request.
Use completion notifications or the runtime's waiting mechanism within its
responsiveness limits instead of repeated status polling. An idle wakeup is
not a reason to inspect files, request another report, or restart planning.

Keep routine worker traffic, intermediate artifacts, and phase reports with the
manager. Do not independently monitor or review ongoing implementation while
the manager owns it. Handle new user input and actual decision requests when
they arrive. Keep required user-facing progress updates concise and use already
available status rather than soliciting extra reports solely for those updates.

## Update intent during execution

Review escalations for their evidence, effect on the goal, and decision needed.
Make decisions within the user's existing instructions and your authority. Ask
the user only when material intent remains unresolved, required input or action
must come from the user, or an explicit user decision gate applies.

For matters reserved to the root, the manager pauses affected work until it
receives your decision or revised guidance. Return actionable instructions so
that work can resume; independent, unaffected work may continue.

When user feedback or new evidence changes the interpretation of the task,
update the shared brief and notify the manager. Have the manager pause or
redirect affected workers and propagate the revised conditions. Unaffected
work may continue. Evaluate results against the latest requirements.

## Accept the outcome

The manager checks whether assigned work is correct and works together. The
root checks whether the integrated result solves the user's actual problem.

Start with one concise manager handoff: each requirement's outcome and evidence,
artifact references, consequential implementation choices, verification results,
and unresolved issues. This handoff is the basis for the root's acceptance review.
Inspect artifacts or run additional checks when evidence is missing or
inconsistent, a consequential question remains, or the user requests that
inspection. Avoid a second full implementation review or routine test reruns
when the evidence already establishes the requested outcome. Do not accept a
completion claim without adequate evidence.

Send defects or missing requirements back to the manager with the failed
condition and supporting evidence. Let the manager arrange corrections. Do not
claim completion while required delegated work or verification remains
unresolved; distinguish observed failures from checks that could not run.

Report the outcome, meaningful verification, and remaining limitations
concisely.
