# Ink Diorama

Build one finished animated film as a cartoon short: flat 2D bean-head characters, drawn like paper cutout cards with plum outlines, act inside a colorful toy-like world of painted boxes, planks, stone and plaster, every edge of the world inked in black, shot by a gliding camera with shallow focus. Whatever the content brief tells is staged as a little story with a hook, escalating beats and a payoff. The story and technical delivery follow this text.

## The film you must not make

The predictable version: characters pasted flat on a static background, a slideshow of scenes joined by fades, a camera that never moves, gray untextured shapes, captions narrating what we already see, a march loop with stock whooshes on every cut. All of that fails. This film feels like a short from a small animation studio: a built world you could walk into, characters who never freeze, and a camera that glides from one beat to the next.

## 1. Identity

**Contract.** A 2.5D diorama rendered in Canvas 2D: the world is built from simple solids (boxes, wedges, cylinders, half-buried spheres) projected in perspective and painted with flat textures, every silhouette and crease inked in black; the characters are flat cards standing in that world, turned to face the camera, with their own plum outline.

**Three signatures that any still frame must show:**

1. Black ink lines on the world's outer silhouettes and depth jumps (about 2.5 px at 1080 lines), thinner on creases, fading out with distance.
2. Bean-head cartoon cards: a big rounded head, a small body, plum outline 5 px, flat fills, a simple expressive face.
3. Depth of field: foreground and background softly blurred in close and medium shots, focus on the eyes; wide shots sharp.

**Three exclusions:** never a static frame (nothing holds still for more than 4 frames); never a gradient sky without painted cloud cards; never a character without a contact shadow on the ground.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. Diegetic text (a sign, a carved word, a label on a box) is welcome and must read correctly, never mirrored. A requested aspect ratio is a recomposition, never a stretch; in vertical, stage characters in depth, not side by side.

## 3. Material primitives

Build every texture and card once, before `ready`. Per frame: project, sort by depth, draw, ink, blur by layer.

- **World solids.** Boxes, wedges (roofs, ramps), cylinders (posts, towers, trees), half-buried spheres (hills), cones (mountains with snow caps), planks and beams. Projected with a simple perspective camera (vertical field of view 34 to 45 degrees). Each visible face is filled with its painted texture at a constant texel density and a 2-step toon light: lit faces at 100%, faces turned away at 72%, with one cast shadow shape from the sun.
- **Painted textures.** Drawn once on small canvases in a flat-with-dark-seams style: planks (boards with darker gaps and nail dots), beams, stone blocks with mortar, moss and ivy dabs, grass tufts, dirt, plaster with cracks, roof tiles in staggered rows, marble veins, cloth banners. Seeded so each surface varies.
- **Ink.** Draw the outline of every world shape's silhouette and its depth jumps in `#1A1414` at 2.5 px; creases between faces at 1.5 px; ink fades to 0 between 60% and 100% of the scene depth. Characters are never inked by this pass; they carry their own outline.
- **Character cards.** Each character is drawn once per pose and expression on an offscreen canvas (design size 600 x 1000, soles at y 975) and placed in the world as a vertical card turned to face the camera, scaled by perspective. Redraw a card only when its pose or expression visibly changes. Each card has a soft contact blob on the ground and a flat shadow shape cast by the sun.
- **Sky and distance.** Sky as a flat color by light preset, with 4 to 8 painted cloud cards drifting 6 to 10 px per second; distant hills, mountains and tree silhouettes in 2 or 3 parallax layers, tinted toward the horizon color (fog = horizon color at distance).
- **Depth of field.** Render the scene in 3 depth layers (background, middle, foreground) to offscreen canvases; blur background and foreground with `filter: blur()` by a circle-of-confusion of 8 to 14 px in close and medium shots, 0 in wides. Focus moves in about 14 frames when it racks.
- **Grade.** A gentle final grade: saturation 1.08, a warm lift in the shadows, a vignette at 12%, and a full-frame white flash available for time jumps.
- **Lettering.** Google Fonts: `Lilita One` for big words and diegetic signs, `Nunito` (800) for labels. Diegetic text is painted onto world surfaces (signs, boxes, banners) in perspective. Minimums at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px.
- **Palette.** Bright and clear, never neon: sky day `#9FD3F2`, golden `#F7C27A`, night-blue `#3E5A8C`; grass `#7CC15A`, moss `#5E9A48`; wood `#B5794A`, dark wood `#7A4E2E`; stone `#C9C0B2`; plaster `#F2E3C8`; roof tile `#C9623F`; water `#5FB4D8`; character skins `#F6C9A6`, `#E3A67C`, `#B97A52`, `#8D5A3B`, `#5E3A26`; outline plum `#4A2340`; ink `#1A1414`.
- **Finish.** Something secondary always moves: banners wave, leaves fall, dust drifts, water flows, smoke curls.

## 4. Material time

