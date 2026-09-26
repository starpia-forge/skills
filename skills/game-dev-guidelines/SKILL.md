---
name: game-dev-guidelines
description: Guide game code and component design when choosing responsibilities, dependencies, or writing implementation plans, with an emphasis on avoiding overengineering.
---

# Game Development Guidelines

Choose the simplest structure that satisfies current requirements. Apply these
principles within the project's engine conventions and existing architecture;
they do not justify unrelated restructuring.

- **YAGNI:** Add abstractions, extension points, and general-purpose systems only
  for a concrete present need. Hypothetical future features are insufficient
  justification. Prefer a local solution when generalization adds more complexity
  than it removes.
- **Low coupling:** Keep dependencies explicit and expose only what collaborators
  need. Avoid reaching into another component's internals or relying on hidden
  shared state. Introduce interfaces or events when they solve an actual dependency
  problem, rather than wrapping every interaction.
- **Composition:** Prefer combining focused behaviors over growing inheritance
  hierarchies for gameplay variations. Use the engine's existing composition
  mechanisms where suitable; avoid building a custom component framework without
  a demonstrated need.
- **SRP:** Group behavior and state that change for the same reason. Separate
  unrelated responsibilities, but keep cohesive logic together; a small method
  or class does not automatically need its own component.
- **Data-driven configuration:** Separate tunable values and content definitions,
  such as stats, item properties, and balance settings, from behavior. Use simple
  data structures or existing engine resources. This means configuration and
  behavior separation, not a requirement for ECS, memory-layout optimization,
  or a generic rules engine.

When principles compete, favor the simplest design that meets current needs.
In implementation plans, briefly explain responsibility boundaries, dependency
direction, and which values belong in data where relevant. Justify added
abstractions with the current problem they solve; scale detail to the change.

Writing approach informed by [OpenAI's Astra skill guidance](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra).
