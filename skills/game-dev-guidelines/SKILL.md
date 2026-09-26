---
name: game-dev-guidelines
description: Guide game code and component design when choosing responsibilities, dependencies, or writing implementation plans, with an emphasis on avoiding overengineering.
---

# Game Development Guidelines

Apply these principles within the project's engine conventions and existing
architecture; they do not justify unrelated restructuring. When principles
compete, favor the simplest design that meets current needs.

- **YAGNI:** Justify abstractions and extension points with a concrete present
  need, not hypothetical future features. Prefer a local solution when
  generalization adds more complexity than it removes.
- **Low coupling:** Introduce interfaces or events when they solve an actual
  dependency problem, rather than wrapping every interaction.
- **Composition:** Prefer the engine's existing composition mechanisms for
  gameplay variations; avoid building a custom component framework without
  a demonstrated need.
- **SRP:** Keep cohesive logic together; a small method or class does not
  automatically need its own component.
- **Data-driven configuration:** Separate tunable values and content definitions,
  such as stats, item properties, and balance settings, from behavior. Use simple
  data structures or existing engine resources. This means configuration and
  behavior separation, not a requirement for ECS, memory-layout optimization,
  or a generic rules engine.

In implementation plans, briefly explain responsibility boundaries, dependency
direction, and which values belong in data where relevant; scale detail to
the change.