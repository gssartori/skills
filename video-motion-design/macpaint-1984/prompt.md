# MacPaint 1984

Build one finished animated film inside an authentic 1984 1-bit desktop paint workspace: whatever the content brief tells becomes a crisp black-and-white composition built inside striped-title windows, double-bordered alert dialogs, 8x8 fill patterns, Atkinson-dithered portraits, and crawling marching-ant selections, rendered into a `640x360` 1-bit framebuffer and upscaled `3x` nearest-neighbor to `1920x1080` at `30 fps`. The story and technical delivery follow this text.

## The film you must not make

The predictable version: a modern flat-design slideshow with anti-aliased grey fonts, soft drop shadows, color gradients, or a dozen tiny cramped tiles flashing past too fast to read. All of that fails. This film looks like genuine 1984 72-dpi software running live on a crisp monochrome monitor: binary `#000000` ink on `#FFFFFF` paper, tactile mouse and disk choreography, and calm, readable pacing where every beat has room to breathe.

## 1. Identity

**Contract.** Pure 1-bit monochrome (`0` = `#FFFFFF` paper, `1` = `#000000` ink) in a `640x360` `Uint8Array` buffer, blitted `3x` with `imageSmoothingEnabled = false` onto `1920x1080`. All shading comes exclusively from a `50%` checkerboard desktop, `8x8` bitmask patterns, and Atkinson error-diffusion dithering.

**Three signatures that any still frame must show:**

1. Authentic 1984 desktop chrome: `20px` white menu bar with rounded black screen corners (`[5, 3, 2, 1, 1]` pixel masks), `2px`-pitch striped window title bars with a `11x10` close box, and right-margin 1-bit desktop icons (`Disk` / `Trash`).
2. Strict 1-bit tone craft: `8x8` bitmask fills (`PAT`), `1px` hard drop shadows, `2px` thick ink arrows, and Atkinson-dithered (`6/8` error diffusion) characters or hero objects.
3. Living 1984 paint tools: an active `2x9` tool palette (inverted active cell), crawling `4px`-on / `4px`-off marching ants (`Math.floor(t * 8)`), and thresholded bitmap lettering.

**Three exclusions:** never any color pixel, anti-aliased grey alpha, or blur/glow shadow; never an empty blank screen on frame `0`; never crowd more than `4` detailed cards or cramped micro-tiles into one viewport at frantic speed.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the desktop windows, never a stretch.

## 3. Material primitives

Pre-allocate the `640x360` `Uint8Array`, the `640x360` offscreen blit canvas, and a `640x70` text-rasterization canvas once at init so `seek(t)` runs in `< 10 ms` per frame.

- **Binary ink and paper.** `#000000` (`1`) and `#FFFFFF` (`0`) only. Desktop background is `50%` checkerboard `(x + y) & 1`.
- **8x8 bitmask patterns (`PAT`).** Define at least `16` classic `8`-byte tiles (solid black, `75%`, `50%`, `25%`, `12.5%`, diagonal stripes, bricks, crosshatch, stipple, weaves) indexed via `(PAT[p][y & 7] >> (7 - (x & 7))) & 1`. Each recurring category in a brief keeps one consistent pattern all film.
- **Atkinson dithering.** Render grayscale portraits or shaded props into a small offscreen canvas, read luminance, threshold at `0.5`, and diffuse `6/8` of the error (`1/8` each to `(x+1,y)`, `(x+2,y)`, `(x-1,y+1)`, `(x,y+1)`, `(x+1,y+1)`, `(x,y+2)`).
- **Window & dialog chrome.** Windows have `1px` black borders, `1px` hard right/bottom drop shadows, `18px` striped title bars (`y+3..y+15` step `2`), `11x10` white close boxes, and centered title pills (`8px` horizontal white padding). Alerts use triple-nested `1px` frames (`0px`, `3px`, `4px` inset) and a triple-ringed rounded `OK` button (`rbox`).
- **2x9 Tool palette & pattern strip.** Left `53x181` grid of `26x20` tool cells (`select`, `lasso`, `hand`, `text`, `bucket`, `spray`, `brush`, `pencil`, `line`, `eraser`, `rect`, `frect`, `rrect`, `frrect`, `oval`, `foval`, `free`, `poly`) with the active tool inverted (`XOR 1`), a `60px` line-width selector (`1, 2, 3, 4, 6px`), and a `2`-row `8x8` pattern swatch bar at the bottom.
- **Lettering.** Google Fonts: `Inter` (`700`/`800`) for crisp UI, labels, and hero numbers; `Libre Baskerville` (`700`) for editorial titles. Rasterize to offscreen canvas (`textBaseline = 'top'`) and stamp pixels with `alpha > 120` into the `640x360` buffer. Minimums at `640x360` (scaling `3x` to `1920x1080`): headlines `22px–40px` (`66px–120px` at `1080p`), essential labels `13px` (`39px`), secondary icon captions `11px` (`33px`), key numbers `36px–44px` (`108px–132px`). Keep all text inside `x = 14..626`, `y = 22..348`.
- **Finish.** Pure pixel-doubled sharpness (`imageSmoothingEnabled = false`) plus `4` rounded black screen corners.

