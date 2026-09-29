---
name: game-dev-visual-feedback
description: Design and review clear, expressive visual feedback for game UI and world interactions, including without supplied examples. Use for interaction cues, input responses, activity indicators, and game feel while preserving the project's visual language; not for unrelated decorative art.
---

# Game Development Visual Feedback

Help players discover possible actions, predict their consequences, recognize
accepted input, understand results and ongoing states, and feel the character
and significance of their actions. Richness means responsive, differentiated,
well-timed behavior, not the number of effects. Apply this guidance
to the elements within the requested scope, using the game's existing visual
language and engine conventions.

Generate feedback from interaction meaning and project context; supplied visual
examples or an external reference collection are not prerequisites. Inspect
available project patterns for consistency, but do not require the user to supply
examples before proposing a concrete response. Use explicit provisional choices
when context is incomplete, subject to the conflict rules below.

## Match the guidance to the task

- **Design:** Use available briefs, mockups, and references to propose states and
  event behavior. Identify assumptions when project evidence is missing; source
  code access and implementation changes are not prerequisites.
- **Implementation:** Inspect the relevant code, scenes, resources, and input
  paths, then apply the guidance within the requested change.
- **Review:** Identify missing or misleading information and its player impact
  using the supplied artifacts. Recommend corrections without assuming edits
  are requested.

Apply code inspection, reuse, and runtime checks below when those resources and
activities are relevant to the task. Missing evidence is an uncertainty to state,
not proof that the project has no existing pattern.

## Establish the project's feedback baseline

Before choosing an effect, find the existing pattern for the same interaction
role and UI context. For a new menu button, inspect a comparable menu button,
its shared component or scene, and the theme, animation resource, or style tokens
it uses. An unrelated reward animation is not a suitable button reference.

Use this precedence when selecting behavior:

1. The user's explicit direction for this task.
2. The project's designated source of truth for the relevant UI family.
3. Applicable design rules, shared components, and presets, resolving any
   disagreement as described below.
4. Established examples serving the same role in the same screen or UI family.
5. A minimal extension of the closest compatible pattern when none covers the need.

When documentation and implementation disagree without a designated source of
truth, check their scope, maintenance status, and evidence of intended migration
or replacement. Neither a newer timestamp nor an existing implementation alone
establishes authority. Prefer the pattern supported by that evidence. If a
material conflict remains unresolved, explain the alternatives and seek direction
before choosing the disputed behavior; continue unaffected work. Ordinary reuse
and corrections already covered by the task need no additional approval.

Keep a proportional decision record in the proposal or implementation notes:
the chosen baseline and its source, relevant states and visual parameters,
informational and experiential goals, trigger/end/interruption behavior, and any
deviation with its rationale. Separate observed evidence from design assumptions.
Distinguish the intended design baseline from observed implementation values.
Read current values from code or resources when available, but resolve differences
using the precedence above rather than treating current code as authoritative.
A brief note is sufficient for a small change; no separate design document is
required.

Reuse the shared implementation or preset before copying values into a new
one-off effect. By default, preserve its normal, focused, pressed, selected, and
unavailable behaviors where applicable; use the change criteria below for
exceptions.

Examples in this skill illustrate communication roles; they do not prescribe
the project's aesthetic. A game whose buttons acknowledge input with a restrained
tint change should use that pattern for another equivalent button, not introduce
a spring bounce simply because the input-feedback example permits deformation.

Do not combine incompatible patterns or silently restyle unrelated elements.
If no baseline exists, establish a reusable feedback language before designing
elements independently. Infer a provisional direction from the game's tone,
materials, interaction cadence, and visual hierarchy; state assumptions when
these are unspecified. Define motion character (for example, crisp mechanical
or soft elastic), a few emphasis levels, semantic color/shape cues, and timing
and easing conventions. Assign comparable interactions to the same family.
Start with the families needed for the task, not a complete design system.
For implementation, capture these defaults in relevant components, presets, or
existing design documentation; for design-only work, include them in the proposal.

