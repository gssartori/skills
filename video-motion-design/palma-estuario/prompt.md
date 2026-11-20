# GTA 6

An original coastal illustration system in which a drawn contour opens onto another place. Give an object enough specificity to read in solid ink before putting scenery or ornament inside it. Keep the palette of the world outside the contour distinct from the light seen through it. Build new figures, architecture, ornament and typography for the subject supplied by the reader.

## Shape and light

Start with one dominant silhouette, one clean interior opening and at least one near edge that can cover the opening. Draw the weight-bearing side of a figure or structure first. Keep fine features such as the eye, lip of a window or joint of a hand outside the busiest patterned area. Separate deep shadow, local pigment, grazing light and paper. Preserve enough unmarked space for a contour to read at thumbnail size.

Choose one of the two treatments below for a piece. Both share the same masking and spatial rules. Their finishes remain distinct.

- **Deco light.** Set a matte slate stage in #1C212C. Raise a plaque in #242B3A, cut opposite corners, and use a restrained magenta-to-amber or pink-to-cyan edge. Crop scallops, interlocking arches or a tritone scene inside the silhouette. Reserve #F8F9FC for lettering; a small warm coral script accent can sit beside a heavier condensed word. Keep broad areas of slate free of bloom.
- **Tidal intaglio.** Cut the exterior in plum #221D35 or petrol #142C37. Light the internal scene with guava #EE8383, peach #FFCC97 and warm paper #FFF0CE. Draw three line scales: the structural contour, the break between two planes and a tapered engraving stroke. Hatch along the material. Keep paper tooth and broken ink fixed to the surface they describe. Reflections on water spread horizontally and break around objects.

## Lighting families for the Deco treatment

| Family | Deep pigment | Body | Lit edge | Use |
| --- | --- | --- | --- | --- |
| Slate and sunset neon | #1C212C | #E84393 | #FF9F5A | Type plates, active perimeter, warm opening. |
| Coral and plum | #4A325C | #D96B96 | #FAD389 | A sunset silhouette with a peach intermediate plane. |
| Cyan marsh | #243452 | #2E607A | #A7E4D8 | A cool interior scene with cyan water and indigo mesh. |
| Electric orchid | #3C2766 | #9B5DE5 | #38E4F0 | Club glass and a selective pink or cyan highlight. |
| Pulp foliage | #1F3B2B | #D8A24A | #9CE04B | A dense near-camera collage that momentarily hides the reveal. |

Apply a single pattern such as a stepped fan, ogee or interlocking arch to a silhouette. Clip its strokes at the edge and keep the negative openings the color of the stage. One scene may move from one family to another as the camera enters the aperture. A small hot edge can carry the eye across the change.

## Figure construction and continuity

Choose a head angle before drawing the features. In a true profile the bridge, tip, lips and chin share one continuous outer contour. Show one eye and one brow; place the ear behind the jaw hinge. In a three-quarter pose carry the center line from brow to philtrum around the head volume, compress the far cheek and foreshorten the far eye. Keep the near eye, nostril, mouth and chin on that same rotation. The head sits on a neck that meets the collar. Use the same construction whenever the character returns, including the small portraits and the closing image.

Build the arm from shoulder, elbow and paired wrist edges. For a palm carrying an object, show the object resting across the curled fingers with a visible contact edge, a distinct opposing thumb and a forearm that meets the palm continuously. Foreshorten fingers along a common knuckle arc. At a small scale a joined finger silhouette with one or two separation cuts is clearer than a row of identical prongs. Keep the drawing order anatomically consistent as the hand moves behind and in front of the prop. Inspect the opening, maximum reach and release at full size and in the card crop. In silhouette alone the viewer should be able to tell which way the person is looking and what the hand is doing.

## Spatial behavior

Register the aperture, the scenery behind it and the closest obstruction on separate planes. Shift the nearest obstruction furthest and the horizon least. An offset must uncover something that was hidden. Keep a recognizable anchor on both sides of a transition so a change in scale feels like travel. Treat a thin light on one physical edge as an accent; allow it to end naturally where the edge turns away.

