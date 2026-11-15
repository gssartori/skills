# Wood-Type Letterpress

Build one finished animated film as a hand-pulled two-ink letterpress poster on heavy cream cotton paper: whatever the content brief tells becomes bold wood-type display typography, carved block-cut illustrations, printer's rules, and ornaments inked in charcoal-black and transparent vermilion red, stamped onto textured paper with real wood grain, ink squeeze, worn edges, slight misregistration, and physical platen deboss. The story and technical delivery follow this text.

## The film you must not make

The predictable version: a clean digital vector poster with uniform `#000000` fill, crisp mathematical edges, zero ink bleed, or a dozen tiny cramped blocks flashing past too fast to read. All of that fails. This film looks and feels like real ink pressed into cotton rag on a tabletop proof press: warm paper fibers, visible wood grain inside large type, red ink slightly off-register over black, and tactile sheet-by-sheet rhythm.

## 1. Identity

**Contract.** Two-ink letterpress printing (`#1F1C1A` charcoal-black and transparent `#C83524` vermilion red) on cached `#F3EBDC` cream cotton paper (`1920x1080` at `30 fps`). Every block is stamped with a brief platen `"kiss"` (`1.14x -> 1.0x` over `0.1s`), showing worn noisy edges, `12%` edge ink squeeze, directional paper deboss, and `2.5 px` / `0.1°` red misregistration.

**Three signatures that any still frame must show:**

1. Authentic wood-type materiality: horizontal wood-grain striations inside bold display letters (`up to 32%` ink reduction), noisy worn edges, and `12%` darker ink pooling along outer contours.
2. True two-ink overprint & misregistration: transparent vermilion red (`#C83524`) offset `2.5 px` and `~0.1°` from the charcoal-black key form, darkening naturally where inks overlap.
3. Directional letterpress deboss & cotton paper: `14%` shadowed upper-left impression wall and `4%` sunlit lower-right highlight on `#F3EBDC` paper with visible cotton fibers and deckled/tabletop framing.

**Three exclusions:** never pure `#000000` digital vector fills; never digital gradients or neon/blue colors; never crowd more than `4` detailed woodcut cards onto a single proof sheet.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the poster broadside, never a stretch.

## 3. Material primitives

Pre-render the `#F3EBDC` cotton paper (low-frequency rag variation, `300` subtle fibers, pulp flecks, and warm tabletop surround) once at init, and cache wood-grain / edge-wear noise fields so `seek(t)` runs in `< 20 ms` per frame.

- **Cotton paper & tabletop.** Sheet `#F3EBDC` (`1780x960` centered on a `#2E2824` warm walnut press bed with a soft `18 px` sheet shadow). Paper has `±3%` mottled formation, subtle `300` short fibers, and `0.2%` tiny pulp specks.
- **Two inks.** Charcoal-black `#1F1C1A` (opaque key ink) and vermilion `#C83524` (transparent `88%` multiply overprint). Ink coverage per block varies `76%–100%` so adjacent wood blocks show authentic press variation.
- **Mask-channel encoding & pixel pass (or cached block sprites).** For each printed block or display headline, encode block ink load and wood-grain phase; apply:
  - **Worn edge:** noisy threshold between sharp and `2px`-blurred mask.
  - **Wood grain:** fine horizontal grain subtracting up to `28%–32%` ink inside large areas.
  - **Ink squeeze:** `+12%` denser ink along the outer `1.5 px` contour.
  - **Directional deboss:** `14%` shadow on the top-left inner wall (`-1.5 px, -1.5 px`) and `4%` paper-light catch on the bottom-right rim (`+1.5 px, +1.5 px`).
- **Printer's ornaments & rules.** Horizontal brass rules (`2 px` and `5 px` thick), diamond dividers, `8`-point printer stars, pointing-hand manicules, and cut-out woodblock illustrations (`solid ink silhouette with crisp white woodcut gouge lines`).
- **Lettering.** Google Fonts: `Bebas Neue` or `Oswald` (`700`, condensed wood-type display), `Playfair Display` (`900`, heavy slab/serif), and `IBM Plex Mono` (`600`) for printer's colophons and numbers. Minimums at `1920x1080`: display headlines `88 px–150 px`, essential labels `42 px–56 px`, key numbers `110 px–160 px`, secondary captions `36 px`. Keep all printed blocks inside `x = 120..1800`, `y = 95..985` on the sheet.
- **Finish.** Cached paper grain and subtle vignette on every frame.

## 4. Material time

