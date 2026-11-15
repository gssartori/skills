# Lightbox Test

Build one finished animated film seen straight down on a hand animator's lightbox: whatever the content brief tells is drawn on punched paper sheets, first as blue construction roughs, then as confident graphite cleanup, with red timing notes, light glowing up through the stacked sheets, and moments where the drawings play back on twos as a pencil test. The story and technical delivery follow this text.

## The film you must not make

The predictable version: a vector character tweening smoothly on white with a "sketch" filter on top, pencils that never touch the paper, red and green digital onion-skin tints, a hand-drawn font pretending to be handwriting, a piano loop. All of that fails. This film shows the real craft of hand animation: blue construction under a graphite line, drawings numbered on twos, spacing that matches the timing chart, and light passing through paper.

## 1. Identity

**Contract.** Top-down at 1:1 on an animator's desk: a backlit aluminium animation disc set into sea-green linoleum, punched paper on a steel peg bar, pencils and an eraser beside it, a ruled exposure sheet to the right. The paper glows from below, so drawings on the sheets underneath show through as lighter lines.

**Three signatures that any still frame must show:**

1. Blue construction lines (egg shapes, center lines, a curved line of action) under one confident graphite line with tapered ends.
2. Onion skin made of light: earlier sheets show through the top sheet at decreasing strength.
3. A real pencil, drawn top-down, lying on its stroke with its point leading as each line appears.

**Three exclusions:** never smooth tweened motion of the drawn figures (they change drawing on twos); never a pencil filter over finished vector art; never color fills inside the drawings.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the desk, never a stretch.

## 3. Material primitives

Render the desk, the disc, the pencils and the paper fiber once into offscreen canvases. Precompute every stroke at load as a polyline with per-point pressure and a start time; each frame draws only the part revealed by t.

- **Desk.** Sea-green linoleum `#3F6A5E` with a seeded mottle `#46736A` (two octaves, 4% amplitude) and a beech front edge `#A7845C` along the bottom 60 px, with a seeded wood grain.
- **Disc.** Brushed aluminium `#B8BCC0`, 860 px across, centered a little left of frame center, in a recessed steel ring with engraved degree marks `#7E8388` every 5 degrees; a frosted window `#FFF8E8` under the paper area.
- **Paper.** Animation paper `#F7F3E7`, about 780 x 590 px, lit from below: `#FFFAEE` at the center fading to `#EFE7D3` toward the edges (the only gradient in the film besides the lightbox glow itself), with fine seeded fiber (short light strokes at 4% alpha). The top edge is punched with three peg holes (a round hole between two slots) seated on a steel peg bar.
- **Strokes.** Every line is a pressure-varying ribbon: width follows a curve heavier in the middle and tapering at both ends; jitter of ±0.6 px at 40 px intervals; slight overshoot past corners. Blue pencil `#3F86D6` at 1.8 to 2.4 px, loose and searching, 2 to 4 overlapping passes on curves. Graphite `#2C2C30` at 2.5 to 3.5 px, one confident closed pass. Red pencil `#D64B3C` at 2 px for paths of action (dotted), timing charts and notes.
- **Graphite grain.** Graphite lines are drawn through a seeded paper-tooth mask (a high-frequency noise tile, 256 px) so they break slightly on the paper grain, never perfectly solid.
- **Onion skin.** When a new sheet drops onto the pegs, the sheets below show through at 55%, 32%, 18% and 10% of their line strength (top sheet 100%); the paper's own glow stays constant. Never tinted red or green.
- **Pencils.** Each pencil drawn top-down in code: a hexagonal body 18 px wide and 380 px long with faces shaded so it reads as a solid, a sharpened cone of bare wood `#E3C49A`, a colored point, and a soft shadow 10 px down-right. Blue lacquer `#2F6FC0` (with an eraser and metal ferrule), red `#C23B30`, natural cedar `#D8B48A` for graphite. A kneaded eraser `#9C9C98` and a pink eraser `#E7A4A0` lie on the desk.
- **Exposure sheet.** A narrow ruled pad, `#F7F3E7` with sage `#BFD3CB` rules every 30 px, to the right of the disc. It fills in pencil as the work goes.
- **Masking-tape slate.** A strip of tape `#E9D27A` on the disc ring at the top left of the paper, with the scene label in pencil.
- **Lettering.** Google Fonts: `Kalam` (700 and 400) for everything pencilled on paper and tape; `Literata` (600 italic) for the title on the desk; `Courier Prime` (700) for the playback frame counter on a dark chip. Minimums at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px. Pencil notes that are texture (frame numbers, initials) may be smaller, but anything the viewer must read is at least 42 px.
- **Finish.** The lightbox glow under the paper, a faint warm vignette at 10%, and nothing else. No grain on the desk image beyond the baked mottle.