Smooth at 30 fps for camera, light and world; character cards may animate on twos (15 fps) for a hand-made feel while their idle and position stay smooth. No frame holds still for more than 4 frames: every hold has a creeping camera, idle breathing (head bob 2 to 3%), blinks every 2 to 3.5 s, and secondary motion.

## 5. Piece vocabulary

Turn any noun of the brief into one of these.

- **Character.** See Cast construction.
- **Set piece** (the central object or place: a machine, a building, a bridge, a ship, a tower). Built from solids with painted textures and a part that physically changes when the story changes: a door that swings, a roof that lifts, a wheel that turns, a wall that collapses in staggered parts, driven by a 0 to 1 progress with eased and staggered pieces.
- **Prop.** A small painted solid or a flat card held by a character; props carry the jokes.
- **Item.** A crate, a jar, a scroll, a sign, a banner: each a small solid with a painted face that shows the item's pictogram or word, so any noun becomes a labeled object in the world.
- **Arrow or link.** A rope, a rail, a path of planks, a line of footprints, a stream of water that runs from one thing to another.
- **Label.** A painted wooden sign on a post or a hanging board, in perspective, never a floating caption.
- **Counter.** A tally painted on a board, or crates that stack up; each step lands with a small thunk; at most 12 per second.
- **Effects.** Dust puffs, Zzz, sweat drops, swirl lines, sparkles, drips: small flat cards in the characters' style with a plum outline.
- **Error mark.** Something in the set piece cracks, wobbles or falls; the character reacts (squint, cheek in hand, swirl above the temple). **Success mark:** the part settles into place with a bounce, a sparkle card pops, and the character cheers.
- **Emphasis.** A push-in with a 3 to 5 degree roll on the key object.

## 6. Story grammar

### Cast construction

The style does not know who is in the story. It says how anyone the brief describes becomes a bean-head card.

- **Construction.** Head a rounded bean about 40% of the figure's height; small torso and short limbs; plum outline 5 px; flat fills with one darker shade shape per part. Face: two oval eyes with white catchlights, simple brows, a nose bump, a mouth stroke that opens into shapes. Expressions: neutral, smile, laugh, surprise, worry, stubborn, squint, snore.
- **Poses.** Arms: hang, point, up, wave, hand on hip, hand on belly, hand to temple, lift, reach, hand to cheek, arms crossed, thumb up. Hands hold props firmly.
- **What the brief says about a person** becomes an outfit and a prop: hair, cap or helmet, beard, glasses, apron, coat, tunic, dress, a tool of the job. A beard is a flat shape along the jaw one step lighter than the hair. Every character keeps the same outfit and marks all film.
- **Scale.** In main scenes the character in focus is at least one third of frame height with a face of at least 50 px. With more than 4 characters, show 2 to 4 at a time as the camera passes, and gather everyone only at the reunion moment, where no face is under 24 px; whatever does not fit becomes a group with one large representative.
- **Several characters:** each distinct by silhouette, outfit color and headgear, never by a caption alone.
- **Acting.** Anticipation, overshoot and spring settle on every action. A stamp or landing is a 2-frame dip, a dust puff and a small camera kick. Laughs are an alternating tilt and bob. Walks plant their feet with a 3 to 7% bob.
- **Originality.** No real person, mascot, logo or existing cartoon character.

### A list of N things

Never assume N. Items become objects in the world.

- **N up to 8:** each item appears in the world one by one, every 0.15 to 0.25 s, carried in, dropped onto a table or hung on a line, each with its own small sound.
- **N from 9 to 30:** items are grouped. Each group belongs to one character and lives in one place of the set (a stall, a shelf, a cart, a room of a building), shown as the camera glides past; within a group the items stand in rows on shelves.
- **N above 30:** the first group in detail; the rest as a long market street or warehouse of shelves seen in a wide gliding shot, with a counter board giving the total.
- Every item is built the same way; variety comes from the painted face. Two items that could be swapped without anyone noticing have failed.

### Steps

Each step of the brief is one **shot**. Vary shot sizes in this order when it fits: close on the hook, wide reveal, two-shot, insert close-up on the key object, reaction close-up, a camera move through the set for the payoff. Something always continues from one shot to the next: the camera pulls back from a close-up into the wide, racks focus, cranes over a wall, pushes into an object.

### Cause, error and fix

Cause is something that physically travels: a rolling barrel, a rope pulled, water poured, a character walking. Obstacles and mistakes use the error mark; the fix is a physical action on the set piece, then the success mark.

### Numbers and short words

A number or short word the brief puts on screen is diegetic: painted on a big sign, carved into stone, spelled with crates, at least 96 px on screen (140 px or more when it is the key image), landing with a spring and a dust puff.

### Climax and ending

