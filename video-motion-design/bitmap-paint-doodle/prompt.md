# Bitmap Paint Doodle

Build one finished animated film inside an early-2000s desktop bitmap paint program: whatever the content brief tells is painted live onto one wide `Uint32Array` pixel document — aliased pencil strokes, wonky double-drawn rectangles, instant bucket flood fills, airbrush speckles, `Ctrl+V` opaque paste stacks, and dashed text-tool boxes — while the horizontal scrollbar thumb pans the camera smoothly across beats, upscaled `3x` nearest-neighbor from `640x360` to `1920x1080` at `30 fps`. The story and technical delivery follow this text.

## The film you must not make

The predictable version: a clean modern vector whiteboard with smooth Bezier curves, anti-aliased fonts, soft drop shadows, or dozens of tiny unreadable cards flashing past at frantic speed. All of that fails. This film looks like someone genuinely painting an explanation in a classic `#c0c0c0` bitmap paint window: crisp `1px` stair-stepped pixels, tactile mouse and keyboard choreography, and calm, breathable pacing so the viewer can enjoy every stroke.

## 1. Identity

**Contract.** Classic `#c0c0c0` beveled desktop paint-program UI (`640x360` logical buffer, `3x` nearest-neighbor to `1920x1080`) framing a `540px`-wide viewport into a wide scrollable `Uint32Array` bitmap canvas (`~2400x230`). Every stroke, fill, and character is plotted as raw `1px` aliased pixels.

**Three signatures that any still frame must show:**

1. Authentic `#c0c0c0` paint chrome: `#000080 -> #1084d0` gradient title bar, `2x8` beveled tool palette (active tool in a pressed dithered cell), `28`-color bottom swatch bar, and a 3-pane status bar showing live cursor `x,y` coordinates.
2. Live `PixelDoc` bitmap craft: mouse-jittered hand strokes (`rng.gauss()`), double-drawn rectangles, instant scanline `flood()` fills, radial airbrush speckles, and dashed marching-ant text boxes with `#000080` resize handles.
3. Scrollbar camera pans: a working horizontal scrollbar directly beneath the `540px` canvas well whose thumb width and position track the exact `scroll` offset between beats.

**Three exclusions:** never smooth anti-aliased strokes or blurry shadows; never start frame `0` on an empty white canvas; never crowd more than `4` detailed cards or clip text past the `540px` viewport edges.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the paint viewport, never a stretch.

## 3. Material primitives

Pre-allocate the `640x360` offscreen buffer, the `PixelDoc` `Uint32Array`, and the `rasterText` scratch canvas (or cache static text masks) once at init so `seek(t)` executes in `< 12 ms` per frame.

- **Chrome palette.** `#c0c0c0` face, `#ffffff` highlight, `#dfdfdf` light bevel, `#808080` shadow, `#000000` black, `#000080` to `#1084d0` title bar gradient.
- **28-color swatch palette.** Two rows of `14` sunken `16x16` wells (`#000000`, `#808080`, `#800000`, `#808000`, `#008000`, `#008080`, `#000080`, `#800080`, `#ffff00`, `#00ff00`, `#00ffff`, `#0000ff`, `#ff00ff`, `#ff8040`, `#ffffff`, etc.) plus overlapping active foreground/background squares on the left.
- **PixelDoc primitives.**
  - `line()` / `stamp()`: Bresenham `1px` lines and circular pixel stamps (`size = 1..5`).
  - `hand()`: densified polyline with seeded `rng.gauss() * jit` (`jit = 0.6..1.4`) drawn progressively from `0..p`.
  - `rectO()` / `ellipse()`: crisp axis-aligned outlines and rubber-band corner-dragged ellipses.
  - `flood()`: true scanline flood fill executing instantaneously (`dur = 0.001`) when clicked.
  - `spray()`: seeded radial airbrush dots (`r = 10..20px`).
- **Lettering.** Google Fonts: `Inter` (`400`/`700` at `9px` = `27px` at `1080p`) for menus, title bar, and status bar; `Patrick Hand` (`400`) thresholded at `alpha > 110–120` via `rasterText()` for all painted canvas text. Minimums in `PixelDoc` coordinates (`3x` at `1080p`): headlines `28px–44px` (`84px–132px` at `1080p`), labels `18px–22px` (`54px–66px`), key numbers `36px–52px` (`108px–156px`). Always ensure painted text fits comfortably inside `x_local = 16..524`, `y_local = 14..216` of each scroll stop so nothing clips against the viewport or dashed text box.
- **Tool cursors.** Pixel-art `pencil`, `crosshair`, `bucket`, `eraser`, and `I-beam` cursors tracking the active stroke tip and gliding smoothly (`easeInOut`) during gaps.
- **Finish.** Pure unfiltered pixel scaling (`imageSmoothingEnabled = false`) on both buffers.

## 4. Material time