## 4. Material time

The camera, pencils and light move smoothly at 30 fps. The drawings themselves always change on twos: each drawing is held for 2 frames of a 24 fps count, so drawn motion advances at 12 drawings per second (in a 30 fps render, map time to the nearest drawing on a 12 per second grid). Lines draw on along their paths at about 2400 px per second, with the working pencil's point on the leading end. Sheets drop onto the pegs from 30 px above over 0.2 s with a 2 px settle.

## 5. Piece vocabulary

Turn any noun of the brief into one of these. Everything is a drawing on paper, drawn on screen by a pencil.

- **Figure.** See Cast construction. Appears as blue construction first, then graphite cleanup.
- **Central object.** A larger drawing with clear construction (boxes, ellipses, perspective lines in blue) and one part that changes when the story changes, redrawn on the next sheet: a lid opening, a needle moving, a door swinging. The change is visible as onion skin: old position faint, new position firm.
- **Item.** A small thumbnail drawing inside a ruled box (a thumbnail frame, 120 to 200 px) with a quick blue rough and a graphite cleanup of the item's most recognizable silhouette. Any noun becomes an item by its silhouette plus one prop.
- **Arrow or link.** A red pencil path of action: a dotted arc drawn on, with a small arrowhead at the end and tick marks along it like a spacing chart.
- **Label.** Pencilled in `Kalam` 700, graphite, with a short underline; or on a scrap of masking tape stuck beside what it names.
- **Counter.** Numbers written in graphite and then struck through and rewritten as they rise (3 to 4 milestones), each new number heavier, the last circled twice in red.
- **Error mark.** A red pencil cross through the wrong drawing, then the kneaded eraser rubs it (a 0.4 s back-and-forth with grey crumbs), and the corrected drawing goes in. **Success mark:** a red check and a circle around the drawing.
- **Emphasis.** A red pencil ring drawn around the key drawing in one stroke, at most once per scene.

## 6. Story grammar

### Cast construction

The style does not know who is in the story. It says how anyone the brief describes becomes a drawn character.

- **Construction.** Each character is drawn as a hand animator would: in blue, an egg for the head with a center line and eye line, a bean for the torso, a curved line of action through the body, stick limbs with ovals at joints; then in graphite, one confident closed contour, simple features (dot or oval eyes, a short line mouth, brows), hair and clothes as clean shapes with one or two folds. No fills; shading only as a few graphite hatching strokes in shadows.
- **Proportions.** Adults about 5.5 heads tall, children about 4; the main character roughly 0.35 of the paper height when standing.
- **Scale.** In main scenes the character in focus is at least one third of frame height with a face of at least 50 px. With more than 4 characters, show 2 to 4 at a time as the camera passes, and gather everyone only at the reunion moment, where no face is under 24 px; whatever does not fit becomes a group with one large representative.
- **What the brief says about a person** becomes line: a beard as a tapered graphite contour with a few hair strokes inside, glasses as two clean rings, age and job as posture and one prop. Every character keeps the same marks on every sheet.
- **Several characters:** each one identifiable by silhouette and one strong drawn attribute (hair shape, a prop, a garment), never by a caption alone.
- **Acting on twos.** Key poses are circled in red on their sheets; inbetweens bunch near the keys (slow in and out) and open out in fast moves, and the timing chart on the sheet's right margin shows the same spacing with one tick per drawing. Squash and stretch keep volume within ±5%.
- **Originality.** No existing cartoon character; no face on objects unless the brief asks for a character; no colored fills.

