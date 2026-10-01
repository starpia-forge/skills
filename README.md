# Skills

A collection of Codex skills I use.

## Install

### User-wide Installation

```sh
gh skill install starpia-forge/skills --agent codex --scope user
```

### Project Installation (Git Repository)

```sh
gh skill install starpia-forge/skills --agent codex --scope project
```

### Non-Interactive

```sh
gh skill install starpia-forge/skills <skill-name> --agent codex --scope project
```

## Skill List

| Skill | Description |
| --- | --- |
| [game-dev-guidelines](skills/game-dev-guidelines/SKILL.md) | Guide game component design and implementation planning, including responsibilities, dependencies, composition, and tunable gameplay data. |
| [game-dev-visual-feedback](skills/game-dev-visual-feedback/SKILL.md) | Guide when and how to provide visual interaction cues, input responses, and state feedback in game UI and world objects. |
| [git-commit](skills/git-commit/SKILL.md) | Review and commit changes using purpose-focused Conventional Commits in the selected language. |
| [astra-orchestration](skills/astra-orchestration/SKILL.md) | Coordinate an Astra root, a Sol/xhigh manager, and Luna/max workers with separate execution review and final acceptance. |
| [karpathy-guidelines](skills/karpathy-guidelines/SKILL.md) | Guide code implementation, review, and refactoring with explicit assumptions, focused changes, and verifiable outcomes. |
| [luna-implement](skills/luna-implement/SKILL.md) | Delegate code implementation to GPT-6 Luna at max effort while the main agent handles design, planning, and verification. |

## Codex Agents

The `astra-orchestration` skill also requires these custom agent definitions.
Install the skill, then copy both files from `codex/agents/` into the target
repository's `.codex/agents/`, or into `~/.codex/agents/` for personal use.
The `codex/agents/` directory here stores the definitions for distribution;
Codex discovers installed agents under `.codex/agents/`.

| Agent | Model | Reasoning effort |
| --- | --- | --- |
| [astra_orchestration_manager](codex/agents/astra_orchestration_manager.toml) | `gpt-6.1-sol` | `xhigh` |
| [astra_orchestration_worker](codex/agents/astra_orchestration_worker.toml) | `gpt-6-luna` | `max` |

Start the root session with `gpt-6-astra` and use a runtime that supports named
custom agents and nested delegation. Invoke `$astra-orchestration` for work that
needs coordinated execution. The skill does not switch the root model.