Tactile, physical, and unhurried at `30 fps`. Each letter, ornament, or woodcut block lands with a crisp platen `"kiss"` (`scale 1.14 -> 1.0` over `0.10s` ease-out, `0.04s–0.08s` stagger between blocks). Impression pressure deepens smoothly over `0.6s–1.2s`. Sheet exchanges lift the finished proof (`up 260 px, out 1500 px, 4° tilt, growing shadow` over `0.55s–0.65s`) to reveal the fresh sheet waiting on the press bed below. Give every proof sheet `2.2s–3.2s` of breathing room, and keep consecutive identical frames `<= 15%`.

## 5. Piece vocabulary

Turn any noun of the brief into one of these letterpress pieces:

- **Proof sheet (scene block).** A full `#F3EBDC` broadside bordered by `3 px` charcoal rules and corner printer's stars.
- **Figure.** See Cast construction.
- **Woodcut cliché block.** Solid charcoal-black or vermilion rounded-corner block (`~360x540` for character cards, or `~145x105` for grid clichés) with crisp `#F3EBDC` paper-white gouge carvings inside.
- **Manicule / Rule arrow.** Segmented brass-rule shaft assembled block-by-block ending in a carved printer's pointing fist or diamond arrowhead.
- **Type counter.** Bold `110–150 px` numeric block in vermilion red that stamps upward through `4–6` milestone values (`0.18s` per kiss-stamp) rather than blurry interpolation.
- **Block bar / Chart.** Columns built from stacked `24x18 px` square wood-type spacers stamping upward (`25 ms` per block).
- **Error / Success stamp.** Tilted vermilion rubber-stamp box (`-8°`, double-ruled border, distressed ink) slamming onto the sheet for errors; crisp charcoal-and-gold/vermilion laurel/checkmark cliché for fixes.
- **Emphasis.** Hand-drawn vermilion wax-pencil ring or heavy double printer's rule box around the key takeaway.

## 6. Story grammar

### Cast construction

- **Scale & legibility.** Any primary character in focus occupies at least `1/3` of frame height (`>= 360 px` at `1080p`) with a clear face (`>= 50 px`).
- **Character craft.** Render characters as bold, expressive woodcut engravings: strong `#1F1C1A` charcoal silhouettes with clean `#F3EBDC` cream gouge-line contours for hair, beard, glasses, collars, and facial features, accented by a single vermilion `#C83524` scarf/tie/badge overprint. Keep the protagonist's silhouette and gouge marks consistent across every sheet.
- **Multi-character rule.** If a story has more than `4` characters, never crowd them all onto one broadside at tiny sizes. Present them calmly in **groups of 2 to 4** across consecutive proof sheets (`~360 px` wide woodcut columns each) with `3–4` bold, unmistakable white-on-black woodcut task icons per column, gathering the full overview only on the final broadside where the main figure stays `>= 360 px` tall (`>= 24 px` minimum for any secondary face).
- **Originality.** No real-world logos, protected characters, or brand trademarks.

### A list of N things

Never assume `N`. Adapt the broadside typography and clichés cleanly:

- **N up to 8:** Stamp each item as a `2x4` or `4x2` grid of woodcut clichés (`0.22s` per kiss), each with a bold rule label below.
- **N from 9 to 24:** Group items into `2` to `4` poster columns (`3–4` bold woodcut icons per column) across sequential proof sheets, holding `>= 1.8s` per sheet.
- **N above 24:** Showcase top-level roles on `4`-column proof sheets first, then pull a clean broadside matrix of `~24–32` well-spaced woodcut clichés (`18 px` gutters, `1` unmistakable carved icon per block) paired with a rising block-spacer bar chart.

### Steps

Each step of the brief is a new **proof sheet** pulled on the press (`4–5` sheets across `15s`). Blocks on the incoming sheet stamp in smoothly (`kiss` landings) while rules lock them into a clean typographic grid. Always let the final block settle for `>= 0.7s` before lifting the sheet.

### Cause, error and fix

Cause is shown by segmented printer's-rule arrows assembling toward the central woodcut block. An error slams a tilted vermilion rubber stamp onto the sheet and shakes the press bed slightly (`4 px` dampened), followed by a red rule returning to `3` engraved gear/dial blocks rotating into alignment, and a crisp `✓` seal.

### Numbers and short words

Key numbers (`110–150 px`) and short Portuguese/target-language headlines (`72–120 px`) are treated as heroic wood-type display blocks filling their column width cleanly. Never use small prose paragraphs or subtitles.

### Climax and ending

Before the final broadside, pause motion briefly (`0.3s` stillness + music drop) as the previous sheet lifts away. On the climax sheet, the central woodcut protagonist (`>= 360 px` tall) anchors the center flanked symmetrically by crisp mini-clichés, the hero ratio/takeaway stamps in at `140 px` vermilion + charcoal overprint with full press weight, and the final broadside holds cleanly for at least `1.2s` (with gentle press-bed light/grain life).