### Criteria for changing the baseline

Unless the user explicitly requests a different direction, change or extend the
baseline only for one of these reasons:

- A distinct interaction role or information need that the pattern cannot express.
- A difference in action cadence or event importance that warrants different emphasis.
- A specific experiential goal within the task, such as conveying weight,
  elasticity, impact, or rewarding completion, that the current response does not
  express. The agent may derive this goal from the action's characteristics or
  project direction; it need not be explicitly supplied by the user. Explain the
  connection: action or project context → missing experiential quality → how the
  proposed behavior expresses it. If context is incomplete, label the assumed
  direction. Treat untested improvements as hypotheses, not demonstrated defects.
- An evidenced usability, accessibility, or correctness defect, such as delayed
  acknowledgment, unreadable state distinctions, or misleading success feedback.

These criteria govern both visual variants and parameter tuning. A preference
without the context-to-behavior rationale above is insufficient; prior player
testing is not required to propose or implement a scoped design hypothesis.
Preserve intentional
differences between UI families; consistency does not require every button,
world object, and combat effect to look identical.

Consistency does not require reproducing a demonstrated defect. Choose the
smallest correction that addresses it while preserving the surrounding visual
language. Use an existing configuration, variant, or supported extension point
for a context-specific need or scoped local mitigation. Correct a shared component
when the defect is shared and that change is within the task's scope. Avoid
copying the shared implementation into a separately maintained local fork merely
to work around the defect. If the shared correction exceeds the task's scope,
report the issue and proposed scope separately. Describe any local mitigation's
limitation; if none is feasible, identify the remaining issue rather than silently
expanding the task into an interface redesign.

## Identify the communication need

Inspect the relevant gameplay logic, input paths, visual states, and existing
effects before adding feedback. For each element, determine:

- What can the player do, and under which conditions?
- What must they know before acting, immediately after input, and while waiting?
- Which success, failure, or state changes are otherwise hard to perceive?
- Does the response express the intended weight, energy, material, or significance
  of the action, or does it merely confirm that a state changed?

Evaluate informational clarity and experiential quality separately. A readable
button can still feel unresponsive or weightless. Consider expressive feedback
for frequently repeated core actions, meaningful success and rewards, interactions
whose force or material matters, and objects whose ongoing activity should feel
alive. These are candidates to assess, not a requirement to animate everything;
frequent actions especially need responses that remain comfortable on repetition.
Develop concrete candidates for relevant opportunities rather than stopping at
"add polish" or "make it juicy." Use the decision and composition steps below.

Use the following distinctions to choose a response. These are overlapping
communication roles, not separate components that every object must implement.

| Player's question | Role | When and how to communicate |
| --- | --- | --- |
| Can I use this? | Signifier | Show a recognizable affordance cue when discovery matters: silhouette, handle, outline, icon, or contextual prompt. Distinguish interactable objects from scenery. |
| What will this do? | Feedforward | Before commitment, show action labels, placement previews, trajectories, costs, or affected areas when the outcome needs explanation. |
| Did you receive my input? | Input feedback | Acknowledge input with a pressed state, highlight, or local motion. |
| Did it work? | Outcome feedback | Communicate success, failure, or partial result through state changes, impact responses, counts, or explanations. |
| What is happening now? | State visibility | Express ongoing playback, channeling, cooldown, selection, or processing. |
| How significant was that? | Game feel / juiciness | Convey the event's significance through expressive motion, flashes, particles, or other established effects. |

Affordance is the possible action; a signifier communicates that possibility.
Do not solve an unclear interaction solely by adding a stronger click animation:
the player must first discover where and how to act.

For theoretical rationale or source requests, read
[references/theory.md](references/theory.md). Routine implementation does not
require reading the research again.

## Decide when feedback is needed

After inspecting available context and identifying the relevant goals, select
one route for each interaction family:

