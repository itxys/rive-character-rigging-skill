---
name: rive-character-rigging
description: Edit and validate Rive character rigs, body variants, IK, and expressive native animation with the Rive CLI. Use for joint alignment, pose-preserving switches, crouches, jumps, facial acting, and motion timing.
---

# Rive character rigging

Use the installed Rive CLI and the actual project source. RML and CLI details change: query `rive docs` and `rive schema` for unfamiliar object types or properties instead of guessing.

## Work from the visible fault

1. Identify the active source, artboards, state machine, body variant, and owner of each animated property. Preserve source files and make edits in the designated test copy unless the user selects the production project.
2. Reproduce the reported pose in the native renderer. Compare neutral, affected pose, both directions, and any body switch that should preserve the pose. Distinguish source artwork placement, bone length/angle, IK, state-machine writing, and stale preview state before editing.
3. Change the smallest owning source. Keep one calibration source for per-body shoulder/hip coordinates, bone lengths, and artwork anchors. Do not compensate for a joint error by stacking unrelated offsets.
4. Render and inspect the result at the actual runtime pose. Bone coordinates and a clean compile do not establish visual quality; inspect silhouette, joint seams, overlap, and ground contact. Try a few measured variants when a visual parameter has no obvious correct value.

## Rigging invariants

- Match each part's measured `start` and `end` artwork points to its bone endpoints. Apply rotation, uniform fit, and the correct mirrored transform for the opposite side. Check anchor coincidence after parent rotation.
- When changing a shoulder or hip position, inspect the connected artwork in standing and moving poses. Keep style-specific proportions; one skeleton layout may need different profiles for different bodies.
- For a front-facing crouch, lowering the torso alone can push IK knees into a split stance. If the design calls for perspective, shorten the *actual thigh bone* continuously with crouch depth and shorten its artwork on the artwork's measured long axis. Keep the lower leg and grounded ankle target as intended, and check IK reach during lateral lean.
- A nested artwork's long axis is not necessarily its local X axis. Inspect the source artboard and rendered result; if bone length changes but artwork protrudes, verify the bound scale axis and mirror sign.
- Check which timeline or binding owns each calibrated property. A neutral/support layer must not overwrite the body-selection layer's joint positions or lengths. Test switching styles while a pose is active for stale values.
- For a dance that lifts a foot, move the ankle IK target and any toe target together. Give their live position one writer, then recompute the neutral target from the selected body's calibration on every frame. Check actual foot-to-target distance during the moving pose, not just at rest.
- Do not claim a body has a fully articulated knee or foot if the source art is a single leg graphic or the foot slot is empty. That needs artwork changes, not only a new bone value.

## Design the motion before polishing curves

- State the action's intent, camera view, weight, start/end state, and the few poses that must read clearly. Block those poses and their timing before adding secondary motion or more keys.
- Choose curves by purpose: continuous travel through poses needs continuity of speed; an impact or held expression may deliberately stop; a loop needs matching position and velocity at its seam. Judge the rendered movement, not the curve label.
- Watch the whole action at normal speed, then inspect problem intervals and transitions. For interactive actions, test interruption and return from anticipation, peak, and recovery.

## Verify and hand off

- Run `rive . --verify` and `rive inspect . --summary`; resolve new errors and distinguish existing source warnings.
- Render native screenshots for the reported pose and nearby poses. Check actual world joint positions, segment lengths, IK target error, and body-switch behavior when those properties changed. Prefer focused project tests over broad retesting.
- Use `rive .` for the interactive native preview. Local unsigned scripted builds may not work in a browser runtime. `rive push` uploads to the account; use it only when the user authorizes that destination.
- Export an editable `.rev` only after verification. Confirm its timestamp and content after export; do not present an older file as the latest result. An exported `.riv` is a runtime artifact, not the editable source.
- Summarize what was changed, the poses checked, and the path to a directly viewable preview or screenshot.
- After a Rive task reveals a new verified technique, failure mode, or user-approved proportion, update this skill or its relevant case reference in the same task. Record the cause, correction, and evidence; replace superseded guidance instead of accumulating contradictory rules. Skip routine parameter changes that teach nothing reusable.

For worked lessons on body variants, crouches, acting, and curve selection, read [references/character-motion-lessons.md](references/character-motion-lessons.md) when those tasks apply. For character motion design and squash/stretch, read [references/classical-motion-principles.md](references/classical-motion-principles.md). Treat all examples as diagnostic patterns, not universal coordinates.

