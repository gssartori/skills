# Crayon Fridge

Build one finished animated film as a child's wax-crayon drawing made on the kitchen table: whatever the content brief tells is drawn stroke by stroke with crayons on white paper, then comes alive with the wobbly, boiling life of a drawing that wants to move. The story and technical delivery follow this text.

## The film you must not make

The predictable version: clean vector shapes with a "crayon" brush filter, perfect circles with a texture overlay, Comic Sans titles, a ukulele-and-whistle jingle. All of that fails. This film looks like the drawing a seven-year-old would proudly put on the fridge, filmed on the table where it was made: wax skipping over paper grain, scribble fills that overshoot, honest childish choices.

## 1. Identity

**Contract.** White paper on a mint laminate kitchen table, seen from above, drawn in wax crayon. Every line is a crayon stroke with pressure and grain; every fill is a back-and-forth scribble.

**Three signatures that any still frame must show:**

1. Wax texture: strokes that skip over the paper grain, leaving white flecks, denser where pressure is high.
2. Scribble fills that overshoot the outline by 3 to 10 px and leave small gaps, never a clean flat fill.
3. The child's world grammar: a blue sky strip along the top of the sheet, a sun in a corner with ray lines, a green ground strip with grass ticks.

**Three exclusions:** never a clean vector edge, a perfect circle or a straight ruled line; never a gradient or a soft shadow on the drawing; never a typeset font on the drawing (all text on the paper is hand-lettered in crayon).

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the sheet, never a stretch.

## 3. Material primitives

Pre-render the table, the paper, the paper-grain mask and a set of crayon stamp textures once into offscreen canvases. Strokes are paths sampled into many small stamps along their length; per frame, draw only strokes in progress and moving parts.

- **Table.** Mint laminate `#BFE3D0` with a faint speckle (seeded, 3% alpha) and a soft edge sheen. Scattered crayons lie on it: wax cylinders in the palette colors, with paper wrappers (a lighter band with a printed stripe), worn tips, and soft contact shadows.
- **Paper.** `#FBFAF5` sheet, slightly rotated (1.5°), with a seeded paper-grain mask (a fine bumpy noise). Wax only sticks where the grain is high, so heavy strokes cover 80 to 95% and light strokes 40 to 60%.
- **Crayon stroke.** A path drawn as overlapping elliptical stamps (6 to 14 px wide) along its length, each stamp multiplied by the grain mask, opacity following pressure (a seeded slow wobble between 0.6 and 1.0). Lines wobble: every point is displaced by seeded low-frequency noise (2 to 4 px). Strokes start and end with a slight hook.
- **Scribble fill.** A zigzag of strokes at a consistent child angle (about 30°), each zig 8 to 16 px apart, overshooting the outline by 3 to 10 px and leaving 2 to 6 small gaps. A second, lighter pass in a crossing angle on big areas.
- **Boil.** The drawing is alive: every 3 frames the wobble noise advances, so lines and scribbles shimmer in place by 1 to 2 px, with no change in brightness. Between boil steps, everything that moves in the story moves continuously every frame, so no two consecutive frames are equal.
- **Palette.** Table mint, paper, crayon colors: red `#E0342A`, orange `#F28A1F`, yellow `#F7CF24`, green `#3BA34A`, sky blue `#4FA3E0`, blue `#2453B3`, violet `#7B4BB5`, pink `#F07AA8`, brown `#8A5A33`, black `#2A2A2A`, peach `#F6C29A`. Off-paper text (only on the table, if any) in deep green `#1F5A3F`. Nothing else.
- **Lettering.** All text on the drawing is hand-lettered in crayon: built from strokes with uneven letter sizes (±12%), a slight baseline drift, and, once in the film, one letter reversed the way a child writes it, in a word that is not the key word. Use `Gaegu` or `Patrick Hand` from Google Fonts only as the skeleton of the stroke paths, never rendered as type. Minimums at 1920x1080: titles 80 px letter height, essential labels 50 px, key numbers 130 px, captions 44 px.
- **Finish.** The camera's view of the table: very soft vignette and 1.5% grain, re-seeded every frame. The drawing itself has no effects.

## 4. Material time

Lively and smooth at 30 fps. A crayon draws a stroke at child speed (300 to 700 px per second, a little faster in the middle of the stroke), and the crayon itself is visible as it draws: a wax cylinder with its wrapper, tilted 25°, moving along the path with a tiny shake. Fills scribble in at 0.3 to 0.8 s per area. Motion of drawn things is a child's animation: bouncy, with squash and stretch (up to 15%), anticipation and overshoot. The boil never stops.

**Entry, life and exit of every element.** An element enters by being drawn (outline first, then the scribble fill, then details), at least 0.3 s, often longer; lives by boiling and by its own small loop (a wave, a hop, a blink, smoke puffing, a sun winking); and leaves by being scribbled over with the background color, rubbed out by a pink eraser (crumbs flying), or by the sheet sliding off the table. Nothing appears or vanishes in one frame.