Tactile and unhurried at `30 fps`. Model the entire film as a deterministic `ops` timeline (`t0, dur, tool, col, fn, pen`) replayed up to `t`. Hand strokes draw over `0.15s–0.45s`; bucket fills pop cleanly on click; `Ctrl+V` pastes stack every `0.16s–0.22s` with brief marquee highlights; horizontal scrollbar pans ease smoothly (`easeInOut`) over `0.55s–0.75s`. Give each major beat `2.0s–3.2s` of breathing room so every painted group finishes drawing completely before the canvas scrolls away. Consecutive identical frames must stay `<= 15%`.

## 5. Piece vocabulary

Turn any noun of the brief into one of these painted `PixelDoc` pieces, drawn strictly in local `(x, y)` coordinates:

- **Main canvas viewport.** `540x230` window into the wide bitmap document, framed by a `4px` sunken `#808080` bevel and horizontal scrollbar below.
- **Figure.** See Cast construction.
- **Painted card.** Wonky double-drawn `rectO` frame (`~118x186` for showcase groups, or `~60x38` for mini-tiles) with a solid `#000080`/`#008000`/`#800080`/`#008080` header bar and white painted interior.
- **Paste stack (`Ctrl+V`).** `4` to `8` offset opaque `rectF` + `rectO` cards stamped sequentially with a dashed selection marquee on the newest card.
- **Arrow / Flow.** `3px` straight `line()` or quadratic `curve()` stroke with a `14px` two-prong arrowhead drawn progressively by the line/curve tool.
- **Counter.** `Patrick Hand` numeric readout (`32px–52px`) painted over an opaque `#ffffff` `rectF` clearing block inside a dashed text box, climbing smoothly by ease-in-out.
- **Control knob.** `13px`-radius `ellipse()` dials with `2px` pointer needles that step cleanly to new angles during calibration beats.
- **Error / Success mark.** Two fat `5px` `#ff0000` brush slashes forming an `X` for wrong states, wiped away by the white `eraser` tool and replaced by a `5px` `#008000` checkmark.
- **Emphasis.** `#ff0000` rubber-band `ellipse()` circle (`3px`) or `#ff0000` hand-drawn underline plus `#ff8040` airbrush sparkles.

## 6. Story grammar

### Cast construction

- **Scale & legibility.** Any primary character in focus occupies at least `1/3` of frame height (`>= 120px` in `640x360`, `>= 360px` at `1080p`) with a clear face (`>= 18px` in `640x360`, `>= 54px` at `1080p`).
- **Character craft.** Paint characters with bold `2px` `#000000` outlines, distinct hairstyles/beards/glasses/shirt colors via `flood()` fills, and expressive dot eyes + mouth lines. Keep the protagonist recognizable from frame `0` to the final frame.
- **Multi-character rule.** Never crowd more than `4` characters into one `540px`-wide scroll stop. Present larger casts calmly in **groups of 2 to 4** across consecutive scroll stops (`~118px` wide cards each) with `3–4` large, unmistakable painted task icons per card (drawn completely before scrolling!), reserving the full overview for the final scroll stop where the central character stays `>= 120px` tall.
- **Originality.** No real-world logos, protected characters, or brand trademarks.

### A list of N things

Never assume `N`. Scale the painted layout to keep every scroll stop clean and readable:

- **N up to 8:** Paint each item as a `70x76` card or distinct icon along the current viewport, `0.25s` per item.
- **N from 9 to 24:** Group into `2` to `4` painted columns (`3–4` clear task icons per column) across sequential scroll stops, holding `>= 0.8s` after the last icon finishes painting before panning.
- **N above 24:** Present the top-level roles in calm `4`-column scroll stops first, then pan to a clean, well-spaced matrix of mini-tiles (each showing `1` crisp local-coordinate glyph) paired with a rising painted chart or climbing counter.

### Steps

Each step of the brief is a sequence of live paint operations (`rectO` -> `hand` -> `flood` -> `typeOp`) followed by a smooth scrollbar pan to the next area of the wide bitmap. Never start a scroll pan until every stroke and icon in the current viewport has finished drawing (`>= 0.5s` settle time).

### Cause, error and fix

Cause is shown by `line()`/`curve()` tool arrows, `Ctrl+V` paste stacks, and bucket fills. An error triggers two fast `#ff0000` brush slashes (`X`) and a red label, followed by a red return curve adjusting painted dial knobs, an `eraser` wipe, and a `#008000` brush checkmark.

### Numbers and short words

Use `Patrick Hand` via `rasterText()` for short Portuguese/target-language labels (`18px–24px`), key numbers (`36px–52px`), and the closing takeaway (`30px–44px`). Never let a text string overflow or clip against its dashed text box or the `540px` viewport edge — size the `box.w` generously from `rasterText(fullString).w + 16`.

### Climax and ending

