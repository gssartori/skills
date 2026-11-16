# Clockwork Orbits

Build one finished animated film as a brass orrery on a collector's table: whatever the content brief tells becomes a mechanism of polished brass arms, stacked tubes and gears turning around a gilded center, with the story's things riding the arms as small spheres of stone and enamel, and its people as cast brass figurines with enamel faces. One crank drives everything. The story and technical delivery follow this text.

## The film you must not make

The predictable version: a flat yellow solar system on a starfield, orbit lines drawn as thin circles, planets as glowing gradients, icons orbiting a logo, a space synth pad. All of that fails. This film looks like a museum piece filmed on a quiet afternoon: weight, polish, exact gearing, light sliding across metal.

## 1. Identity

**Contract.** A brass mechanism on deep green velvet and green baize, lit warm from the upper left. Metal reads as metal through long soft highlights, never through flat yellow. Every motion is driven by visible gearing.

**Three signatures that any still frame must show:**

1. Brass arms radiating from stacked concentric tubes around a gilded center, each arm ending in a small sphere or figurine.
2. An engraved calendar ring around the base drum, with fine tick marks and engraved numerals, turning slowly.
3. Long soft highlights that slide along brass surfaces as the pieces turn, with soft shadows of the arms falling on the drum and the baize.

**Three exclusions:** never drawn orbit lines, starfields or glow halos; never a flat yellow fill for brass; never a part that moves without a gear, arm or crank driving it.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the table, never a stretch.

## 3. Material primitives

Render the velvet, the baize, the drum, the calendar ring artwork and every sphere's surface texture once into offscreen canvases; per frame, draw only transforms, the moving highlights and shadows.

