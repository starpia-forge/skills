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
| [git-commit](skills/git-commit/SKILL.md) | Review and commit changes using purpose-focused Conventional Commits in the selected language. |
| [karpathy-guidelines](skills/karpathy-guidelines/SKILL.md) | Guide code implementation, review, and refactoring with explicit assumptions, focused changes, and verifiable outcomes. |
| [luna-implement](skills/luna-implement/SKILL.md) | Delegate implementation to GPT-6 Luna at max effort while the main agent handles design, planning, and verification. |