## 4. Material time

Calm, deliberate, and tactile at `30 fps`. Cursor glides smoothly (`easeInOut`, `0.35s–0.65s`) between targets; `8`-step `zoom-rects` expand or contract windows over `0.28s–0.35s`; Atkinson scan-line reveals wipe top-to-bottom over `0.5s–0.9s`; marching ants crawl continuously at `8` steps/s (`Math.floor(t * 8)`). Give every major beat `1.8s–3.0s` of breathing room, limit simultaneous items so the eye never feels rushed, and ensure no element pops in or vanishes on a single frame (`>= 0.3s` enter/exit). Consecutive identical frames must stay `<= 15%`.

## 5. Piece vocabulary

Turn any noun of the brief into one of these 1-bit desktop pieces, drawn strictly in local `(x, y)` coordinates:

- **Main workspace window.** Striped-title window (`~560x326` or `~616x328` in `640x360`) framing the active beat.
- **Figure.** See Cast construction.
- **Alert dialog.** Double-bordered modal (`~300x96` to `~480x180`) with a `32px` 1-bit icon (speech `?`, stop octagon, or emblem), bold headline, and default `OK` button that inverts when clicked.
- **Card / Sub-window.** Compact `1px`-framed window (`~125x250` for showcase groups, or `~64x42` for grid tiles) with a `12px` striped or solid title bar and crisp 1-bit vector/bitmap pictograms inside.
- **Icon & Pictogram.** `24x24` to `36x36` 1-bit Finder document or tool glyph drawn strictly relative to its parent card's `(x, y)` origin — never stamped at `(0, 0)`.
- **Arrow / Flow.** `2px` thick polyline (`thick()`) with a `9px` arrowhead drawing smoothly along its length (`0.3s–0.5s`); dashed (`4px` on/off) for feedback or return loops.
- **Counter.** Large `800 36px–44px` numeric readout inside a white cutout box, climbing smoothly by ease-out and framed by crawling marching ants on arrival.
- **Control slider.** `120px` horizontal track with tick marks and a `12x17` notched thumb knob sliding smoothly during calibration beats.
- **Error / Success mark.** System beep flash (menu bar `XOR 1` for `0.15s`) + stop alert + `2px` cross-out `X` for errors; crisp `2px` checkmark + inverted badge for fixes.
- **Emphasis.** Crawling marching-ant rectangle (`ants()`) or `2px` oval ring around the key metric.

## 6. Story grammar

### Cast construction

- **Scale & legibility.** Any primary character in focus occupies at least `1/3` of frame height (`>= 120px` in `640x360`, `>= 360px` at `1080p`) with a clear face (`>= 18px` in `640x360`, `>= 54px` at `1080p`).
- **Character craft.** Render recognizable 1-bit human characters using clean `2px` ink contours, Atkinson-dithered hair/beards/jackets, distinct silhouettes (glasses, collars, hairlines, posture), and expressive eyes/brows. Keep each character's visual identity consistent from first frame to last.
- **Multi-character rule.** If a story has more than `4` characters, never crowd them all onto one screen at tiny sizes. Present them calmly in **groups of 2 to 4** across consecutive beats (`~135px` wide window cards each) with `3–4` large, unmistakable 1-bit task icons per card so every detail is easy to enjoy, gathering the full overview only in the final composition where the main character stays `>= 120px` tall.
- **Originality.** No real-world logos, protected characters, or brand trademarks.

### A list of N things

Never assume `N`. Adapt the desktop layout cleanly to the brief's count without visual overload:

- **N up to 8:** Show each item as its own `1px`-bordered card or Finder document icon with a `12px` label pill below it, revealed `0.25s` apart inside one window.
- **N from 9 to 24:** Group items into `2` to `4` calm sub-windows or `4`-column rows (`4–6` clean glyphs per window), panning or stepping cleanly with `>= 1.8s` per view.
- **N above 24:** Showcase the top-level groups in `2–4` window cards first, then show the full parallel system as a clean, breathable matrix of mini-windows (with generous `4px` gutters and `1` crisp glyph per tile) under an unclipped fixed HUD title pill, paired with a climbing counter.

### Steps

Each step of the brief is a tactile desktop action: clicking `OK` on an alert, dragging a dotted marquee outline into a hub icon, stepping through `Guess / Check / Adjust` buttons, or sliding calibration knobs. Keep transitions calm (`0.3s` zoom-rect or scan wipe) and let each completed state hold for `0.6s–1.0s` so the viewer reads it comfortably.

### Cause, error and fix

Cause is shown by `2px` arrows, dotted-outline drags, and `1` active tool switching in the palette. An obstacle or wrong state triggers a `0.15s` menu-bar invert flash, a compact stop alert, and a `2px` `X`, followed by a dashed feedback arrow adjusting Control-Panel sliders and a clean checkmark.

### Numbers and short words

Key numbers (`800 36px–44px`) and short Portuguese/target-language labels (`700 13px` or `800 22px`) sit on clean white cutout pills (`4px–8px` padding) with zero sentence-long subtitles. Never allow a header pill to clip against `y < 20` or `x > 628`.