For a static application, show the occlusion with overlapping shapes, changing detail density and contact shadows. On an interactive surface keep the label fixed and move the inlay behind it. Use a visible focus ring and communicate state through position or form as well as hue. Under reduced motion, reveal the final arrangement immediately. On a narrow frame recompose around the aperture. Keep the clean reading zone and simplify small detail before reducing type.

# Tidal Intaglio on film

Render a moving editorial engraving in the tidal treatment of the accompanying visual system. Carry the supplied story through a changing physical aperture.

## Rendering the rules on film

At 30 frames per second interpolate position, rotation and exposure with continuous curves. A useful short gesture has a small preparation, a longer transfer and a breathable settle. It starts by showing the material already on screen. Local movement can continue under a deliberate compositional hold. Measure change at the edge between two plates; displacement at that edge tells the viewer more than rotation of the complete image. Let the first accelerative change be visible in the near plate. Bring the distant reflection to rest later and by a smaller amount.

Bind time to an explicit seek value and use the same trajectory on replay. Keep paper grain pinned to its own printed sheet. Use a different seed for the next sheet but maintain the prior seed right up to the actual replacement. On water, draw the reflection as a set of broken horizontal strokes whose width follows their distance from the horizon. Drift a subset sideways and shift their opacity at slightly different rates while preserving an overall light column.

A semitransparent plate has a contact edge and a body. On entry advance the edge before the density settles. On the next action let the lower plate travel behind it. On exit delay the small last sliver caught between two contours by a few frames. A reveal should contain one point the audience can watch all the way through. A camera zoom applied to a single finished painting cannot create a new occlusion. Maintain genuinely separate regions and let at least one object previously hidden come into view.

## Narrative grammar

Map cause and effect to a physical dependency before selecting a transition. To show one input influencing several destinations, allow a printing wash to travel along the actual edges of a larger drawing; only the areas it reaches become readable. To show an error, shift one separation slightly out of register and expose an unmistakable doubled edge beside an error sign. To show recovery, register the edge again, tighten its contact shadow and show the correct sign. State and meaning must remain recognizable on a still frame with sound off.

For a before-and-after scene hold an invariant anchor such as a hinge, bank line or window. The same anchor must be visible both before and after the event so the audience knows what changed. For a sequence of stages, attach each stage to the recurring physical surface but give each one a different spatial treatment. Allow one to arrive in the aperture, the next to be embodied by a departing foreground object and another to come into focus on the revealed plane. Repetition of exactly one wipe for every event flattens the narrative rhythm.

Use one strong scale change during a climax. Hold the lower object in place while the camera traverses a hole in a much nearer sheet. Carry a strip of its contour toward the edge of the image so the change is continuous. Land on a complete composition with its own foreground, subject and light mass. Allow enough time for the newly revealed information to be understood. A camera move ending on a magnified piece of blank paint has spent the gesture without revealing anything.

## Transitions

**Aperture crossing.** Treat outline geometry and interior painting as separate coordinate systems. Compute the outline transform at time t, establish the clip, then draw a translated and scaled interior using its own world-to-view transform. Restore before drawing the exterior ink and the few feather, plating or stone edges that actually lie above the opening. When the aperture encloses the frame, its outer rim may travel out of view. Keep the inner scenery continuous across that instant. Test both sides of the switch with single frames and at playback speed.

**Eclipse by structure.** Anchor a column, shutter or long exterior leaf close to the lens. Make the width sufficient to physically cover the seam between two scenes. Accelerate smoothly toward the occlusion, change the plate while that area is covered, and emerge moving in the same direction. Set the duration from the actual screen coverage, not from a universal wipe timer. Design two reveal windows if the near object has perforations; the outgoing scene may still be visible in one while the incoming starts to appear in the other.

**Register and light.** Begin with an ink recess and two thin offsets of color, with the same underlying outline. As the print seats, align the offsets and reveal an interior image from one side. Release a very short cut of paper along the edge as pressure settles. This works for an emblem, icon or confirmation in a component. Use an original silhouette with a counter or incision engineered into its shape. The action must still be intelligible at reduced color saturation.

