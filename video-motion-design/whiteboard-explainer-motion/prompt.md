# Whiteboard Explainer

Build one finished animated film drawn live with dry-erase markers on a glossy porcelain whiteboard: whatever the content brief tells is sketched in real time with authentic marker strokes (two-frequency hand tremor, edge-ink pooling, dry-tip skips, and start/end ink puddles), wiped clean between acts by a felt eraser leaving faint residual streaks over ghostly remnants of earlier lessons, framed by an aluminum tray holding colored markers. The story and technical delivery follow this text.

## The film you must not make

The predictable version: sterile smooth SVG lines on a flat `#FFFFFF` background, digital drop shadows, a generic cartoon hand PNG sliding stiffly across the screen, or dozens of tiny unreadable doodles flashing past at frantic speed. All of that fails. This film looks like a real dry-erase board in a sunlit room: glossy radial sheen, faint wiped ghosts underneath, edge-pooled marker ink, and calm, legible pacing.

## 1. Identity

**Contract.** Live dry-erase marker illustration (`1920x1080` at `30 fps`) on a slightly warm-cool glossy whiteboard (`#F6F7F4` to `#EAECE8`) framed by a brushed aluminum border and bottom marker tray, with faint `10%–12%` erased ghost diagrams beneath the live ink and diagonal ceiling-light reflections.

**Three signatures that any still frame must show:**

1. Authentic dry-erase marker strokes: `30%` translucent base pass, edge-pooled darker perimeter filaments, `1.6 px` normal-direction hand tremor, dry-tip skips, and `2px` ink puddles where the marker lands and lifts.
2. Living whiteboard environment: `10%–12%` faint erased ghost sketches underneath, subtle cleaner-smudge patches, diagonal fluorescent ceiling reflections (`5%` alpha), and a bottom aluminum tray with `4` colored markers (`#1E242B`, `#1B5EC4`, `#D93829`, `#1E8A4C`) and felt eraser.
3. Physical felt-eraser & camera choreography: smooth camera pans across regions of a wide board, plus zigzag felt-eraser wipes that leave `0%–5%` streaky residue bands before new diagrams draw in.

**Three exclusions:** never sterile anti-aliased vector curves without tremor or ink pooling; never start frame `0` on a completely blank white board; never crowd more than `4` detailed marker cards into one camera stop.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the whiteboard frame, never a stretch.

## 3. Material primitives

Pre-render the whiteboard surface gradient, cleaner smudges, aluminum frame + marker tray, and the faint `11%` erased-lesson ghost layer once at init (after fonts resolve!) so `seek(t)` executes in `< 15 ms` per frame.

- **Board & lighting.** Glossy porcelain surface (`#F7F8F5` upper-left to `#E6E9E4` lower-right) with `2` soft diagonal ceiling-lamp reflection bands (`rgba(255,255,255,0.06)`) shifting with `15%` parallax during camera moves, plus `2%` subtle room grain.
- **Dry-erase marker palette.** Charcoal-black `#1E242B` (primary ink), cobalt blue `#1B5EC4` (structure/headers), crimson red `#D93829` (errors/emphasis), emerald green `#1E8A4C` (growth/success), amber `#D98218` (highlights/accents).
- **Marker stroke recipe (`markerPath`).** Resample every polyline every `2.5 px`, displace along the normal using two-frequency seeded noise (`±1.5 px`), draw a `30%`-alpha wide base pass, layer `10`-point wet/dry body segments, add darker edge-pooled perimeter strands, leave occasional `1–2 px` dry-tip skips, and stamp small circular ink puddles at stroke start/end. Reveal progressively by arc length (`0..p`).
- **Felt eraser wipe.** Zigzag `8`-pass sweep (`~140 px` wide) erasing an active layer along its path while leaving `16` faint residual grey streaks (`0%–5%` alpha) where the felt fibers drag.
- **Aluminum frame & marker tray.** `18 px` brushed-silver perimeter bevel (`#C8CDD2` / `#9DA4AB`) with corner rivets and a bottom tray holding horizontal capped/uncapped markers (the active color marker lifts out of the tray or sits at the active stroke tip!).
- **Lettering.** Google Fonts: `Patrick Hand` or `Caveat` (`700`) for bold hand-lettered marker titles, `Inter` (`700`) only if crisp numeric readouts are needed. Minimums at `1920x1080`: headlines `72 px–110 px`, essential labels `44 px–54 px`, key numbers `96 px–140 px`, secondary captions `36 px`. Keep all live ink cleanly inside the aluminum frame (`x = 70..1850`, `y = 65..960`).
- **Finish.** Diagonal glass sheen and subtle corner vignette on every frame.