## 5. Piece vocabulary

Turn any noun of the brief into one of these.

- **The sheet** (the brief's world). Each scene is a drawing on a sheet; a new scene is a new sheet slid on top, or the camera moving across a big sheet.
- **Figure.** See Cast construction.
- **Item.** The item's most recognizable silhouette as a child draws it: a few confident strokes, a scribble fill in its color, one detail that makes it unmistakable, and a crayon label beside it.
- **Arrow.** A thick crayon arrow with a wobbly shaft and a big triangle head, drawn on in one stroke.
- **Label.** Hand-lettered beside its thing, with a wobbly underline or an arrow pointing to it.
- **Caption.** Hand-lettered at the bottom of the sheet, 90 px above the frame edge, written letter by letter; the old caption is scribbled out before the new one is written. At least 1.6 s on screen.
- **Counter.** Tally marks in crayon, four strokes and a crossing fifth, drawn as the number grows; or a big hand-lettered number that is rewritten (the old one scribbled out) at least 130 px when it is the key number.
- **Error mark.** A big crayon scribble-cloud of frustration over the problem, a wrong line drawn too hard (the crayon snaps in two). **Success mark:** the eraser rubs it out and the right line is drawn proudly, with a heart or a star beside it.
- **Emphasis.** A wobbly crayon circle around the key part, drawn twice over, at most once per scene.

## 6. Story grammar

### Cast construction

The style does not know who is in the story. It says how anyone the brief describes is drawn by a child.

- **Figures as a child draws people**, but carefully, as the child's best drawing: a round-ish head (never a perfect circle) with peach scribble skin, two dot eyes with a white gap, eyebrows, a curve smile, rosy cheek scribbles; a body as a shirt shape with arms that end in hands with fingers; legs with shoes. Hair as a burst of crayon strokes in the person's color.
- **Life.** Each figure breathes (body stretches 2%), blinks (the eyes become two short lines for 4 frames), waves, hops; arms swing as a whole, with squash on landing.
- **Scale.** In main scenes the figure in focus is at least one third of frame height with a face of at least 50 px. With more than 4 figures, show 2 to 4 at a time as the camera moves across the sheet, and gather everyone only at the reunion moment, where no face is under 24 px; whatever does not fit becomes a group with one large representative.
- **What the brief says about a person** becomes crayon: a beard as a brown scribble on the chin, glasses as two wobbly rings, a job as one prop held, a role as the shirt color. Each figure keeps the same marks all film.
- **Several figures:** distinct by shirt color and hair, never by a caption alone.
- **Originality.** No real person, mascot, logo or brand.

### A list of N things

Never assume N.

- **N up to 8:** each item is drawn in turn every 0.3 to 0.5 s around the sheet, each with its label.
- **N from 9 to 30:** items are grouped. Each group is drawn inside a big crayon box or cloud (2 to 6 small drawings per row), with one label per group.
- **N above 30:** the first group is drawn in detail; the rest become a crowd of tiny doodles filling a corner of the sheet, each still a recognizable tiny silhouette, and the tally gives the total.
- Every item is drawn the same way. Two items that could be swapped without anyone noticing have failed.

### Steps

Each step of the brief is one **drawing**: a new part of the picture is added on the same sheet (or a new sheet joins the table beside the first), and nothing already drawn is lost. Group two steps per drawing when they share one.

### Cause, error and fix

Cause is drawn: an arrow scribbles from the cause to the effect before the effect moves. If the brief has an obstacle or a mistake, use the error mark: the snap, the frustration scribble, then the eraser and the proud redraw.

### Numbers and short words

A number or short word the brief puts on screen is hand-lettered big in crayon, at least 130 px (180 px or more when it is the key image), each letter drawn in its own stroke, then colored in with a scribble.

### Climax and ending

Exactly one moment is the biggest in the film: the brief's key image, shown as the drawing coming fully alive. Before it, 0.3 s of stillness: the crayon lifts off the paper, the boil slows, the music stops. Then the key image is drawn in one bold sweep, the whole drawing jumps with joy (every figure hops, the sun spins and winks, stars and hearts are scribbled around), and the camera eases back to show the whole sheet on the table. The last image is the finished drawing with the closing words or number largest, the crayons around it on the table, held at least 1.2 s with the boil and one small loop still running.

### Pacing by duration

Hook in the first frame: a crayon is already drawing on the sheet, close up. Something changes every 1 to 2 s. About 10 s: 3 drawings. 13 to 16 s: 4. Before drawing, write a beat table: one row per beat with start and end time, the exact on-screen text, the physical cause that moves us to the next beat, and the main sounds. Picture and sound both read times from that table.

## 7. Transitions

Every change of place is a continuous move, 0.5 to 0.9 s.

1. **Across the sheet.** The camera glides over the paper to an empty area where the next scene is drawn.
2. **New sheet.** A fresh sheet slides in over the old one, a little crooked, and the crayon starts at once.
3. **Follow the crayon.** The camera follows the crayon from the end of one drawing to the start of the next.
4. **Pull back.** The camera eases back to the table and pushes in again elsewhere.

Never a dissolve, a generic wipe or a hard cut to change idea. A hard cut only for a jump in time, at most once, with a 6-frame paper-white flash.

## 8. Camera

Top-down over the table, never still: a slow drift, pushes in on figures in focus (close enough to see the wax grain), gentle 2 to 4° rotations, and one ease-back at the end that shows the whole sheet with the crayons around it. Vary shot sizes: close on the hook, wide reveal, two-shot, insert on a detail, close reaction, wide ending. The scattered crayons on the table move with parallax only through the camera, as objects on a flat table.

## 9. Sound

A kitchen in the afternoon, a child drawing, a playful score. Picture and sound share one clock; every sound lands on the frame of visible contact (the crayon touching down, a hop landing, the eraser starting), within one frame.

**Helpers.** `nz(t, kind, filter, f, Q, a, d, lvl)`: seeded white, pink or brown noise. `pluck(t, f, dur, lvl)`: Karplus-Strong in plain JS. `pad(t, freqs, dur, lvl)`: detuned sines through lowpass 1800 Hz with a slow attack. Levels in dB. No speech.

**Bed.** Kitchen room tone (pink noise lowpass 2500 Hz, -40 dB) and distant birds outside (two short sine chirps 2800→3400 Hz, rarely, -38 dB).

**Music.** A playful cue at 112 BPM in C major: a toy piano (sine plus 4.0 ratio partial, fast decay) on the melody, plucked bass on the roots, a soft shaker (white noise highpass 6000 Hz, 25 ms) on eighths. One instrument joins with each drawing.

**Vocabulary.**

- Crayon drawing: a waxy scratch, white noise bandpass 2200 Hz with grain modulation (random 40 to 80 Hz amplitude flutter), amplitude following stroke speed, for exactly as long as the stroke draws, -22 dB. Scribble fills are faster and rhythmic.
- Crayon touch-down: a tiny tap, -18 dB.
- Hop and landing: a boing (sine 300→600→350 Hz, 0.15 s) and a soft paper pat, -16 dB.
- Eraser: a rubbery squeak and rub, pink noise bandpass 1400 Hz with fast tremolo, -18 dB.
- Sheet sliding: a paper slide, pink noise bandpass 900 Hz, 0.4 s, -18 dB.
- Tally marks: a short stroke tick per mark, at most 12 per second; completion with a two-note toy piano chime.
- Crayon snap: a dry crack (white noise bandpass 3000 Hz, 15 ms) and a sad slide-whistle down; proud redraw: a rising toy-piano arpeggio.
- Climax: the music stops 0.3 s before; then a bold crayon swoosh, a big boing chord, a cymbal-like shimmer (white noise highpass 5000 Hz, 1 s fade), and the full cue returning. It is the single loudest moment.
- Ending: the toy piano plays the opening motif once, slower, over the kitchen tone.

**Density.** 3 to 10 audible events per second; at most 3 foreground sounds at once besides music and bed; repeated ticks at most 12 per second.

**Mix.** Music ducked 4 dB under each foreground hit by scheduled gain; pan by screen position, `(x / 1920 - 0.5) * 1.2`. Loudness and peaks as the technical delivery asks.

## 10. Hero frame

The last frame: the whole drawing on the sheet, sky strip, sun and ground, every figure and item, the closing words or number hand-lettered largest, the crayons scattered on the mint table around the sheet. It must read as this style with no caption.

## 11. Style check

Never ship a stub or "similar for the rest": every figure, item and drawing the brief asks for must exist, drawn. A long file is expected. Inspect frames at 0%, 10%, 25%, 50%, 75% and 95% of the duration, plus three crops at full resolution:

- Is a crayon already drawing in the first frame?
- Do strokes show wax skipping over the grain, with white flecks, and do fills overshoot with gaps?
- Is there no clean vector edge, perfect circle, gradient or typeset text on the drawing?
- Does the drawing boil without brightness flicker, while story motion is continuous every frame?
- Are figures at least one third of frame height in focus, faces at least 50 px, distinct and the same all film?
- Are all items drawn, recognizable, distinct, with no empty slot?
- Are the two house animals drawn in crayon, readable at their size?
- Does every element enter by being drawn and leave by being erased, scribbled over or slid away?
- Is there exactly one coming-alive climax, and does the last frame hold at least 1.2 s with the closing text the largest element?
- Text at 1920x1080: titles 80 px, essential labels 50 px, key numbers 130 px, captions 44 px, never smaller.

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
