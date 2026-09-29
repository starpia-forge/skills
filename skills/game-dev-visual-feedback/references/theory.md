# Theory and evidence

Use these sources to explain design choices or resolve conceptual ambiguity.
The implementation guidance in the skill is a practical synthesis, not a single
published theory or a universally validated set of animation parameters.

## Discoverability: affordances and signifiers

An affordance describes a possible action in the relationship between an actor
and the environment. A signifier is a perceivable clue that communicates useful
information. For game design, an available interaction and its visible cue need
separate consideration: working code does not ensure discoverability.

Source: Don Norman, [Signifiers, Not Affordances](https://jnd.org/signifiers-not-affordances/),
ACM Interactions, 2008.

Game-specific guidance: [Give a clear indication that interactive elements are interactive](https://gameaccessibilityguidelines.com/give-a-clear-indication-that-interactive-elements-are-interactive/).
Players do not necessarily share the designer's conventions for recognizing
usable UI elements or world objects.

## Before and after action: feedforward and feedback

Feedforward helps players anticipate the result of an action. Feedback helps
them interpret the action taken and resulting state. These address Norman's
gulf of execution and gulf of evaluation respectively. A button shape can suggest
pressing; its label can explain what pressing accomplishes. Both roles may be
served by the same visual element.

Source: Vermeulen et al., [Crossing the Bridge over Norman's Gulf of Execution: Revealing Feedforward's True Identity](https://documentserver.uhasselt.be/bitstream/1942/14759/1/VermeulenLuytenVandenHovenConinx_chi2013.pdf),
CHI 2013.

## Ongoing activity: visibility of system status

Players need timely information about current state, including changes caused
by time or external events. Input acknowledgment and final outcome are distinct
information needs. In a game, persistent playback, cooldown, or selection cues
are applications of this usability principle.

Source: Nielsen Norman Group, [Visibility of System Status](https://www.nngroup.com/articles/visibility-system-status/).

## Sensation and emphasis: game feel and juiciness

Game feel covers the affective experience of moment-to-moment interaction,
beyond visual effects alone. A survey of over 200 sources groups design intent
into physicality, amplification, and support. Juicing relates to amplification:
making events and their significance perceptible and felt.

Source: Pichlmair and Johansen, [Designing Game Feel. A Survey](https://arxiv.org/abs/2011.09201),
preprint 2020; related IEEE Transactions on Games publication 2021.

For practical demonstrations of expressive responses, see Jonasson and Purho,
[Juice It or Lose It](https://gdcvault.com/play/1016487/Juice-It-or-Lose), GDC Europe 2012.
Treat these techniques as a palette, not a requirement to maximize effects.

Kao et al. tested effectance (experiencing that one's actions cause effects),
competence, and curiosity in a preregistered experiment with 1,699 participants.
Feedback tied to success enhanced the tested motives, while amplification in the
tested condition reduced them. The authors suggest impaired agency and obscured
action–outcome relationships as possible explanations. This supports preserving
legible causality and success differences; it does not establish that stronger
feedback is always harmful or prescribe a universal effect intensity.

Source: [How does Juicy Game Feedback Motivate? Testing Curiosity, Competence, and Effectance](https://people.csail.mit.edu/dkao/pdf/3613904.3642656.pdf),
CHI 2024.

## Information across sensory channels

Visual and audio cues can communicate the same important information through
different channels. Preserve the information needed for play: an activity pulse
may identify an active speaker, but does not replace the meaning of a warning
or dialogue. Accessible alternatives should convey the relevant content.

Source: Microsoft, [Xbox Accessibility Guideline 103: Additional channels for visual and audio cues](https://learn.microsoft.com/en-us/xbox/accessibility/xbox-accessibility-guidelines/103).