## 4. Material time

Smooth, brisk-yet-readable live drawing at `30 fps`. Marker strokes draw along their arc length (`0.25s–0.65s` per shape/word) with a slight deceleration at corners; underlines sweep in `0.25s`; felt-eraser zigzags clear a region over `0.6s–0.75s`; camera pans and log-zooms (`0.85x–1.35x`) ease smoothly over `0.5s–0.75s`. Give each beat `2.0s–3.0s` of breathing room, limit simultaneous cards to `2–4` at a time, and keep consecutive identical frames `<= 15%`.

## 5. Piece vocabulary

Turn any noun of the brief into one of these marker-drawn pieces:

- **Board region / Hub.** Double-traced marker box (corners slightly overshooting by `4 px`) or bold cobalt cylinder/node representing the central system.
- **Figure.** See Cast construction.
- **Marker card.** `~340x520` (for character showcases) or `~145x105` (for grid tiles) hand-drawn rectangle with a colored marker header stripe and crisp marker-sketched icon inside.
- **Arrow / Connector.** Single-stroke marker line with `2` hand-drawn barbs at the tip, drawn progressively (`0.3s`) from source to target.
- **Counter.** Bold marker number (`96–130 px`) written cleanly beside a milestone or erased-and-rewritten across `3–4` clear steps.
- **Rotary / Dial weights.** `3` circular marker knobs whose pointer lines turn red while rotating into calibration, turning emerald green once locked.
- **Error / Success mark.** Double-slashed crimson `#D93829` marker `X` for errors; bold emerald `#1E8A4C` checkmark + hand-drawn red/green emphasis ring for fixes.
- **Speech / Callout bubble.** Hand-drawn rounded cloud/bubble with a clipped marker underline.

## 6. Story grammar

### Cast construction

- **Scale & legibility.** Any primary character in focus occupies at least `1/3` of frame height (`>= 360 px` at `1080p`) with a clear face (`>= 50 px`).
- **Character craft.** Sketch recognizable, expressive characters using bold `#1E242B` marker outlines with loose `#1B5EC4`/`#D98218`/`#1E8A4C` marker hatch fills: distinct hairstyles, beards, glasses, collars, and lively eyes/brows that react to events. Keep the protagonist consistent from frame `0` to the final frame.
- **Multi-character rule.** If a story has more than `4` characters, never crowd them all onto one cramped view. Present them calmly in **groups of 2 to 4** across consecutive board regions (`~340 px` wide marker cards each) with `3–4` large, unmistakable marker-sketched task icons per card, gathering the full overview only in the final pull-back where the central figure stays `>= 360 px` tall (`>= 24 px` minimum for any secondary face).
- **Originality.** No real-world logos, protected characters, or brand trademarks.

### A list of N things

Never assume `N`. Adapt the whiteboard layout cleanly without visual clutter:

- **N up to 8:** Sketch items in a calm `2x4` or `4x2` grid (`0.22s` per card) with hanging marker tags.
- **N from 9 to 24:** Group items into `2` to `4` marker-framed columns (`3–4` clear icons per column) across adjacent board regions, holding `>= 1.8s` per view.
- **N above 24:** Showcase top-level roles in calm `4`-card groups first, then pan/draw a clean, well-spaced grid of `~24–32` marker mini-cards (`18 px` gutters, `1` unmistakable icon per tile) paired with a rising marker-drawn growth curve.

### Steps

Each step of the brief is drawn live on a region of the wide whiteboard (`4–5` regions across `15s`). Keep previously drawn anchor titles visible or let the felt eraser intentionally clear an obsolete loop so the final chart or resolution sits cleanly in the center.

### Cause, error and fix

Cause flows along hand-drawn marker arrows (`0.35s`). An error draws a double crimson `X`, followed by a red return arrow to `3` rotating dial knobs, a quick zigzag felt-eraser wipe over the wrong guess, and a bold emerald checkmark.

### Numbers and short words

Use bold hand-lettered marker titles (`72–110 px`), short Portuguese/target-language labels (`44–54 px`), and key numbers (`96–130 px`) with generous whitespace so every word reads instantly over the glossy board.

### Climax and ending

Before the final resolution, pause motion briefly (`0.3s` stillness + music drop) as the felt eraser finishes clearing space or the camera pulls back. On the climax beat, the protagonist sits calmly at full `>= 360 px` scale in the center of the board, flanked symmetrically by crisp active marker mini-cards, while the hero ratio/takeaway draws in bold crimson + charcoal with a hand-drawn underline and `1.2s+` clean hold (with subtle room-light drift).