**Turn of a printed sheet.** Anchor one edge, compress the other in perspective and allow the reverse side to catch a cooler light. Show the thickness of the printed edge in the small middle window where the plane is almost side-on. Let the reverse material carry new content. In a short interface motion use one rotation and settle. In a film use a contact shadow detached from the leading edge to indicate its depth.

## Camera and registration

Define a world larger than its final view and include overscan on every moving plate. The furthest atmosphere might take 3 to 7 percent of nominal travel, far architecture 16 to 25 percent, middle subject 35 to 55 percent, and a near screen 90 to 135 percent. Choose values that reveal actual information rather than chasing ratios for their own sake. Move the camera origin around a visual anchor when zooming. If the zoom targets an aperture, place the origin inside its thickest region so it does not accidentally escape through empty background.

For an oblique push add mild pitch or a change of lens centering on the near plate only if the apparent geometry supports it. Building verticals should stay coherent. Preserve a believable relationship between the advancing film plane and the horizon. Let a near object pass close enough to show its carved ridges. Keep the horizon gently moving behind the mask. Avoid moving the sun a large distance relative to the very remote cloud band. An extreme difference between perceived distances already provides drama without additional shakes.

Judge one frame early, one at contact and one after the camera has passed through the aperture. Find a point on each plane and track it relative to its neighbors. Something that was genuinely covered must become visible. Check two adjacent frames on the most rapid move. If a black border, unpainted canvas edge or single-frame changing mask is visible, extend the paintings, match transforms and rerender. Do not paper over the error with a full-frame flash.

## Sound

Compose original sound from local oscillators, filtered noise, envelopes and delays. Begin with a low rounded fundamental and a quieter fifth to give the ink weight. Introduce a small high-frequency detail only where a metal edge catches. Tie the paper contact and the start of the camera move to the same timeline. Separate the rise of a gesture from its transient. Leave a short decay audible after the object settles.

| Event | Source | Envelope and placement |
| --- | --- | --- |
| Ink running | Low-pass noise and a sine undercurrent | Open the filter slowly from about 260 to 680 Hz over the advance; roll the tail under the next stroke. |
| Paper contact | Short, dry filtered noise burst | Attack in 4 ms, release over 75 ms, pan slightly toward the point of contact. |
| Brass fitting | Two detuned sines near 620 and 930 Hz | Strike softly, let the higher partial die first, decay the lower under 240 ms. |
| Shutter slide | Narrow midband brushing noise | Swell for the travel time, stop the brush before the catch locks. |
| Open water | Low airy wash with irregular slow modulation | Maintain width but keep the center clear for the primary event. |
| Interior revealed | A pair of soft pitched reeds above the low tone | Increase the second voice smoothly as the aperture opens and reduce the noise bed. |
| Misregistration | Two brief, close dry ticks | Separate them enough to hear the doubled edge, then leave space for recovery. |
| Registration | One definite wood-and-metal transient | Align the attack to the first settled frame and let the resonance stay quiet. |
| Final light | Short high harmonic from the established chord | Hold the fundamental and allow the new upper partial to disappear into ambience. |

Use the host contract for export loudness and true peak. Measure the final encoded file, not only the offline buffer. Avoid broad hiss during a quiet hold. No soundtrack from a reference enters the work. The print should still explain its own movement muted. Interactive components are silent by default; keep confirmation understandable through form, position and a meaningful programmatic state.

## Cover and review

The best cover usually comes just before the silhouette begins to occupy the entire view: its outline is still recognizable and there is enough interior detail to reward inspection. Another valid cover is a newly revealed vista framed by a real foreground object. Inspect both at gallery size. Choose the frame in which important edges remain separated and the light shapes read as a small group rather than a field of specks. Never infer quality from the number of generated paths or the duration of a render.

Review with the palette reduced to luminance, at small size, and with textured layers temporarily hidden. Confirm the silhouette reads in all three conditions. Play the full shot at normal speed once while watching the near edge and again while watching the distant horizon. The near edge should conceal and reveal parallax; the horizon should feel grounded. Check a stationary point on the subject for grain crawling, especially after video compression. Render a clean frame beyond both extremes of travel before final cropping.