Before the final scroll stop, let the canvas pan smoothly (`0.5s–0.6s`) while background motion settles (`0.3s` pause before the climax hit). On the final scroll stop, center the calm protagonist (`>= 120px` tall) flanked symmetrically by the active system mini-tiles, circle the hero ratio/number with the `#ff0000` `ellipse()` tool, underline the unclipped closing phrase, spray `#ff8040` airbrush sparkles, and hold cleanly for at least `1.2s` (with blinking cursor and gentle idle life).

### Pacing by duration

Frame `0` (`t = 0`) MUST already be visually active and legible: open immediately with the protagonist's silhouette/head and opening hook already visible in the first viewport (never just an empty white sheet with one tiny arc). Aim for `14s–16s` across `5` calm scroll-stop beats (`2.2s–3.2s` each). Build a `BEATS` table (`id, t0, t1, scrollX, title, sounds`) before coding so camera scroll and audio share exact timestamps.

## 7. Transitions

1. **Horizontal scrollbar pan (`0.55s–0.75s`).** Smooth `easeInOut` interpolation of `scroll` across `PixelDoc` while the scrollbar thumb slides along the bottom track.
2. **Marquee drag-to-corner (`0.5s`).** Dashed selection box shrinking and moving the opening hook into a persistent corner label.
3. **Eraser wipe (`0.25s–0.35s`).** Crisp white square eraser sweeps replacing an old guess with the corrected answer.

Never use blurry crossfades or unmotivated hard cuts.

## 8. Camera

`PixelDoc` horizontal scroll (`scroll` from `0` to `EXW - 540`) inside the fixed `640x360` paint-program window. Keep all strokes and text inside `y = 14..216` so nothing ever touches the top menu or bottom scrollbar.

## 9. Sound

Synthesized `100%` via Web Audio API (`48000 Hz` stereo, `-19` to `-12` LUFS integrated, true peaks `<= -1 dBFS`, last stage `<= -4 dBFS`, no hard clipper, no silence `> 1.5s`). Picture and sound share the exact `BEATS` and `ops` clock.

**Bed.** Quiet room tone (brown noise lowpass `320 Hz`, `-38 dB`) + subtle PC tower hum (`60 Hz` sine `-34 dB`, `120 Hz` `-40 dB`).

**Vocabulary & levels.**
- Mouse micro-switch down/up: bandpass noise (`2600 Hz` down `-15 dB`, `3100 Hz` up `-21 dB`, `Q = 1.6`, `10 ms`) + `230->150 Hz` thump (`35 ms`, `-24 dB`).
- Mouse-pad slide (during drags): pink noise bandpass `650 Hz`, `Q = 0.8`, `-23 dB`.
- Bucket flood `"bloop"`: triangle sweep `260 -> 520 Hz` (`120 ms`, `-20 dB`).
- Keyboard & `Ctrl+V` paste: crisp key clicks (`2600–3800 Hz` bandpass + `160 Hz` body) capped at `<= 10` keys/s + triangle `"thup"` (`340->190 Hz`, `70 ms`) on paste.
- Scrollbar wheel notches: `7–9` rhythmic notches (`1500 Hz` bandpass `12 ms` + `180 Hz` thump) eased along each scroll pan.
- Error `X` / Climax (`0.3s` pause before climax hit): heavy brush noise + `120 Hz` thud on `X`; bright 5-note triangle chord (`C4-E4-G4-C5-E5`, `1.3 s`, `-14 dB`, reverb `0.4`) + impact thud on the hero reveal.

**Density & Mix.** Keep `3` to `10` audible events/s, max `3` simultaneous foreground voices, and stereo pan `(x_viewport / 540 - 0.5) * 1.1`.

## 10. Hero frame

The final frame (`t = duration - 0.5s`): full `640x360` Paint window with the scrollbar thumb at its rightmost stop, calm centered protagonist (`>= 120px` tall) flanked symmetrically by active mini-tiles, bold hero ratio circled in `#ff0000`, unclipped closing text underlined below, house animals in their corners, and airbrush sparkles held `>= 1.2s`.

## 11. Style check

Before finishing, inspect rendered frames at `0%`, `10%`, `25%`, `50%`, `75%`, and `95%` of duration:
- [ ] Frame `0` is already active and readable (protagonist + hook visible immediately, not an empty white sheet).
- [ ] Authentic `#c0c0c0` paint chrome (`2x8` tools, `28` colors, live `x,y` status bar, tracking scrollbar thumb).
- [ ] Primary characters `>= 120px` tall in `640x360` (`>= 1/3` frame height), showcased `2–4` at a time with every icon finished before scrolling away.
- [ ] Zero clipped text at any dashed text box or viewport edge (check the final takeaway line!).
- [ ] Calm, breathable pacing (`14–16s`, `<= 15%` identical consecutive frames, `>= 1.2s` final hold).
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