### Pacing by duration

Frame `0` (`t = 0`) MUST already be an active, legible hook — open immediately with the protagonist's silhouette and opening marker title already being sketched on the glossy board (never an empty white board). Aim for `14.5s–16s` across `4–5` unhurried beats (`2.5s–3.2s` each). Build a `BEATS` table (`id, t0, t1, region, title, sounds`) before coding so marker strokes, eraser wipes, and audio cues share one exact clock.

## 7. Transitions

1. **Board camera pan & zoom (`0.55s–0.7s`).** Smooth `easeInOut` camera travel across the wide whiteboard (`15%` parallax on ceiling-lamp reflections) to the next diagram region.
2. **Zigzag felt-eraser wipe (`0.6s–0.75s`).** `8` rapid diagonal passes clearing an old zone and leaving faint residual streaks before the new diagram draws in.
3. **Marker cap-pop & underline (`0.3s`).** Active marker color changes in the tray with a bold underline sweeping across the new section header.

Never use abrupt hard cuts or generic crossfades.

## 8. Camera

`10`-keyframe (or `5`-region) board camera using smooth log-scale zoom (`0.85x` wide overview to `1.25x` focus) and eased pan, keeping marker stroke thickness visually balanced and all essential text well inside the aluminum frame.

## 9. Sound

Synthesized `100%` via Web Audio API (`48000 Hz` stereo, `-19` to `-12` LUFS integrated, true peaks `<= -1 dBFS`, last stage `<= -4 dBFS`, no hard clipper, no silence `> 1.5s`). Picture and sound share the exact `BEATS` clock.

**Bed.** Quiet classroom/studio room tone (brown noise lowpass `300 Hz`, `-36 dB`) + faint air hum.

**Vocabulary & levels.**
- Marker cap pop (opening/closing): plastic snap (`2.2 kHz` bandpass `15 ms` + `190 Hz` pop, `-15 dB`).
- Marker felt-tip draw: crisp squeak-tap on touchdown (`1.5 kHz` bandpass, `22 ms`, `-18 dB`) + continuous bandpass felt-on-porcelain drag (`2.6–3.2 kHz`, `Q = 2.2`, `-22 dB`) lasting the exact duration of the stroke.
- Lettering: one short marker flick per word (`<= 10` flicks/s).
- Felt eraser wipe: `8` alternating-pan brush sweeps (`700 Hz` pink bandpass, `80 ms` each, `-16 dB`).
- Knob calibration: dry plastic ratchet clicks (`1.2 kHz`, `>= 90 ms` apart, `-18 dB`).
- Error `X`: two fast permanent-marker slashes + low `105 Hz` thud (`-13 dB`).
- Climax (`0.3s` silence drop before hit): bold marker underline + warm `4`-voice acoustic/marimba-like chord (`C4-E4-G4-C5`, `1.1 s`, `-13 dB`, `0.3` reverb) + low `75 Hz` thud landing on the final reveal.

**Density & Mix.** Keep `3` to `10` audible events/s, max `3` simultaneous foreground voices, and stereo pan `(x / 1920 - 0.5) * 1.1`.

## 10. Hero frame

The final frame (`t = duration - 0.5s`): full aluminum-framed glossy whiteboard with bottom marker tray, faint erased ghosts underneath, calm centered marker protagonist (`>= 360 px` tall) flanked symmetrically by active marker mini-cards, bold crimson & charcoal hero ratio/takeaway underlined, house animals sketched in the lower-left and upper-right board corners, held `>= 1.2s`.

## 11. Style check

Before finishing, inspect rendered frames at `0%`, `10%`, `25%`, `50%`, `75%`, and `95%` of duration:
- [ ] Frame `0` is already active and readable (protagonist + opening stroke visible immediately).
- [ ] Marker strokes show real hand tremor, edge-ink pooling, and wet/dry texture (not sterile digital vectors).
- [ ] Glossy ceiling reflections, `10%–12%` erased ghosts, aluminum frame, and marker tray are visible.
- [ ] Primary characters `>= 1/3` frame height (`>= 360 px`), showcased `2–4` per view with `3–4` clear marker task icons per card.
- [ ] Calm, breathable pacing (`14.5–16s`, `<= 15%` identical frames, `>= 1.2s` final hold).
- [ ] `renderAudio()` outputs `48000 Hz` stereo within `-19` to `-12` LUFS, peaks `<= -4 dBFS`, zero silence `> 1.5s`.

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
