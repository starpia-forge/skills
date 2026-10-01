# Astra orchestration

`astra-orchestration` separates understanding the user's goal, managing
execution, and performing bounded work. An Astra root owns intent and final
acceptance; a Sol manager coordinates execution; Luna workers carry out tasks
with explicit completion checks.

## Purpose and design rationale

This skill was inspired by
[codex-astra-luna-orchestrator](https://github.com/donvito/codex-astra-luna-orchestrator/),
which provides profiles with execution roles such as explorer, worker, tester,
and researcher, plus an independent reviewer. The motivation here was to
simplify orchestration for work that OpenSpec has already turned into concrete
specifications: the broader setup felt like more machinery than that work
needed.

The design assigns each model the kind of work it is expected to handle well:

- **Astra:** interpret ambiguous user intent, resolve important choices, and
  judge whether the result solves the actual problem.
- **Sol:** design the execution plan and manage delivery once the goal is clear,
  including decomposition, local implementation decisions, review, and retries.
- **Luna:** perform defined actions whose results can be verified from the
  supplied context and completion conditions.

These are this workflow's design assumptions, not a benchmark-proven ranking
of model abilities. The simplification is a fixed root/manager/worker split
with routine coordination owned by the manager. It does not guarantee fewer
agents, lower cost, or faster completion.

## When to use it

Use it for substantial work that benefits from multiple bounded tasks,
coordinated revisions, and integrated verification, or when this hierarchy is
explicitly requested. Existing OpenSpec specifications can supply the goal,
constraints, and acceptance conditions; OpenSpec is useful context, not a
runtime prerequisite.

A small, localized task may not justify the coordination overhead. Discussion
about orchestration alone should not activate the skill, and a request for
analysis or planning does not authorize implementation. For code-only work
where the main agent should keep design, planning, and verification, see
[`luna-implement`](../skills/luna-implement/SKILL.md).

## Setup

Install the skill and the two custom agents as described in
[Codex Agents](../README.md#codex-agents). Start the root session with
`gpt-6-astra`, retain its selected reasoning effort, and invoke
`$astra-orchestration` with the task and relevant specifications.

The named agents are
[`astra_orchestration_manager`](../codex/agents/astra_orchestration_manager.toml)
(`gpt-6.1-sol`, `xhigh`) and
[`astra_orchestration_worker`](../codex/agents/astra_orchestration_worker.toml)
(`gpt-6-luna`, `max`). The runtime must select these installed agents and allow
the manager to spawn workers. Putting a role or model name in a prompt does not
load its configuration. Missing capabilities are reported as blockers; the
skill neither switches the root model nor installs configuration during use.

## Workflow

```text
User request / existing specifications
                 |
                 v
Astra root: clarify intent + success conditions
                 |
                 v
Sol manager: plan + assign bounded tasks
                 |
                 v
Luna workers: execute + run task checks <-----------+
                 |                                  |
                 v                                  |
Sol manager: review + integrate + verify -- fixes --+
                 |
                 v
Astra root: accept against intent -- gaps --> Sol manager
                 |
                 v
Verified outcome + remaining limitations

Escalation: worker -> manager -> root -> user when needed
Revised guidance returns down the same chain.
```

1. **Clarify and hand off.** The root establishes scope, priorities, constraints,
   and observable success conditions, separating requirements from assumptions.
   It resolves material ambiguity and gives one manager a proportional brief
   with relevant sources; a separate planning document is not required.
2. **Plan and delegate.** The manager chooses task boundaries, sequencing, and
   verification. Each worker receives purpose, inputs, scope, expected output,
   and completion checks. Independent work can run concurrently; dependent or
   overlapping edits are serialized with one writer per overlapping scope.
   Workers handle implementation and corrective edits and do not spawn agents.
3. **Escalate or revise.** Workers return missing context and decisions beyond
   their brief to the manager. Routine execution decisions stay there. Changes
   to goals, scope, priorities, success conditions, significant design tradeoffs,
   and unresolved reasoning blockers go to the root with evidence and impact.
   The root asks the user when material intent remains unresolved. Affected
   work pauses until guidance returns; independent work may continue. User
   feedback updates the brief and propagates to affected workers.
4. **Verify and correct.** Workers return artifacts and check evidence. The
   manager reviews actual results and combined behavior, sends corrections
   with the failed condition, and revises the approach if failures repeat.
   Checks that could not run are reported separately from observed defects.
5. **Accept.** The root inspects the integrated result against the latest user
   requirements, reuses sufficient evidence, and investigates important gaps.
   Missing requirements return to the manager. Completion requires required
   work and verification to be resolved, not merely a worker's success claim.

The [skill definition](../skills/astra-orchestration/SKILL.md) and linked agent
definitions specify the full role boundaries.

## Benchmark summary

One OpenSpec implementation task was run once per condition on 2026-10-01.
All roots used Astra/medium. Times are rounded whole-tree generation durations;
costs are calculated API-equivalent USD, not subscription charges. The
no-skill control omitted the two tested skills but retained standard OpenSpec
skills.

- **No skill:** 32/32 acceptance tests; 6m 52s; $2.17316600; fastest and cheapest generation in this task.
- **`luna-implement`:** 32/32 acceptance tests; 12m 59s; $5.18635024; Astra root with two Luna workers.
- **`astra-orchestration`:** 32/32 acceptance tests; 22m 49s; $4.93597050; Astra root, one Sol manager, and four Luna workers.

This single case does not establish a general speed, cost, or quality advantage.
Scheduling and cache conditions were not fully controlled, and deeper review
found a shared pathological-input defect despite the acceptance passes. See
the [full benchmark](astra-orchestration-bench.md) for methodology, per-agent
usage, implementation-performance findings, and limitations.