### Climax and ending

Before the final resolution, pause motion briefly (`0.3s` stillness + music drop) as the final `zoom-rect` or scan wipe prepares the hero frame. On the climax beat, the primary figure sits centered (`>= 120px` tall) inside crawling marching ants, flanked symmetrically by crisp active mini-tiles, with the closing headline and ratio/takeaway inside a double-bordered dialog or banner, held calmly for at least `1.2s` (with only marching ants and gentle idle cursor/mascot breathing).

### Pacing by duration

Frame `0` (`t = 0`) is ALREADY an active, populated hook (never an empty desktop or mid-zoom blank frame). Aim for `14s–16s` total duration across `5` unhurried beats (`2.5s–3.5s` each). Before writing drawing code, build a `BEATS` table (`id, t0, t1, title, action, sounds`) so visual timing and audio cues read from one source of truth.

## 7. Transitions

1. **Finder zoom-rect (`0.28s–0.35s`).** `8` stepped `1px` outline boxes interpolating from the source icon/button to the destination window frame.
2. **Atkinson scan wipe (`0.4s–0.6s`).** Inverted `2px` scanner bar sweeping vertically across the canvas as the new dithered image materializes above it.
3. **Pattern curtain (`0.35s`).** `8x8` stipple pattern stepping from `12.5%` -> `50%` -> `0%` white paper.

Never use blurry crossfades, CSS transitions, or unmotivated hard cuts.

## 8. Camera

Fixed `640x360` desktop frame (`imageSmoothingEnabled = false` scaled `3x` to `1920x1080`). Simulate depth and focus through overlapping windows with `1px` drop shadows, `zoom-rects`, and foreground alert dialogs rather than zooming past the menu bar (which clips HUD text).

## 9. Sound

Synthesized `100%` via Web Audio API (`48000 Hz` stereo, `-19` to `-12` LUFS integrated, true peaks `<= -1 dBFS`, last stage `<= -4 dBFS`, no hard clipper, no silence `> 1.5s`). Picture and sound share the exact `BEATS` clock.

**Bed.** Quiet room tone (brown noise lowpass `320 Hz`, `-36 dB`) + faint CRT whine/hiss (pink noise highpass `5000 Hz`, `-42 dB`).

**Vocabulary & levels.**
- Mouse micro-switch down/up: bandpass noise (`1700 Hz` down / `2300 Hz` up, `Q = 3`, `14 ms`, `-14 dB`) + `210–280 Hz` sine thump (`35 ms`, `-20 dB`).
- Mouse ball rumble (during cursor glides/drags): brown noise bandpass `260 Hz`, `Q = 1.2`, `-24 dB`.
- Floppy drive motor + head steps: `92 Hz` sawtooth (`-32 dB`) + `700 Hz` bandpass (`-34 dB`), with `950 Hz` head-step clunks (`20 ms`, `-16 dB`, max `10` steps/s).
- Zoom-rects: `8` stepped square-wave ticks rising `180 Hz -> 400 Hz` (`30 ms` each, lowpass `1200 Hz`, `-24 dB`).
- System beep (error / menu-bar invert): `1000 Hz` + `500 Hz` square waves (`170 ms`, lowpass `3200 Hz`, `-16 dB`) + low `110 Hz` thud.
- Typing / counters: crisp key clicks (`2600–3800 Hz` bandpass + `160 Hz` body) capped at `<= 12` clicks/s.
- Climax (`0.3s` silence drop before hit): `4`-voice square + triangle synth chord (`C5-E5-G5-C6` over `C3`, `700 ms`, `-14 dB`, subtle room reverb) landing on the final frame.

**Density & Mix.** Keep `3` to `10` audible events/s, max `3` simultaneous foreground voices, and stereo pan `(x / 640 - 0.5) * 1.1`.

## 10. Hero frame

The final frame (`t = duration - 0.5s`): full `640x360` 1-bit desktop with menu bar, rounded corners, central figure (`>= 120px` tall) inside crawling marching ants, symmetrical surrounding mini-windows with crisp glyphs, house animals in their corner niches, and the closing headline/takeaway cleanly centered and held `>= 1.2s`.

## 11. Style check

Before finishing, inspect rendered frames at `0%`, `10%`, `25%`, `50%`, `75%`, and `95%` of duration:
- [ ] Frame `0` is already active and readable (no blank screen or empty zoom-rect).
- [ ] Strictly binary `#000000`/`#FFFFFF` pixels in `640x360` upscaled `3x` with `imageSmoothingEnabled = false`.
- [ ] Primary characters `>= 120px` tall in `640x360` (`>= 1/3` frame height), showcased `2–4` at a time with `3–4` clear task icons per card.
- [ ] Zero overlapping cards, zero clipped HUD text (`y >= 22`), and every mini-icon drawn in local `(x, y)` coordinates.
- [ ] Calm, breathable pacing (`14–16s`, `<= 15%` identical consecutive frames, `>= 0.3s` transitions, `>= 1.2s` final hold).
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