| Situation | Route |
| --- | --- |
| An applicable pattern serves the informational and experiential goals | Reuse it; no additional effect is needed. |
| An applicable pattern leaves a justified gap under the change criteria | Extend or refine it using the composition procedure, preserving the family's shared character. |
| No applicable baseline can be established from available material | Propose a provisional feedback language as described above, then compose the needed responses. Distinguish a confirmed absence from unavailable evidence. |

The absence of user-supplied examples alone does not select the third route.
Clarity alone does not rule out expressive improvement: a door opening may already
communicate success, while its motion could still be refined to convey weight.

- Add discovery cues when useful objects resemble scenery or their interaction
  rules are unfamiliar. Use proximity, targeting, or focus to reveal details;
  keep enough earlier information for players to discover the target at all.
- Show current eligibility where it affects a decision. A locked door is still
  an interactive object: communicate the lock or required key instead of making
  it look like irrelevant scenery.
- Give input acknowledgment when acceptance would otherwise be ambiguous.
- Provide ongoing feedback for invisible activity, waiting, or persistent
  modes. Display progress only when there is meaningful progress to report;
  otherwise indicate activity without inventing a percentage.
- Explain actionable rejection near the affected target, such as insufficient
  resources or an occupied placement area. Avoid an identical success-looking
  reaction for an action that was rejected.
- Reinforce significant results that are easy to miss.
- Respect intentional uncertainty, hidden objects, and discovery mechanics.
  Do not reveal secret interactions or enemy information beyond the requested
  design; make intended controls legible within those constraints.

## Choose how feedback behaves

### Compose feedback from the action's meaning

For the extend or establish route above, develop the response through these
decisions. Scale the detail to the task; reused behavior needs no fresh design.

1. **Meaning:** Identify the action or state, its target, and the result that matters.
2. **Intended experience:** Name the quality to convey, such as precision,
   resistance, elasticity, power, relief, or celebration. Ground it in the game
   and action rather than selecting an arbitrary attractive effect.
3. **Visual mechanism:** Choose motion, deformation, light/contrast, shape,
   particles, or an indicator that expresses that quality in the feedback family.
   Prefer changes to the object itself when they communicate the cause clearly.
4. **Temporal behavior:** Define trigger, attack, hold or loop if needed, recovery,
   and cancellation. Specify intensity and how repeated input affects the response.
   Use existing parameters where available; otherwise give tunable starting values
   or ranges labeled as provisional, not universal rules.
5. **Composition:** Combine channels only when each contributes something useful,
   such as immediate press acknowledgment, a distinct completion response, and a
   persistent active marker. A single response may suffice; coordinate multiple
   phases when they serve different aspects of the informational or experiential
   goal. Apply the timing, state, and attention rules below to the resulting design.

For example, a heavy switch may use short travel and a firm settle to express
resistance and commitment; an elastic control may compress and recover; a reward
may travel toward the resource counter and settle as the count changes. These
are mappings from meaning to behavior, not presets to apply across all games.

### Bind visuals to meaning and state

Keep ongoing indicators aligned with the state they represent, ending or replacing
them when that state changes. A speaker's fixed pulse can indicate active playback;
an actual loudness visualization needs an audio level or meaningful proxy, smoothed
for readability. Do not present a fixed pulse as an accurate loudness meter.

Distinguish event effects from persistent states. A brief selection flash cannot
replace a persistent selected marker. Define how relevant states combine or
take priority, such as focused + selected or focused + unavailable, so one effect
does not erase another state's meaning.

### Preserve timing and causality

Distinguish input receipt from outcome. Begin input feedback without waiting for
decorative animation or a remote result. By default, bind success effects to
confirmed outcomes. When the project already uses predicted outcome feedback
for this action, follow that model's confirmation, cancellation, and reconciliation
rules, including how rejected
predictions are corrected visually. Do not introduce outcome prediction solely
to make feedback faster; immediate input acknowledgment can precede confirmation.