## House animals

Two recurring animals live in the background of every film that has room for animal life. They are not part of the story: they never act out a step of the brief, never carry a caption, and never take focus from the brief's characters. They are the film's running gag and its signature. Draw them in the medium of the style (ink, paint, print, clay, pixels), but keep their shapes, proportions and behavior exactly as written here, so they read as the same two animals in every style. They replace any generic background animal the style might otherwise use (birds, pets, lizards).

Proportions are given in **head units (h)**: the height of that animal's head.

### The capybara

Calm, round, unbothered. The world can explode around it; it keeps sitting.

- **Body:** one soft barrel, a rounded rectangle 3.4h long and 2.0h tall, with the back as one smooth arc slightly higher at the hips than at the shoulders. No visible waist, no neck: the head joins the body directly.
- **Head:** a large blunt block 1.6h long and 1.0h tall, with rounded corners. The muzzle is deep and square: the front of the face is an almost vertical flat plane, the top of the head an almost straight line from the ears to the nose.
- **Nose:** two short nostril slits high on the front plane, near the top corner. A soft vertical cleft runs down to a small closed mouth.
- **Eyes:** small (0.14h), set high, near the top line of the head and about one third back from the nose. Always relaxed: half-closed, lids as one gentle downward curve. They open fully only once, at the film's single biggest impact, and close again.
- **Ears:** two small round ears (0.22h) set far back and high, slightly cupped.
- **Legs:** four short straight legs, 0.6h tall, mostly hidden under the belly when it sits. Front feet with four short toes, back feet with three, each toe a small rounded wedge.
- **Tail:** none.
- **Coat:** warm reddish brown, slightly lighter on the belly and under the jaw, darker along the spine. Coarse: a few short dry strokes or texture marks along the back, never fluffy.
- **Size:** about 0.55 of an adult human's height at the shoulder, so it reads clearly next to people.
- **Behavior:** sits or lies like a loaf, chewing slowly (jaw moves 2 times per second). Things land on its head (a fruit, a leaf, a falling paper, a small object from the story's world) and it does not react, except for one slow blink. It moves at most twice in the film, at a calm walk.
- **Sound:** a soft low huff (pink noise, lowpass 400 Hz, 180 ms) when something lands on it; gentle chewing clicks (filtered noise, 1.2 kHz, 15 ms, 2 per second) at very low level when the camera is close. Never squeaks.

### The sloth

Slow, wide-eyed, always one beat behind the rest of the world.

- **Body:** a shaggy pear, 2.2h tall, hanging or clinging, never walking upright. Arms are very long (2.6h), legs shorter (1.6h), each limb ending in three long curved claws (0.5h), slightly darker than the coat.
- **Neck:** long and slightly arched, 0.9h, so the head can swing and turn far from the body; it bends like a hook when the sloth hangs upside down and looks at the camera.
- **Head:** small and round, slightly wider than tall (1.1h wide, 1.0h tall), with a short flat face.
- **Eyes:** big and bulging, each 0.32h, two round domes set high on the head and slightly apart, with small black pupils. The eyes are the joke: in surprise they swell to 0.38h and the pupils shrink to dots; when confused, each pupil looks a slightly different way.
- **Face marks:** a pale face disc with a dark mask stripe running back from each eye toward the ear, like a three-toed sloth. This mask is the sloth's identity mark and must always be visible.
- **Nose and mouth:** a small dark oval nose; a gentle closed smile. No teeth showing, no overbite.
- **Coat:** long, shaggy, greyish beige with a faint green tint (algae), lighter on the face. Hair hangs downward from the limbs with gravity.
- **Size:** about 0.45 of an adult human's height when hanging stretched.
- **Behavior:** hangs from whatever is high in the scene (a wire, a branch, a lamp, a frame, a shelf). Moves at one quarter of the speed of everything else. Reacts to every big event about 0.8 s late: when everyone has already moved on, the sloth slowly turns its head, eyes swelling. Once in the film, it reaches for something that is no longer there.
- **Sound:** a slow wooden creak of the thing it hangs from (bandpass noise 300 to 500 Hz, 400 ms) when it moves; one long soft yawn (sine 260 to 180 Hz through a 700 Hz formant, 0.9 s) late in the film. Never speaks.

### Rules

- Both are original animals, not any existing cartoon character. No buck teeth, no overbite, no lisp, no clothes, no human hands, no speech.
- Both appear in at least three moments of the film, one of them the final image (the capybara sitting at the edge of the frame, the sloth hanging above it), small enough never to compete with the brief's characters.
- If the style has no place for animals (pure typography, abstract diagrams), leave them out.

## Content

Tell the film what to show: the subject, the main character, the steps or items to explain, any numbers, and the closing line. One idea that fits 10 to 16 seconds. If something is missing, choose it yourself and do not ask.

## Technical delivery

Deliver one complete, self-contained HTML file. Do not ask for approval and do not send a storyboard first: go straight to the finished film.

- Picture is drawn on one `<canvas>` of 1920x1080 at 30 frames per second, scaled to fit the browser window.
- All sound is synthesized with the Web Audio API. No image, video or audio files. The only thing that may load from the network is Google Fonts.
- A single Play button starts picture and sound together. It can be pressed again to replay.
- Every frame is a pure function of time, so any instant can be drawn in any order. All randomness comes from a seeded generator: never use `Math.random`, `Date` or `performance.now` inside drawing or sound scheduling.
- The final mix should measure around -16 LUFS with true peaks below -1 dBFS in the exported video. Encoding the audio adds up to 3.5 dB of overshoot, so the last stage of the mix must hold sample peaks at or below -4 dBFS. Use gain riding and compression to reach the loudness; never use a hard clipper.

## Continuous motion (applies to every style)

The point of a film made in code is that nothing jumps. Every frame is computed, so every change can be gradual.

- **Every property moves a little on every frame**, at 30 frames per second: position, size, rotation, opacity, color, perspective, shadow, blur, line length, fill level. Interpolate from the previous state with an easing curve; never set a new value from one frame to the next. Moving from x to x + 30 takes many frames (x + 1, x + 2, x + 3...), not one.
- **Every element has a beginning, a middle and an end.** It enters with a visible motion of at least 0.3 s (grows from a point, slides in, draws on, unfolds, is carried in, rises into focus), with an ease-out and a small overshoot. While on screen it keeps a secondary motion (breathing, drift, sway, idle, shimmer). It leaves with a visible motion (shrinks, slides out, is covered, falls away, fades into the background). Nothing appears or vanishes on a single frame.
- **Depth and light move too.** Things coming closer grow, sharpen and gain contrast; things moving away shrink and fade toward the background color. Shadows follow their objects and stretch with the light. The camera moves in perspective, with near layers moving faster than far ones.
- **Changes of place are continuous camera or world moves** (push in, pull back, pan, crane, a physical object covering the frame) lasting 0.4 to 1 s. A hard cut only marks a jump in time, at most once per film.
- **The frame is never still.** Even during a hold, something moves: idle breathing, a drifting particle, a slow camera creep. No more than 15% of frames may be identical to the previous one.
- **Stepped motion only on purpose.** If the style asks for animation on twos or pixel steps, the steps are small and regular along a continuous path; it is never a jump to a distant position.
- **Before delivering**, step through consecutive frames at the busiest moments. Fix any element that moves more than about 48 px between two frames without motion blur or a smear, and any element that appears or disappears from one frame to the next.

Expose this object so the film can be exported to video:

```js
window.film = {
  canvas,            // the canvas element
  width: 1920,
  height: 1080,
  fps: 30,
  duration,          // total seconds
  ready,             // Promise that resolves when fonts and pre-rendered layers are ready
  seek(seconds),     // draws exactly that instant on the canvas
  renderAudio(),     // Promise<AudioBuffer>: the whole soundtrack, stereo, rendered in an
                     // OfflineAudioContext by the same code that plays it live
}
```
