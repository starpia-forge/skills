---
name: game-dev-guidelines
description: Guide game component design and implementation plans involving responsibility boundaries, dependencies, composition, and tunable gameplay data.
---

# Game Development Guidelines

Apply these principles within the project's engine conventions and existing
architecture.

- **Low coupling:** Keep dependencies between gameplay components explicit and
  access another component's state through its public contract.
- **Composition:** Prefer the engine's existing composition mechanisms for
  combining gameplay behaviors.
- **SRP:** Group behavior and state that change for the same gameplay reason.
  Make ownership of shared state and lifecycle responsibilities explicit.
- **Data-driven configuration:** Separate tunable values and content definitions,
  such as stats, item properties, and balance settings, from behavior using the
  project's data structures or engine resources. Configuration separation and
  ECS or memory-layout design are distinct decisions.

In implementation plans, briefly explain responsibility boundaries, dependency
direction, and which values belong in data where relevant; scale detail to
the change.
