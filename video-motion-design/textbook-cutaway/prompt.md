# Textbook Cutaway

Build one finished animated film as a science textbook plate brought to life: whatever the content brief tells becomes a block diagram cut open along its axis, built layer by layer with the patterned fills of a technical section, crossed by channels through which the story flows, and every part named by a leader line ending in a red dot. The story and technical delivery follow this text.

## The film you must not make

The predictable version: an infographic of rounded boxes with icons, glossy 3D blocks with drop shadows, labels floating with no line to what they name, a brown triangle with orange circles flying out of it, a ticking corporate synth bed. All of that fails. This film looks like the best plate in a printed reference book: real construction, exact leaders, calm motion that explains.

## 1. Identity

**Contract.** Warm textbook paper, thin ink linework and flat fills carrying section patterns (crosses, dashes, dots, stipple, hatching), drawn as a block diagram whose front face is a cut through the subject. Not to scale, and it says so in the key.

**Three signatures that any still frame must show:**

1. A solid block in oblique view (front face cut open, top face receding up and right, a darker side strip) holding the subject.
2. Patterned section fills that tell materials apart, with a key of swatches in a corner.
3. Leader lines, 1.5 px ink, each ending in a 7 px red dot placed exactly on the part it names.

**Three exclusions:** never a drop shadow or glossy highlight; never a gradient except inside the one hot flowing substance; never a label without a leader.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the plate, never a stretch.

## 3. Material primitives

Render the paper, the patterns and every static part of the block once into offscreen canvases; per frame, draw only what is revealed or moving.

- **Paper.** `#F1ECE2` with faint seeded fiber (2% alpha) and a thin printed margin rule 40 px in from the edges.
- **Ink.** `#2B2622`. Outlines 2.5 px on the block and main parts, 1.5 px for interior divisions and leaders, round joins. Lines are printed: perfectly even, no wobble.
- **Section patterns.** Built as small repeating tiles (24 to 40 px) and used as fills: crosses for the oldest or deepest material (`#B9AE9C`), horizontal dashes for bedded or stacked material (`#CFC3AE`), sparse dots for porous material (`#7A5A4A`), dense stipple for fine material (`#CDBB95`), 45 degree hatching for metal or structure (`#A9A49B`), wavy lines for liquids (`#9FB8C2`). Each material of the story's subject gets one pattern and keeps it all film.
- **Hot flow.** The one substance that carries the story's cause (energy, work, a message, a product) is drawn as a bright flow: `#E8532B` at its edges to a hot core `#FFB13B`, with a darker crust `#9E3A22` along its borders. This is the only gradient in the film.
- **Bubbles and particles.** Outlined circles in `#FFE2A8` (1.5 px) that ride the flow and grow as it rises or advances (radius 2 px at the source to 14 px near the outlet).
- **Block.** Front face as the cut section; top face receding 80 px right and 50 px up in a surface color (`#C9C29A`); right side face a darker strip (base color minus 18% lightness). The block reads as solid from the first frame.
- **Lettering.** Google Fonts: `IBM Plex Mono` (500) for the kicker, tracked 0.14 em, red `#C2412A`; `IBM Plex Serif` (600) for titles; `IBM Plex Sans` (500) for labels, captions and the key. Minimums at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px, captions 40 px. Labels wrap to two lines within 260 px and sit in two columns at the left and right margins.
- **Palette.** Paper, ink, the pattern colors above, hot flow colors, column greys `#C7C0B6`, `#A39C93`, `#6F6862`, accent red `#C2412A` for dots and the kicker, secondary text `#6E655C`. Nothing else.
- **Finish.** None beyond the paper fiber. The crispness of print is the finish.

## 4. Material time

Smooth and calm at 30 fps. Ink lines draw on along their length (0.25 s for a leader, 0.4 to 0.8 s for a contour); fills appear by wiping from one side in the direction of the material (layers drape down slopes, liquids fill from below, stacks settle from above with a 6 px drop). The hot flow advances on `cubic-bezier(0.45, 0, 0.2, 1)`. Nothing bounces. At most four labels arrive in any one second.

## 5. Piece vocabulary

Turn any noun of the brief into one of these. Every piece is drawn in section, with patterns and ink.

