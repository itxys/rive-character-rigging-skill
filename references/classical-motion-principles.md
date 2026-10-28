# Classical character-motion principles for a Rive rig

This is an applied synthesis of publicly described animation teaching, not a substitute for reading the books. Sources: Richard Williams, [*The Animator's Survival Kit*](https://academic.macmillan.com/academictrade/9780865478978/theanimatorssurvivalkit/); Whitaker, Halas, and Sito, [*Timing for Animation*](https://www.routledge.com/Timing-for-Animation-The-Fundamentals-of-Animation/Whitaker-Halas-Sito/p/book/9780367527754); Thomas and Johnston, [*The Illusion of Life*](https://books.disney.com/book/the-illusion-of-life/); Goldberg, [*Character Animation Crash Course!*](https://www.silmanjamespress.com/shop/filmmaking-directing/character-animation-crash-course/). Disney Animation's [process overview](https://www.disneyanimation.com/process/animation/) and Animation Mentor's [squash-and-stretch teaching](https://www.animationmentor.com/blog/squash-and-stretch-the-12-basic-principles-of-animation/page/25/) clarify the principles used below.

## Block the force before choosing curves

1. Describe the emotion, the initiating force, support/contact points, and the silhouette at anticipation, takeoff, airborne extreme, impact, rebound, and rest. Each pose needs a reason in the action.
2. Allocate duration and spacing by force: a compressed preparation, a decisive launch, an airborne arc, a quick impact, then a smaller settle. Inspect screen-space displacement over consecutive frames; a smooth numerical curve can still feel weightless or sluggish.
3. Check the line of action, balance, and readable negative space at normal playback speed before adding more keys. If the pose is unclear, extra interpolation will not fix it.

## Express elasticity through connected forms

- Squash and stretch should contrast briefly around acceleration and contact. Preserve an approximately consistent apparent volume: when a form gets shorter, it can get wider; when it lengthens, it can get narrower. The character's material and style decide the amount.
- Recover quickly from an extreme so the audience feels the impact without watching the form remain distorted. Make the second rebound smaller than the first action.
- Assign deformation to a form that can actually deform. A root jump translates the whole character; it does not by itself show torso compression. A head-only squash cannot substitute for torso elasticity when the torso is meant to carry the impact.
- In a skeletal rig, keep IK contacts and joint lengths coherent. If scaling an ancestor shifts anchored feet or reverses knees, deform a local artwork or torso control instead and inspect seams at the neck, shoulders, hips, and knees.
- Let related parts arrive at different times: torso reacts to contact, then head and arms settle. Keep the delay small enough to read as one connected action rather than separate oscillations.

## Review as an animation, not a set of stills

- Watch the full action at normal speed first. Then examine consecutive frames around takeoff, contact, and direction changes to judge spacing and knee stability.
- Compare the neutral and most distorted silhouettes for volume, seam exposure, and preserved character identity. Confirm the body returns to its authored rest shape before the next cycle.
- Record which layer owns each deformation and which frames actually show it. A successful compile or a head-only improvement is not evidence that the whole body now feels elastic.