Exactly one moment is the biggest in the film: the brief's key image, treated as the twist. Before it, the music stops dead. At the moment, a low hit, a push-in with a 3 to 5 degree roll, and the set piece's biggest physical change lands on that frame, with every character reacting in the same frame. The last image shows the brief's last words or number largest in frame as a diegetic sign or carving, the cast around it, held at least 1.2 s with a creeping camera, idle breathing, blinks and secondary motion.

### Light by beat

Use light for meaning: day for the normal, golden for drama or decline, night-blue for explanation. Each preset changes the sky color, sun direction and shadow length; change preset across a camera move or with a 6-frame white flash on a time jump.

### Pacing by duration

Frame 0 is already the hook image. Something changes every 1 to 2 s. About 10 s: 4 shots. 13 to 16 s: 5 to 7 shots. Before drawing, write a shot plan: one row per shot with frames, on-screen text, setting, light, camera move, characters with poses and expressions, effects and sound cue. Picture and sound both read times from that plan.

## 7. Transitions

Prefer continuous moves inside one world. When a change of place or time is needed, 0.3 to 0.8 s:

1. **Pull back.** From a close-up into the wide, revealing the next situation.
2. **Crane.** Rise over a wall, roof or hill and descend on the other side.
3. **Push into an object.** Into a window, a doorway, a crate, until it fills the frame and opens onto the next place.
4. **Flash.** A 6-frame white flash for a jump in time only.

Never use a dissolve, a generic wipe or an unmarked hard cut.

## 8. Camera

Always moving. Glides between keys with a smootherstep over 18 to 45 frames; ease-out for reveals and whips; curved paths through via-points. Every hold creeps at 4 to 8 px per second. 3 to 5 degree rolls on drama; a 7-frame shake on impacts. Never place the camera inside a railing or a wall, never let a post cross a face, never put props closer than the near layer. Shallow focus on close and medium shots with focus on the eyes; wides sharp.

## 9. Sound

A bright cartoon score and foley, punchy but never louder than the story needs. Picture and sound share one clock; every sound lands on the frame of visible contact, within one frame.

**Helpers.** `nz(t, kind, filter, f, Q, a, d, lvl)`: seeded white, pink or brown noise. `pluck(t, f, dur, lvl)`: Karplus-Strong in plain JS. `brass(t, f, dur, lvl)`: two detuned saws through a lowpass that opens on the attack. `thump(t, f0, f1, dur, lvl)`: sine with pitch drop. Levels in dB. No speech.

**Music.** A short march-like loop at 112 BPM: kick and snare, a plucked bass, a brass pad on chords, a glockenspiel on top. It stops dead before the twist; a low drone continues under the payoff and the full band returns on the final word or image.

**Vocabulary.**

- Whoosh on big camera moves: pink noise bandpass sweeping 400→2400 Hz, starting 0.4 s before the peak of the move.
- Thunk on stamps and landings: `thump(90→55 Hz, 0.12 s)` plus a wood knock at 700 Hz.
- Rumble and crash on collapses: brown noise lowpass 200 Hz for 0.6 s, then a crash of 20 seeded debris ticks and a wood creak.
- Scrape on metal: bandpass noise 2500 Hz with a slow pitch slide, 0.4 s.
- Ting on reveals: a bell at 2600 Hz with ratios 1, 2.7, 5.1.
- Sting on the twist: music cut, a low hit (sine 55 Hz, 0.8 s) and a high bell.
- Creaks, snaps, splashes, snore, rustling leaves, water ambience: from the helpers, matched to what is seen.
- Footsteps: soft thumps on each planted foot.
- Counter: a small wood tick per step, at most 12 per second.

**Density.** 4 to 12 audible events per second; at most 3 foreground sounds at once besides the music; repeated ticks at most 12 per second; the twist is the single loudest moment.

**Mix.** Music ducked 4 dB under each foreground hit by scheduled gain; pan by screen position, `(x / 1920 - 0.5) * 1.2`. Loudness and peaks as the technical delivery asks.

## 10. Hero frame

The last frame: the set piece in its final state in warm light, the brief's closing words or number largest in frame as a diegetic sign or carving, the cast gathered in front with clear faces, black ink on the world, plum outlines on the cards, a soft background blur. It must read as this style with no caption.

## 11. Style check

Never ship a stub or "similar for the rest": every character, item and place the brief asks for must exist, built. A long file is expected. Inspect frames at 0%, 10%, 25%, 50%, 75% and 95% of the duration:

- Is frame 0 already the hook image?
- Is every world edge inked, and does every surface carry a painted texture?
- Are characters bean-head cards with plum outlines, contact shadows, and faces of at least 50 px in main scenes?
- Do shot sizes vary, and do shots connect by continuous camera moves?
- Does nothing hold still for more than 4 frames?
- Are diegetic texts readable and never mirrored, and is no face crossed by a post or railing?
- Are the two house animals built as cards of the same style, readable at their size?
- Is there exactly one twist moment, and does the last frame hold at least 1.2 s with the closing text the largest element?
- Text at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px, never smaller.

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