- **Velvet backdrop.** `#1F3A2E` at the center to `#0E1D17` at the corners (radial), with a seeded fine nap texture at 3% alpha.
- **Baize table.** `#2E5A3F` with a felt grain (seeded speckle, 4% alpha), meeting the velvet at a soft horizon line 62% down the frame in the wide view.
- **Brass.** Never one flat color. Each brass surface is a linear gradient along its length: shadow `#6B4A16`, body `#B8892E`, light `#E3BE6A`, highlight `#FFF1C4` in a narrow band (6 to 10% of the surface width). The highlight band position is computed from the light direction and the part's current angle, so it slides as the part turns. Edges get a 1 px darker rim `#4A3310`.
- **Brushed drum top.** Radial brushing: 180 seeded hairline strokes from the center outward at 5% alpha, pre-rendered.
- **Gears.** Real involute-looking teeth (12 to 60 teeth, tooth depth 6 to 10% of radius), spokes cut out (4 to 6), a hub with a dark axle hole. Meshing gears turn at the ratio of their tooth counts, in opposite directions, teeth interlocking on screen.
- **Spheres (stone and enamel).** Each body has its own pre-rendered surface: polished stone with seeded veining (agate bands, lapis flecks, carnelian cloud, pewter grain, ivory smoothness, tiger's-eye chatoyance). Light from the gilded center and from the key light: a terminator line on the side away from the center, a small specular dot `#FFFFFF` at 60% alpha on the key-light side.
- **Gilded center.** A sphere of gold leaf (`#D9A93A` to `#FFE7A1`) with a faint warm inner glow that brightens the facing sides of nearby spheres. This is the only light source inside the scene.
- **Shadows.** Soft (8 to 18 px blur), offset down and right from the key light, cast by arms and spheres onto the drum and the baize, moving with them every frame.
- **Lettering.** Google Fonts: `Cormorant Garamond` (600) for titles and the large words, `Cormorant SC` (500) for engraved labels, tracked 0.08 em, warm ivory `#F2E6C8`; numerals on the calendar ring and the legend plate in `Cormorant Garamond` with lining figures. Minimums at 1920x1080: titles 72 px, essential labels 42 px, key numbers 110 px, captions 40 px.
- **Legend plate.** A brass plate in a corner with a double rule, carrying live counts (revolutions, totals) that tick as the crank turns.
- **Palette.** Velvet, baize, the brass ramp, gold, the stone colors (pewter `#8E9297`, ivory `#EDE3CC`, lapis `#2C4E9A`, carnelian `#B5462C`, agate bands `#C79A6B` and `#7A4E33`, tiger's-eye `#A8742A`), ivory type. Nothing else.
- **Finish.** A very soft vignette and a 1.5% film grain, re-seeded every frame.

## 4. Material time

Weighty and smooth at 30 fps. The crank eases in over 0.6 s and out over 0.8 s (`cubic-bezier(0.45, 0, 0.2, 1)`); everything driven by it accelerates and slows with it. Inner arms move fast, outer arms slowly, always at the gear ratio, so the mechanism never moves as one block. Nothing bounces: brass settles with a single 2 px overshoot and a 0.15 s return, as if damped by oil. When nothing in the story moves, the escapement still ticks and the calendar ring still creeps (at least 0.4 degrees per second), so no frame repeats.

**Entry, life and exit of every part.** A new arm slides up its tube from below the drum (0.5 s) and swings out to its radius; a sphere is lowered onto its arm tip by a tiny brass claw and settles 3 px. A figurine rises through a trapdoor in the drum top, turning a quarter turn as it rises. Labels engrave in letter by letter (a burin line traces each letter, then the groove darkens). Exits run backwards: parts swing in, sink into their tubes, the trapdoor closes. Nothing appears or vanishes in one frame.

## 5. Piece vocabulary

Turn any noun of the brief into one of these.

- **The mechanism** (the brief's world: a company, a team, a system, a year). Center, tubes, arms, drum and ring. One part changes when the story changes: an arm extends, a gear engages, the ring advances.
- **Figure.** See Cast construction.
- **Item.** A sphere on an arm tip, of its own stone or enamel, with the item's most recognizable silhouette inlaid on its face in gold (a simple engraved pictogram, 2 px line), turning toward the camera as it passes.
- **Gear train.** A visible chain of 2 to 5 meshing gears carrying motion from the crank to the part that matters. Showing the train is how the film shows cause.
- **Engraved label.** On a brass tag hanging from the part by a hairline chain, or engraved on the drum beside it, with a hairline leader. Never floating in the air.
- **Caption.** One line engraved on a brass strip along the bottom of the frame, 80 px above the edge; the old line scrolls off as the strip slides, the new line engraves in. At least 1.6 s on screen.
- **Counter.** The legend plate: a number on drum-type wheels that roll digit by digit (each digit wheel turning continuously, not jumping), at least 110 px when it is the key number.
- **Error mark.** A gear tooth slips: the train shudders 3 times (2 px), one arm stalls and droops 4 degrees, a small brass spring pops loose. **Success mark:** a pawl clicks into place, the arm lifts back and the train runs smoothly again.
- **Emphasis.** A brass pointer on the calendar ring swings to point at the key part, at most once per scene.

## 6. Story grammar

### Cast construction

The style does not know who is in the story. It says how anyone the brief describes is built as an orrery piece.

- **Figures as cast brass figurines** on small round plinths, with enamel faces in warm skin tones of the brief's people (smooth, two-tone shading, small painted eyes with a highlight, a short painted brow, a small mouth), cast brass clothes with the same brass ramp and sliding highlight, and articulated arms that pivot at the shoulder and elbow like automata. Bodies are modeled, not geometric: rounded shoulders, tapered limbs, hands with a thumb, folds cast into the clothes.
- **Life.** Every figurine breathes (plinth rises 1 px on a 3 s cycle), blinks (eyelids are enamel shutters, 4 frames), and turns its head toward whatever speaks or moves. Gestures are automaton gestures: a smooth arc with a soft stop.
- **Scale.** In main scenes the figure in focus is at least one third of frame height with a face of at least 50 px: the camera comes close to the arm carrying it. With more than 4 figures, show 2 to 4 at a time as their arms sweep past, and gather everyone only at the reunion moment (all arms aligned), where no face is under 24 px; whatever does not fit becomes a group plinth with one large representative.
- **What the brief says about a person** becomes casting and enamel: a beard as a cast textured area, glasses as two fine wire rings, a job as one prop cast in the hand, a role as the color of the enamel sash. Each figure keeps the same marks all film.
- **Several figures:** distinct by silhouette and by sash color, never by a caption alone.
- **Originality.** No real person, mascot, logo or brand.

### A list of N things

Never assume N. Items become spheres on arms.

- **N up to 8:** each item gets its own arm at its own radius, revealed in turn every 0.25 to 0.4 s, each with an engraved tag.
- **N from 9 to 30:** items are grouped. Each group is one arm carrying a small sub-orrery (a moon carrier) whose 2 to 6 small spheres turn around the group's main sphere; one tag names the group, and the legend plate lists the members.
- **N above 30:** the first group is shown in detail; the rest become a ring of small beads on the calendar ring (each bead still inlaid with a tiny pictogram), and the counter gives the total.
- Every sphere enters, turns and settles the same way. Two spheres that could be swapped without anyone noticing have failed.

### Steps

Each step of the brief is one **engagement**: the crank turns, a new gear meshes into the train, a new arm or ring starts turning, and the mechanism keeps everything already running. The steps accumulate: by the end, the whole orrery turns. Group two steps per engagement when they share one.

### Cause, error and fix

Cause is always the gear train: show the gear that drives the change before the change happens. If the brief has an obstacle or a mistake, use the error mark: the slip, the stall, then the pawl and the recovery.

### Numbers and short words

A number or short word the brief puts on screen is engraved on a brass plate or on the calendar ring, in `Cormorant Garamond` 600, at least 110 px (150 px or more when it is the key image), engraving in letter by letter.

### Climax and ending

Exactly one moment is the biggest in the film: the brief's key image, shown as an alignment. Before it, 0.3 s of stillness: the crank holds, the escapement stops ticking and the music stops. Then the crank makes one full turn, every arm swings into a single line (a conjunction), the gilded center opens like a flower of eight gold petals and lifts the key image on a brass stem, and light from inside the center flares across every sphere. The last image is the whole orrery aligned, the closing words or number largest in frame, held at least 1.2 s with the calendar ring still creeping and highlights still sliding.

### Pacing by duration

Hook within the first frame: the mechanism is already turning, close on the gilded center. Something changes every 1 to 2 s. About 10 s: 3 engagements. 13 to 16 s: 4. Before drawing, write a beat table: one row per beat with start and end time, the exact on-screen text, the physical cause that moves us to the next beat, and the main sounds. Picture and sound both read times from that table.

## 7. Transitions

Every change of place is a continuous move of the camera or the mechanism, 0.5 to 0.9 s.

1. **Ride the arm.** The camera follows an arm as it sweeps to the next figure or item.
2. **Down the train.** The camera tracks along the gear train from the crank to the part it drives.
3. **Through the ring.** The calendar ring rotates past the lens and the next scene is behind it.
4. **Rack focus.** Focus shifts from a near sphere to a far one over 14 frames.

Never a dissolve, a generic wipe or a hard cut to change idea. A hard cut only for a jump in time, at most once, with a 6-frame warm flash.

## 8. Camera

A continuous orbit: never still. It starts low and close on the gilded center, pulls back to a three-quarter view over the table, comes close to each figure in focus, and ends in a calm three-quarter wide view with the whole orrery. Perspective is real: near arms move faster across the frame than far ones, near parts are larger and slightly soft (shallow focus in close shots), shadows stretch with the light. Vary shot sizes: close on the hook, wide reveal, two-shot of figurines, insert on a gear, close reaction, wide ending. Line weights and labels stay at their minimum size on screen.

## 9. Sound

A quiet study with a clock collection, and a chamber score. Picture and sound share one clock; every sound lands on the frame of visible contact (a tooth meshing, a pawl dropping, a sphere settling), within one frame.

**Helpers.** `nz(t, kind, filter, f, Q, a, d, lvl)`: seeded white, pink or brown noise. `pluck(t, f, dur, lvl)`: Karplus-Strong in plain JS. `bell(t, f, dur, lvl)`: sine with partials at 2.76 and 5.40 ratios, fast decay. `pad(t, freqs, dur, lvl)`: detuned sines through lowpass 1400 Hz with a slow attack. Levels in dB. No speech.

**Bed.** Room tone (pink noise lowpass 2000 Hz, -40 dB) and the escapement: a soft tick-tock (white noise bandpass 3000 Hz, 12 ms, alternating 2900 and 3300 Hz) at 2 per second, -26 dB, always running except in the stillness before the climax.

**Music.** A chamber cue at 72 BPM in A major: a music-box line (bells on eighth notes), plucked cello on the roots, and a warm string pad that adds one voice with each engagement.

**Vocabulary.**

- Gear meshing: a short metallic ratchet, 3 to 6 clicks (white noise bandpass 2500 Hz, 8 ms each), -18 dB.
- Arm rising from its tube: a smooth brass slide, pink noise bandpass sweeping 600→1400 Hz, 0.5 s, -22 dB.
- Sphere settling: a small stone-on-brass clink, bell at 1800 Hz, 60 ms, -16 dB.
- Trapdoor and figurine rising: a soft hinge creak and a felt thump, -20 dB.
- Engraving letters: a fine burin scratch, white noise bandpass 5000 Hz, following the stroke, -28 dB.
- Counter wheels: a fine tick per digit at 1600 Hz, at most 12 per second; lock with a bell.
- Gear slip: a harsh grind (sawtooth 90 Hz through bandpass 1200 Hz, 0.3 s) and a spring boing; pawl recovery: a crisp double click and a rising two-bell figure.
- Climax: the music and the escapement stop 0.3 s before; then one deep crank rotation (brown noise lowpass 250 Hz rising, 0.6 s), a chime of eight bells as the petals open (a major chord spread over 0.4 s), and the full string pad. It is the single loudest moment.
- Ending: the music box plays the opening motif once, slower, over the escapement returning.

**Density.** 3 to 10 audible events per second; at most 3 foreground sounds at once besides music and bed; repeated ticks at most 12 per second.

**Mix.** Music ducked 4 dB under each foreground hit by scheduled gain; pan by screen position, `(x / 1920 - 0.5) * 1.2`. Loudness and peaks as the technical delivery asks.

## 10. Hero frame

The last frame: the whole orrery in a three-quarter view on the baize, all arms aligned, the gilded center open with the key image on its stem, the closing words or number largest in frame, every figurine readable, the calendar ring and the legend plate in place. It must read as this style with no caption.

## 11. Style check

Never ship a stub or "similar for the rest": every figure, item and engagement the brief asks for must exist, drawn. A long file is expected. Inspect frames at 0%, 10%, 25%, 50%, 75% and 95% of the duration, and inspect at least three close-ups at full resolution:

- Is the mechanism already turning in the first frame?
- Does every brass surface show a sliding highlight and a rim, never a flat yellow?
- Do gears visibly mesh at their ratio, and does every moving part have a visible driver?
- Are there no orbit lines, starfields or glow halos?
- Are figurines modeled (rounded, tapered, with hands and cast folds), not built from visible circles and rectangles?
- Are figures in focus at least one third of frame height, faces at least 50 px, distinct and the same all film?
- Are all items spheres of distinct stone with an inlaid pictogram, no two interchangeable?
- Are the two house animals cast as brass figurines with enamel details, readable at their size?
- Does something move in every frame, and does every part enter and leave with visible motion?
- Is there exactly one alignment climax, and does the last frame hold at least 1.2 s with the closing text the largest element?
- Text at 1920x1080: titles 72 px, essential labels 42 px, key numbers 110 px, captions 40 px, never smaller.

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
