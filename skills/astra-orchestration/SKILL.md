---
name: astra-orchestration
description: Coordinate substantial work through an Astra root, a GPT-6.1 Sol/xhigh manager, and GPT-6 Luna/max workers. Use when execution benefits from multiple bounded tasks, coordinated revisions, and integrated verification, or when the user explicitly requests this hierarchy. Do not activate merely for discussion about orchestration.
---

# Astra Orchestration

Use the root to understand the user's intent and judge the final outcome. Give
the manager authority to operate execution and corrective work. Workers perform
bounded tasks whose results can be checked within the supplied context.

## Roles and runtime

| Role | Model and effort | Responsibility |
| --- | --- | --- |
| Root | `gpt-6-astra`; retain the session's effort | Intent, important decisions, and final acceptance |
| `astra_orchestration_manager` | `gpt-6.1-sol` / `xhigh` | Decomposition, allocation, execution decisions, review, and integration |
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
  Keep the brief proportional to the work; a separate planning document is not
  required.
- Delegate routine execution decisions to the manager: task boundaries,
  sequencing, worker allocation, local implementation choices within the agreed
  direction, verification, and corrective work. Do not require root approval
  for each task or retry. The manager owns worker coordination.
- Retain decisions that change the user's goal, scope, priorities, or success
  conditions, and significant design tradeoffs. Resolve difficult reasoning
  when decomposition alone cannot make a task suitable for a worker.

## Update intent during execution

Review escalations for their evidence, effect on the goal, and decision needed.
Make decisions within the user's existing instructions; ask the user only when
material intent remains unresolved. For matters reserved to the root, the
manager pauses affected work until it receives your decision or revised
guidance. Return actionable instructions so that work can resume; independent,
unaffected work may continue.

When user feedback or new evidence changes the interpretation of the task,
update the shared brief and notify the manager. Have the manager pause or
redirect affected workers and propagate the revised conditions. Unaffected
work may continue. Evaluate results against the latest requirements.

## Accept the outcome

The manager checks whether assigned work is correct and works together. The
root checks whether the integrated result solves the user's actual problem.

Inspect the manager's integrated result, coverage of success conditions,
supporting evidence, and unresolved issues. Examine important artifacts or run
additional checks where needed to resolve gaps, rather than repeating all
worker checks. Do not accept a completion claim without adequate evidence.

Send defects or missing requirements back to the manager with the failed
condition and supporting evidence. Let the manager arrange corrections. Do not
claim completion while required delegated work or verification remains
unresolved; distinguish observed failures from checks that could not run.

Report the outcome, meaningful verification, and remaining limitations
concisely. Keep routine worker traffic with the manager and bring important
decisions and verified results to the root.
