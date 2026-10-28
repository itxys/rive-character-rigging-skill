# Character motion lessons

These are reusable observations from a multi-body, front-facing 2D character study. Measure each new rig and judge it in its native renderer; the values from one character are not defaults for another.

## Body variants and bone ownership

- Keep one calibration source for each variant's shoulder and hip positions, limb lengths, artwork anchors, and neutral IK targets. A body switch during motion should recalculate those targets from the selected variant.
- Inspect source art before promising articulation. A one-piece leg cannot show an independent knee bend; an empty foot slot cannot produce a designed foot through rigging alone.
- Artwork labels can be misleading. Verify the actual painted extent of each source part, then fit its measured start and end points to the corresponding bone. Check the mirrored side separately.
- If a live controller and a selection animation both write an IK target, the latter may silently erase motion. Give each animated property one owner and verify live values at the pose peak.

## Crouch, steps, and jumps

- In a front-facing perspective crouch, lowering the torso while keeping ankle targets grounded can force IK knees outward. Where the art supports it, shorten the actual thigh bone with crouch depth and scale its artwork on its measured long axis. Verify half and full crouch, lateral lean, ankle contact, and IK reach.
- Do not apply crouch foreshortening to every dance step. A wide step may need a mostly extended leg, quick weight transfer, and a slight knee bend. Inspect the peak stride, not just the landing.
- A foot lift needs coordinated ankle and toe targets. Include moving-foot offsets when calculating IK reach; a neutral-pose reach check can miss failure at the accent.
- To make the entire character jump, animate the shared root above the floor. Moving feet against a stationary torso can fold long legs without lifting the body. Use separate small compression at landing, then inspect the floor gap and shadow.
- If a long-leg variant's knees jitter during a root-driven jump, inspect concurrent internal crouch, thigh-length, torso shift, and lean channels. Neutral foot targets alone do not stabilize IK. Disable only the conflicting internal channels for that variant and action when the intended pose is a rigid whole-body hop; retain expressive motion in the head, arms, and face.
- Do not assume a negative root lift is a safe landing squash: in a rig whose IK targets do not follow the root identically, moving the root below floor contact can spread the knees again. Test that trial in native frames. If it fails, keep the root at or above ground and express compression through existing upper-body artwork and delayed arm/head settling.

## Facial acting

- Determine whether a Solo switches visual variants or whether bones deform a selected variant. Do not cycle mouth appearance layers if the rig's speaking motion is authored on mouth bones.
- Speaking generally needs unequal syllable lengths, varied aperture, and explicit holds. Repeating a short regular mouth loop can look mechanical.
- For an expressive reaction, align eye, mouth, body, and arm accents. A short anticipation followed by one strong pose, hold, landing, and smaller rebound reads more clearly than uniformly spaced motion.
- Reuse existing eye artwork when possible. Check whether the rig's eye scale controls are ViewModel properties rather than the nested eye node's transform. Inspect accessories separately; a dark outline may be glasses rather than an eye ring.

## Curves and visual verification

- An Elastic curve on every short adjacent segment creates repeated stops and jitter. Apply a bounce only around a selected accent, or author one overshoot and a smaller settle. The curve's period is relative to its segment length: a small period on a very short segment can oscillate rapidly.
- Separate curve jobs. Ease into a deliberate stop, blink, or impact; carry nonzero velocity through intermediate poses in a traveling action; use sampled periodic motion only for continuous loops such as breathing. An ease-in-out on every adjacent Rive segment can make the character pause at every key.
- In a four-body greeting study, applying a monotone cubic passage only to the greeting's pose sampler kept travel moving through intermediate keys while retaining stops at reversals. All four native previews compiled and rendered. Keep the change scoped to the action under review; broad replacement can alter previously accepted motions.
- The open-source [rive-animator-skill motion tool](https://github.com/obeskay/rive-animator-skill/blob/main/scripts/motion_keys.py) implements a monotone Hermite `flow` for continuous passages and a separate `track` for eased arrivals. Its five focused motion tests passed in an isolated review, but its output has not been tested against this skill's character rig. If adopting it, first validate generated RML and native playback in a disposable copy. Preserve authored accent overshoot where the monotone curve would flatten the intended performance.
- Keep stable foot targets during broad elastic body motion. Dense keyframes are rarely a substitute for clear anticipation, accent, hold, and recovery.
- Begin with a brief motion plan: intention, weight, view, start/end state, key silhouettes, contact points, and the action's readable beat. Block primary motion first; add delayed hair, accessories, breathing, and facial response only after support and pose timing work. This order is adapted from the [Spine-SKILL motion workflow](https://github.com/zxzAndyMAC/Spine-SKILL/blob/main/skills/spine-animation/SKILL.md); its editor instructions are Spine-specific.
- A successful Rive compile does not establish that the animation reads well. Review at full speed first, then sample neutral, anticipation, peak, landing, recovery, and body switches. For loops, watch several consecutive cycles and check both position and velocity at the seam. For one-shots, check entry, interruption, and settling. Inspect silhouette, overlapping parts, joint seams, floor contact, and state-machine output values.