Keep reactions spatially associated with their target and temporally associated
with their cause. Distinguish press, hold, release, completion, and cancellation
when those phases change the action. Do not announce a release-activated action
as completed on pointer-down.

Inherit durations, amplitude, easing, and repetition from the relevant project
pattern by default. Apply the criteria in "Criteria for changing the baseline"
when tuning them; avoid universal timing constants. Do not introduce input delays
or control locks solely for decorative feedback. Preserve intentional gameplay
rules such as hitstop, action locks, and input buffering unless changing those
rules is part of the task.

### Allocate attention deliberately

Use stronger emphasis for more important events and local feedback for routine
ones. Avoid continuous pulsing on every usable object. Prefer a stable cue for
persistent availability and reserve motion for transitions or ongoing activity
that players need to notice.

At normal play speed, keep hit confirmation, success differences, targets, and
subsequent actions readable when amplifying an event. Do not make misses
and successful hits visually equivalent through indiscriminate effects.

Where a visual replaces audio information, identify what it must convey: activity,
source, direction, urgency, or content. Pulsing alone does not convey spoken
instructions. Do not rely solely on color for critical distinctions. Preserve
necessary information with static cues when motion is reduced, and use existing
accessibility settings for flashes and screen shake where applicable.

## Implement within the existing interaction model

When implementation is requested:

- Derive availability, active state, and outcomes from gameplay state or events;
  avoid a separate visual truth that can drift from the actual interaction.
- Cover the relevant input methods. Hover alone does not serve keyboard,
  controller, or touch users; provide equivalent focus or targeting cues.
- Keep decorative scaling or movement from unintentionally changing hit areas,
  layout, gameplay collision, or pointer focus.
- Define whether repeated events restart, blend, coalesce, or replace an effect.
  Avoid accumulating animations that become stronger with every click.
- On cancellation, state exit, or disable, clear only temporary effects owned by
  the state that ended. Preserve or recompute indicators for still-valid states,
  such as selection, unavailability, or ongoing activity. On destruction or object
  reuse, clean up effects and initialize visuals from the current object's state
  as appropriate to its lifecycle.
- Keep useful tuning values with the project's existing configuration pattern.
  Do not introduce a general effects framework for an isolated feedback change.

## Verify the player's interpretation

Validate the affected interaction at normal play speed when runtime access is
available. Check discovery before hover, supported focus/input paths, accepted
and rejected actions, repeated input, cancellation, and state exit where relevant.
For asynchronous actions, also check delayed completion and failure.

Compare the changed element with its baseline in context, including equivalent
focus, press, release, unavailable, and selected states where applicable. Check
motion, timing, intensity, and semantic color/icon usage as well as static
appearance. If a shared component changed, check representative existing users
of that component for unintended differences. A locally attractive effect is
not sufficient evidence of consistency with the surrounding interface.

Check that a player can distinguish availability, input receipt, outcome, and
ongoing activity without relying on an explanation from the developer. Observe
whether effects obscure targets or compete with more important information.
Inspect reduced-motion behavior when it is part of the project.

For expressive changes, also compare the response with its intended experience:
does it convey the chosen weight, energy, or completion, remain satisfying under
repeated input, and fit the neighboring interactions? Compare against the prior
behavior or a simpler variant when practical. Record these as design observations;
do not claim player preference or increased enjoyment without player evidence.

Report what was observed separately from what was inferred from code or a still
image. A screenshot cannot establish animation parameters, input latency, or
cleanup; do not report those as measured or verified from a still image.
State any runtime validation limitation without claiming the interaction passed.

For a nontrivial proposal, a compact table can make decisions reviewable:

| Element | Information / intended experience | Trigger / state | Visual response | End / interruption |
| --- | --- | --- | --- | --- |
| Speaker | Playback is active; restrained rhythmic energy | Actual playback starts | Small repeating pulse in the project's motion style plus active marker | Stop pulse on pause/stop; clear marker when inactive |

Summarize the decision record and applicable validation in the final output.
Do not require a full audit for a single button change.