### Pacing by duration

Frame `0` (`t = 0`) MUST already be active and legible — open immediately with the cream cotton sheet on the press bed and the opening wood-type headline + protagonist woodcut already stamping into place (never an empty walnut table). Aim for `14.5s–16s` across `4–5` proof sheets (`2.6s–3.4s` each). Build a `BEATS` table (`id, t0, t1, sheet, title, sounds`) before coding so sheet lifts, block kisses, and audio land on the exact same clock.

## 7. Transitions

1. **Sheet lift & reveal (`0.6s`).** The finished proof sheet lifts `260 px`, tilts `4°`, and slides `1500 px` off-frame with a growing drop shadow while the fresh sheet sits waiting underneath.
2. **Platen kiss cascade (`0.35s`).** A row of blocks stamps down in rapid `60 ms` succession to lock a new typographic divider.
3. **Rule-line wipe (`0.4s`).** A thick `5 px` brass rule draws across the sheet, splitting a single column into a multi-column layout.

Never use blurry crossfades or digital slides without paper depth.

## 8. Camera

Fixed overhead press-bed framing (`1920x1080`) with a subtle `2%–3%` slow creep-in during long holds and a gentle `4 px` damped press-thump shake on major stamps. Keep all type and clichés cleanly inside the `#F3EBDC` paper margins.

## 9. Sound

Synthesized `100%` via Web Audio API (`48000 Hz` stereo, `-19` to `-12` LUFS integrated, true peaks `<= -1 dBFS`, last stage `<= -4 dBFS`, no hard clipper, no silence `> 1.5s`). Picture and sound share the exact `BEATS` clock.

**Bed.** Quiet printshop room tone (brown noise lowpass `280 Hz`, `-36 dB`) + faint wood-press creak.

**Vocabulary & levels.**
- Block `"kiss"` landing: pitched thump (`150 -> 72 Hz` sine in `80 ms`, `-14 dB`) + wood-block tap (`650 Hz` bandpass, `-18 dB`) + crisp `1.8 kHz` contact click (`12 ms`), scaled slightly deeper for larger display blocks.
- Printer's rule piece: dry brass tick (`1.5 kHz` bandpass, `18 ms`, `-19 dB`).
- Sheet lift & swap: tacky ink-peel crackles (`0.16s` sparse highpass clicks) + paper whoosh (`300 -> 900 -> 280 Hz` pink noise, `-18 dB`) + soft press-bed settle thud.
- Type counter: crisp kiss-stamps capped at `<= 8` per second.
- Block-bar rattle: wooden spacer clicks (`25 ms` apart, `900–1300 Hz`, `-20 dB`).
- Error rubber stamp: heavy low thud (`90 Hz`, `-12 dB`) + dry descending wood-block interval (`E3 -> Bb2`).
- Climax (`0.3s` silence drop before hit): full platen press slam (`60 Hz` sub + brown thump, `-11 dB`) + warm `4`-note brass/organ chord (`C3-G3-C4-E4`, `1.2 s`, `-14 dB`, `0.3` reverb) on the final broadside.

**Density & Mix.** Keep `3` to `10` audible events/s, max `3` simultaneous foreground voices, and stereo pan `(x / 1920 - 0.5) * 1.1`.

## 10. Hero frame

The final frame (`t = duration - 0.5s`): full `#F3EBDC` cotton broadside on the walnut press bed, bold woodcut protagonist (`>= 360 px` tall) centered symmetrically between crisp mini-clichés, `140 px` vermilion & charcoal hero ratio/headline showing wood grain and `2.5 px` misregistration, house animals engraved as corner printer's clichés, held `>= 1.2s`.

## 11. Style check

Before finishing, inspect rendered frames at `0%`, `10%`, `25%`, `50%`, `75%`, and `95%` of duration:
- [ ] Frame `0` is already active and readable (cream sheet + stamping headline/protagonist visible immediately).
- [ ] Two-ink discipline (`#1F1C1A` charcoal + `#C83524` vermilion on `#F3EBDC` paper) with visible wood grain, edge ink squeeze, deboss rim, and slight red misregistration.
- [ ] Primary characters `>= 1/3` frame height (`>= 360 px`), showcased `2–4` per sheet with `3–4` clear white-on-black woodcut task icons per card.
- [ ] Zero overlapping blocks, zero clipped text at sheet margins, and calm sheet-by-sheet pacing (`14.5–16s`, `<= 15%` identical frames, `>= 1.2s` final hold).
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