- **The block** (the brief's world: a company, a city, a body, a machine, a process). Its cut face shows the subject's inside as layers, chambers and channels. One part changes when the story changes: a chamber fills, a valve opens, a channel lights with hot flow.
- **Figure.** See Cast construction.
- **Chamber.** An ellipse or rounded room inside the block where something collects; it fills with the flow from below.
- **Channel.** A conduit (24 to 40 px wide) cut through the layers, through which the hot flow travels; branches (dikes) cut diagonally across layers, side branches (sills) run between them.
- **Item.** A small labeled cell in the section: a compartment, a capsule, a crystal, a pocket, each with its pattern and a pictogram drawn in ink inside it (the item's most recognizable silhouette, 1.5 px line, no fill beyond the pattern).
- **Label.** Leader from the exact part to the margin column, drawn over 0.25 s; the text then fades in over 0.3 s, rising 6 px. Labels never overlap each other, the flow or a caption.
- **Caption.** One line at the bottom on a baseline 80 px above the frame edge, crossfading with a 10 px rise; at least 1.6 s on screen.
- **Counter.** A numbered scale bar or gauge drawn at the block's side, its needle or fill level rising by an ease-out power curve; the number in `IBM Plex Mono`, at least 96 px when it is the key number.
- **Error mark.** A crack in the section (a jagged ink line with a red dot labeled), the flow stalling behind it. **Success mark:** the crack seals with a new layer and the flow continues.
- **Emphasis.** A red dashed ellipse drawn around the key part over 0.4 s, at most once per scene.
- **Key.** Bottom right: one 28 px swatch per pattern with its name, plus "Not to scale" (translated into the brief's language).

## 6. Story grammar

### Cast construction

The style does not know who is in the story. It says how anyone the brief describes is drawn in a textbook plate.

- **Figures as scale figures.** People are drawn like the human figures textbooks place for scale: clean ink contours with a single flat tone fill (`#D8CDB8` for skin areas, palette pattern colors for clothes), simple features (dot eyes, a short brow line, a small mouth), standing on the top face of the block or inside a chamber of the cutaway.
- **Scale.** In main scenes the figure in focus is at least one third of frame height with a face of at least 50 px. With more than 4 figures, show 2 to 4 at a time as the camera passes, and gather everyone only at the reunion moment, where no face is under 24 px; whatever does not fit becomes a group with one large representative.
- **What the brief says about a person** becomes line and pattern: a beard as a hatched area along the jaw, glasses as two thin rings, a job as one prop held or a pattern on the clothes. Each figure gets its own label with a leader, and keeps the same marks all film.
- **Several figures:** each distinct by silhouette and by one pattern on the clothes, never by a caption alone.
- **Originality.** No real person, mascot, logo or brand.

### A list of N things

Never assume N. Items become cells in the section.

- **N up to 8:** each item is a cell in its own layer or chamber, filled in turn every 0.2 to 0.3 s, each with a label in the margin columns.
- **N from 9 to 30:** items are grouped. Each group is one stratum of the block, divided into cells (2 to 6 per row), each cell with its pictogram; one label names the stratum, and a numbered key lists the cells.
- **N above 30:** the first group is drawn in detail; the rest fill the deeper strata as a dense cellular pattern (each cell still with a tiny pictogram), and the counter gives the total. Only the first cells get leaders.
- Every cell enters, fills and settles the same way. Two cells that could be swapped without anyone noticing have failed.

### Steps

Each step of the brief is one **construction or flow stage** of the plate: a layer is added, a chamber fills, a channel opens, the flow rises, an outlet releases. The plate keeps everything already built, so the steps accumulate like the plate in a book. Group two steps per stage when they share one.

### Cause, error and fix

Cause is always the hot flow travelling through channels, bubbles growing as it advances. If the brief has an obstacle or a mistake, use the error mark: the crack, the stall, then the seal and the flow resuming.

### Numbers and short words

A number or short word the brief puts on screen is set in `IBM Plex Serif` 600, at least 96 px (140 px or more when it is the key image), printed in ink on the paper or cut into the top face of the block as an engraved inscription.

### Climax and ending

Exactly one moment is the biggest in the film: the brief's key image, shown as the release of the flow. Before it, 0.3 s of stillness: the flow holds just below the outlet and the music stops. At the moment, the flow breaks out of the top of the block as a column: a dense narrow jet, then billowing lobes that widen as they rise (each lobe slowing from 600 to 80 px per second, three flat grey tones lit from the upper left, only the outer silhouette outlined), spreading into an umbrella that carries the key image. The last image is the finished plate: the brief's last words or number largest in frame, every label and the key in place, held at least 1.2 s with only the column billowing slowly.

### Pacing by duration

Hook within the first 1.5 s: the block is already drawing on. Something changes every 1 to 2 s. About 10 s: 3 stages. 13 to 16 s: 4. Before drawing, write a beat table: one row per beat with start and end time, the exact on-screen text, the physical cause that moves us to the next beat, and the main sounds. Picture and sound both read times from that table.

## 7. Transitions

Every change of place is an event of the plate, 0.4 to 0.8 s long.

1. **Cut deeper.** The camera pushes into a chamber of the block and the chamber's own cutaway draws on, filling the frame.
2. **Turn the plate.** The block rotates its oblique view 20 to 30 degrees, revealing a new cut face.
3. **Next figure.** A figure number and a thin rule draw on, and the plate slides up like the next figure on a printed page, the old plate leaving at the top.
4. **Flow carries.** The camera follows the hot flow along a channel to the next part.

Never use a dissolve, a generic wipe or a hard cut to change idea.

## 8. Camera

Mostly still, the block centered. At most 5 moves in 15 s, eased; zoom in log scale between 0.9 and 1.6, with one pull-back at the end that shows the whole plate. Line widths stay constant on screen; labels are counter-scaled to stay at their minimum size.

## 9. Sound

The sound of a quiet study with a slow documentary score. Picture and sound share one clock; every sound lands on the frame of visible contact (a layer settling, a leader dot landing, the flow reaching a chamber), within one frame.

**Helpers.** `nz(t, kind, filter, f, Q, a, d, lvl)`: seeded white, pink or brown noise. `pluck(t, f, dur, lvl)`: Karplus-Strong in plain JS. `pad(t, freqs, dur, lvl)`: detuned sines through lowpass 1500 Hz with a slow attack. Levels in dB. No speech.

**Bed.** Room tone (pink noise lowpass 2500 Hz, -38 dB) and a faint pen-on-paper texture when lines draw.

**Music.** A slow documentary cue at 80 BPM: a warm pad on D minor and F major, a celesta-like bell (sine plus 3.0 and 4.2 ratio partials, fast decay) on quarter notes, and a low bowed note (saw through lowpass 600 Hz, slow attack) that rises a step with each stage.

**Vocabulary.**

- Ink line drawing: soft pen scratch, white noise bandpass 3500 Hz, amplitude following the drawing speed, for exactly as long as the line draws, -24 dB.
- Layer settling: a soft paper-and-sand pat, pink noise lowpass 900 Hz, 70 ms, -16 dB, pitch rising slightly with each layer.
- Leader dot landing: a small bell tick at 2400 Hz, 30 ms, -14 dB.
- Chamber filling: a low liquid rumble, brown noise lowpass 300 Hz with slow 3 Hz modulation, -16 dB.
- Flow rising: a rising gurgle, bubbles as short pitched pops (sine 400→900 Hz, 25 ms) whose pitch falls as the bubbles grow, at most 12 per second.
- Crack: a dry stone snap, white noise bandpass 1800 Hz, 40 ms, plus a low thud. Seal: a soft settle and a rising two-note bell.
- Counter: a fine mechanical tick per step at 1600 Hz, at most 12 per second; the lock is a bell chord.
- Climax: the music stops 0.3 s before; then a deep rumble swelling for 0.4 s (sine 50→35 Hz plus brown noise lowpass 200 Hz), a bright break (white noise highpass 2000 Hz, 0.2 s), and a long airy roar of the column (pink noise bandpass sweeping 300→1200 Hz, 2 s, slowly fading), with the full pad chord entering under it. It is the single loudest moment.
- Ending: the bell plays the opening motif once, slower, over the fading roar.

**Density.** 3 to 10 audible events per second; at most 3 foreground sounds at once besides music and bed; repeated ticks at most 12 per second.

**Mix.** Music ducked 4 dB under each foreground hit by scheduled gain; pan by screen position, `(x / 1920 - 0.5) * 1.2`. Loudness and peaks as the technical delivery asks.

## 10. Hero frame

The last frame: the full block in cutaway with every layer, chamber and channel, the column carrying the brief's closing words or number largest in frame, all labels on their leaders in the margin columns, the key in the corner. It must read as this style with no caption.

## 11. Style check

Never ship a stub or "similar for the rest": every figure, item and stage the brief asks for must exist, drawn. A long file is expected. Inspect frames at 0%, 10%, 25%, 50%, 75% and 95% of the duration:

- Is the block already drawing on in the first frame?
- Does every material have its own section pattern, with a key that matches?
- Does every leader dot sit exactly on the part it names, with no label overlapping another label, the flow or a caption?
- Is the hot flow the only gradient, and do bubbles grow as it advances?
- Are figures at least one third of frame height in main scenes, distinct, and the same all film?
- Are all items drawn as cells with pictograms, separate and different, with no empty cell?
- Are the two house animals drawn as textbook scale figures with leaders, readable at their size?
- Is there exactly one release climax, and does the last frame hold at least 1.2 s with the closing text the largest element?
- Text at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px, captions 40 px, never smaller.

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