### A list of N things

Never assume N. Items become thumbnail drawings.

- **N up to 8:** a new sheet drops onto the pegs, and the blue pencil roughs N thumbnail boxes in a row or a 2 by 4 grid, then fills each with a quick drawing, every 0.15 to 0.3 s, with a pencil note naming it.
- **N from 9 to 30:** groups become separate sheets. Each sheet holds one group as a thumbnail grid (2 or 3 columns), and the sheets are laid side by side on the desk around the disc, or stacked on the pegs so the earlier groups glow through as onion skin.
- **N above 30:** the first group is drawn on the paper; the rest appear as a long strip of thumbnail frames pencilled across extra sheets taped along the desk, the camera tracking along them, with the counter giving the total.
- Every item is drawn the same way: box, blue rough, graphite cleanup. Two thumbnails that could be swapped without anyone noticing have failed.

### Steps

Each step of the brief is a **sheet** (or a pair of sheets) dropped onto the pegs, drawn in order: rough, path of action, cleanup. The exposure sheet on the right records each step as a row with its action note in pencil, so the steps read as a list. Something always continues from one step to the next: the earlier sheet glows through, the path of action continues, the same character carries on.

### Cause, error and fix

Cause is a red path of action that travels from one drawing to the next. If the brief has an obstacle or a mistake, use the error mark: cross, eraser, redraw, then the success mark.

### Numbers and short words

A number or short word the brief puts on screen is drawn large on the paper: blue block letters first (with construction lines and a baseline), then a heavy graphite outline and a few hatching strokes inside, at least 96 px tall (140 px or more when it is the key image).

### Climax and ending

Exactly one moment is the biggest in the film: the brief's key image as a **pencil test playback**. Before it, 0.3 s of stillness: the pencil lifts off the paper and the music stops. At the moment, the lightbox flattens to a top-lit look (paper `#F4F1E8`, only the top sheet visible, as if each drawing were shot alone), cream corner guides appear, a frame counter on a dark chip appears at the paper's top right, and the key drawings play at 12 per second with the key image landing on its circled key frame. The last image returns to the lightbox: the brief's last words or number drawn largest on the paper, graphite over blue, with the red ring around it and the earlier sheets glowing through, held at least 1.2 s with only the pencil resting and the light breathing ±2%.

### Pacing by duration

Hook within the first 1.5 s: a pencil is already drawing on the paper. Something changes every 1 to 2 s. About 10 s: 3 sheets or places. 13 to 16 s: 4. Before drawing, write a beat table: one row per beat with start and end time, the exact on-screen text, the physical cause that moves us to the next beat, and the main sounds. Picture and sound both read times from that table.

## 7. Transitions

Every change of place is a physical event of the desk, 0.3 to 0.8 s long, and the swap happens while the frame is covered.

1. **Sheet drop.** A new sheet drops onto the pegs and covers the drawing; the old drawing stays as onion skin underneath.
2. **Flip.** The animator's fingers are never shown, but the stack of sheets flips from the bottom corner like a flip book (each sheet lifts and drops in 2 frames), playing the drawings in sequence.
3. **Disc turn.** The disc turns up to ±20 degrees on `easeInOutSine`, carrying the peg bar, paper and lines with it, to bring a new drawing angle under the pencil.
4. **Desk track.** The camera glides across the desk to a neighbouring sheet, the exposure sheet or a taped strip of thumbnails.

Never use a dissolve, a generic wipe or a hard cut to change idea.

## 8. Camera

Top-down and still for most of the film, the disc filling the middle. At most 5 moves in 15 s, eased in and out; zoom in log scale between 1.0 and 1.5, with one push-in onto the paper for the playback and one pull-back at the end that shows the whole desk. A slow drift of 5 px per second keeps it alive. Line widths are in paper space and scale with the zoom; essential text is counter-scaled to stay readable.

## 9. Sound

The sound of a quiet animation desk, close and dry. Picture and sound share one clock; every sound lands on the frame of visible contact (pencil down, sheet seated on the pegs, playback frame change), within one frame.

**Helpers.** `nz(t, kind, filter, f, Q, a, d, lvl)`: seeded white, pink or brown noise. `tick(t, f, lvl)`: a short filtered click. `pluck(t, f, dur, lvl)`: Karplus-Strong in plain JS. Levels in dB. No speech.

**Bed.** The lightbox hum: a 100 Hz sine with a 200 Hz partial at -12 dB relative, very low (-34 dB overall), plus faint room tone (pink noise lowpass 3000 Hz, -38 dB).

**Pencil.** A pencil stroke is continuous noise for exactly as long as the line draws: white noise through bandpass 2500 to 4500 Hz (higher for graphite, lower for the waxy blue and red), amplitude following the stroke's pressure curve and speed, with 30 to 60 tiny grain ticks per second. Each pencil has its own color: blue soft and waxy (bandpass 2200 Hz, Q 1.5), graphite crisp (3800 Hz, Q 2), red slightly sticky (2800 Hz with 8 Hz amplitude flutter). Pencil down: a small tap at 1800 Hz, 8 ms. Pencil laid on the desk: a wooden clatter of 3 ticks.

**Paper.** Sheet drop on pegs: a soft paper slap (pink noise bandpass 1200 Hz, 60 ms) plus a small metallic click at 3200 Hz for the peg bar. Flip: a fast riffle of 6 to 12 paper ticks. Eraser: a rubbery scrub, pink noise bandpass 900 Hz chopped at 9 Hz, plus crumb ticks.

**Music.** A light jazz-trio sketch at 96 BPM, entering after the first sheet: brushed snare (pink noise, 25 ms swishes on 8ths), upright pizzicato bass (pluck lowpass 900 Hz) on beats, and a few muted piano chords (sines with fast decay, lowpass 1800 Hz) on the off-beats. It drops out entirely 0.3 s before the playback.

**Playback.** Each drawing change during the playback is a projector-style tick (white noise highpass 4000 Hz, 6 ms) at 12 per second under a gentle projector whir (brown noise lowpass 400 Hz with 24 Hz amplitude flutter, -24 dB); on the key frame, a warm full chord on piano and bass with a cymbal swell, the single loudest moment.

**Density.** 4 to 12 audible events per second; at most 3 foreground sounds at once besides music and bed; repeated ticks at most 12 per second; the pencil scratch never runs under two other pencils at once.

**Mix.** Music ducked 4 dB under each pencil stroke by scheduled gain; pan by screen position, `(x / 1920 - 0.5) * 1.2`. Loudness and peaks as the technical delivery asks.

## 10. Hero frame

The last frame: the lightbox from above, the paper glowing, the brief's closing words or number drawn largest in graphite over blue construction, a red ring around it, earlier sheets glowing through as onion skin, the exposure sheet filled, the pencils resting. It must read as this style with no caption.

## 11. Style check

Never ship a stub or "similar for the rest": every character, item and step the brief asks for must exist, drawn on paper. A long file is expected. Inspect frames at 0%, 10%, 25%, 50%, 75% and 95% of the duration:

- Is a pencil already drawing in the first frame?
- Does blue construction sit under every graphite line, and do graphite lines taper and break on the paper grain?
- Does onion skin read as light through paper, never as colored tints?
- Do drawn characters change on twos, with spacing matching the timing chart, while camera and pencils move smoothly?
- Does each character keep its marks on every sheet, and is each one distinct by silhouette?
- Are all items drawn, separate and different, with no empty thumbnail box left behind?
- Are the two house animals drawn in the same pencil craft, readable at their size?
- Is there exactly one playback climax, and does the last frame hold at least 1.2 s with the closing text the largest element?
- Text at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px, never smaller for anything the viewer must read.

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
