# Y2K Liquid Chrome

Build one finished animated film in a luminous turn-of-the-millennium studio world of living liquid mercury and inflated chrome lettering: whatever the content brief tells becomes sculpted metaball droplets, specular chrome typography reflecting a studio horizon, iridescent thin-film ribbons, and frosted-glass pills floating over a pearlescent grid. The story and technical delivery follow this text.

## The film you must not make

The predictable version: flat grey vector blobs with a generic two-stop CSS gradient, harsh neon outlines over a void, illegible metallic text with jagged horizon banding, or dozens of tiny glass cards flashing past too fast to read. All of that fails. This film looks like genuine early-2000s raytraced studio chrome and frosted glass: real height-field normals, smooth environment-map reflections with thin-film iridescence, true blurred frosted panels, and calm, unhurried motion.

## 1. Identity

**Contract.** A pearlescent studio-lit world (`1920x1080` at `30 fps`) where every central object is computed from a continuous height field (`normal = grad(height)`) reflecting a rotating studio sky, softbox highlights, horizon band, and lilac floor, accented by iridescent soap-film sheen and `10px`-blurred frosted glass cards.

**Three signatures that any still frame must show:**

1. Specular liquid chrome (`y2k` metaballs and inflated typography) computed from height gradients with a crisp studio horizon reflection, exponent-`90` specular glints, and `18%–63%` grazing-angle thin-film iridescence.
2. True frosted-glass UI cards: `10px`-blurred copy of the underlying scene clipped to rounded pills, topped with a `1.5px` `#FFFFFF` specular top-left rim and soft lilac shadow.
3. Turn-of-the-millennium studio atmosphere: pearlescent off-white backdrop (`#F4F2FA` to `#E8E3F6`) with a subtle perspective grid, drifting translucent soap bubbles, and `4`-point star sparkles.

**Three exclusions:** never flat grey gradients masquerading as chrome; never jagged or speckled horizon reflections on small chrome text; never overcrowd more than `4` detailed glass cards in one beat.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the studio stage, never a stretch.

## 3. Material primitives

Pre-allocate offscreen buffers for the chrome height field, static pearlescent grid, per-call chrome lettering, and frosted-glass blur masks once at init or cache by key so `seek(t)` runs in `< 25 ms` per frame.

- **Studio backdrop.** Pearlescent radial wash (`#FAF9FF` center to `#E4DDF5` edges) over `#ECE7F8`, overlaid with a faint `#C9BFE6` (`28%` alpha) perspective horizon grid and `3%` fine monochrome film grain.
- **Studio environment map (for chrome reflections).** Sampled by elevation `ny` and azimuth: sky `#E8F3FF` to `#7CB2F5`, two crisp `#FFFFFF` rectangular softbox reflections, a narrowed `#2A2442` horizon band (filtered over `5` vertical samples on small chrome text to prevent aliasing), and a `#D5BCEF` lilac studio floor. Rotate the environment azimuth slowly (`0.08 rad/s`) so specular highlights glide continuously.
- **Liquid mercury (`height -> normal -> env`).** Sum overlapping Gaussian/metaball fields (`r = 28..90 px`) with a `1 px` signed-distance anti-aliased edge, compute surface normal from finite differences, blend `18%–63%` thin-film pastel iridescence (`#FFB8E6`, `#A8F0FF`, `#FFF3A8`, `#C3B8FF`) at grazing angles (`(1 - nz)^2.5`), and add `pow(spec, 90)` white highlights.
- **Inflated chrome lettering.** Render bold sans text (`800` weight, `Inter` or `Plus Jakarta Sans`) into an offscreen buffer, blur (`4–8 px` proportional to font size), take `height = sqrt(alpha)` (smoothing small glyphs so no horizon speckling appears), shade with the studio environment map, and ground with a soft lilac shadow (`rgba(110, 82, 168, 0.28)`) plus a `2px` `#2A2442` indigo outer contour where contrast demands.
- **Frosted-glass panels & pills.** Capture the underlying frame region, apply a `10 px` blur inside the rounded rectangle (`radius = 18–24 px`), tint with `rgba(255, 255, 255, 0.38)`, and stroke with a `1.5 px` `#FFFFFF` (`75%` alpha) top-left highlight rim.
- **Iridescent ribbons & bubbles.** Smooth cubic ribbons (`6–10 px` wide) shifting across pastel cyan/magenta/gold with pointed arrowheads; translucent soap bubbles (`r = 8–26 px`) with `1px` rainbow rims drifting upward at `18–32 px/s`; `4`-point star glints pulsing smoothly.
- **Lettering.** Minimums at `1920x1080`: chrome headlines `72 px–120 px`, essential labels `42 px–52 px`, key numbers `96 px–140 px`, secondary captions `36 px`. Always back light text with a frosted-glass pill or crisp `#2A2442` contour so it reads effortlessly over pearlescent backgrounds.
- **Finish.** Subtle `3%` cached grain and soft lilac edge vignette on every frame.

## 4. Material time

Smooth, buoyant, and elastic at `30 fps`. Mercury droplets arrive with a `back.out` overshoot (`1.12x -> 1.0x` over `0.35s`) and merge smoothly; chrome headlines inflate over `0.45s–0.65s`; frosted-glass panels glide horizontally across `0.5s–0.7s` (`easeInOut`); internal mercury droplets wobble `4x` faster during scene morphs, then settle into calm breathing (`4 px` drift). Give every major beat `2.0s–3.0s` of breathing room, limit simultaneous cards to `2–4` at a time, and keep consecutive identical frames `<= 15%`.

## 5. Piece vocabulary

Turn any noun of the brief into one of these studio-chrome pieces:

- **Central hub (the system / model).** A living liquid-mercury blob composed of `5–9` orbiting droplets that pulse, merge, and shift position (`morph`) between beats.
- **Figure.** See Cast construction.
- **Frosted-glass card.** Translucent blurred card (`~360x540` for showcase groups, or `~145x105` for grid tiles) with a pastel iridescent header pill, `1.5px` white rim, and crisp icon/portrait inside.
- **Chrome headline / Pill.** Inflated specular chrome title (`72–110 px`) for openings and key numbers, shrinking smoothly into a `44 px`-tall frosted-glass header pill in the top-left corner after the hook.
- **Iridescent ribbon.** Curved pastel-sheen ribbon carrying capsules or signals along its path, with a `14 px` chrome arrowhead.
- **Capsule / Example.** Small rounded glass pill (`~110x44`) riding an iridescent ribbon and shrinking smoothly from `1.15x` to `0.45x` as it merges into the mercury hub.
- **Control knob / Slider.** `3` circular chrome-ringed rotary knobs or glass slider pills (`38 px` tall) with specular chrome thumbs that glide smoothly during calibration.
- **Error / Success seal.** Round translucent ruby-tinted glass seal (`#FF4D79`) with a chrome `✗` for errors; mint-iridescent glass seal (`#2CE6A8`) with a chrome `✓` for fixes.
- **Emphasis.** Conical iridescent halo ring expanding around the key chrome metric plus `4`-point star sparkles.

## 6. Story grammar

### Cast construction

- **Scale & legibility.** Any primary character in focus occupies at least `1/3` of frame height (`>= 360 px` at `1080p`) with a clear face (`>= 50 px`).
- **Character craft.** Render characters as sleek, stylized studio-era figures inside frosted-glass frames or standing cleanly on the studio floor: smooth rounded silhouettes (`#2A2442` `2.5px` contours), sculpted chrome-accented outfits or accessories (glasses, collars, headsets, distinct hairstyles), warm flat-shaded skin with soft lilac rim highlights, and expressive eyes/brows. Keep the protagonist identical from frame `0` to the final frame.
- **Multi-character rule.** If a story has more than `4` characters, never crowd them all onto one screen at tiny sizes. Present them calmly in **groups of 2 to 4** across consecutive beats (`~360 px` wide frosted-glass cards each) with `3–4` clean, unmistakable vector/chrome task icons per card so every detail is easy to enjoy, gathering the full overview only in the final reunion where the central figure stays `>= 360 px` tall (`>= 24 px` minimum for any secondary face).
- **Originality.** No real-world logos, protected characters, or brand trademarks.

### A list of N things

Never assume `N`. Adapt the glass-and-chrome layout cleanly without clutter:

- **N up to 8:** Show each item as its own frosted-glass capsule riding an iridescent ribbon into the mercury hub (`0.3s` apart).
- **N from 9 to 24:** Group items into `2` to `4` frosted-glass cards (`3–4` clear glyphs per card) gliding smoothly onto stage, holding `>= 1.8s` per group.
- **N above 24:** Showcase top-level roles in calm `4`-card frosted-glass panels first, then reveal a breathable matrix of `~24–32` well-spaced glass mini-tiles (`16 px` gutters, `1` crisp glyph per tile) paired with a rising iridescent progress curve and chrome counter.

### Steps

Each step of the brief is a physical studio transition: the mercury hub morphs to a new anchor (`0.5s`), old glass panels glide `1300 px` off-stage while new frosted panels glide smoothly in (`0.55s`), and chrome ribbons trace new connections. Keep each state settled long enough (`>= 0.7s`) for comfortable reading.

### Cause, error and fix

Cause travels along iridescent ribbons (`0.4s` flow) with rising soap bubbles. An error triggers a ruby glass `✗` seal + rubbery wobble on the mercury hub, followed by a reverse pulse to `3` chrome-knob controls rotating cleanly to calibrated angles and a mint `✓` glass seal.

### Numbers and short words

Key numbers (`96–136 px`) are rendered in inflated liquid chrome with `#2A2442` soft backing; short Portuguese/target-language labels (`42–52 px`) sit inside crisp frosted-glass pills. Keep on-screen text to brief labels and numbers — zero full-sentence subtitles.

### Climax and ending

Before the final resolution, pause motion briefly (`0.3s` stillness + music drop) as the studio light warms and the mercury hub centers. On the climax beat, the protagonist sits calmly at full `>= 360 px` scale framed by symmetrical frosted-glass mini-tiles, a giant inflated chrome ratio/takeaway locks in with a conical iridescent halo and `4`-point star sparkles, and the final frame holds cleanly for at least `1.2s` (with only slow studio reflection drift and rising soap bubbles).

### Pacing by duration

Frame `0` (`t = 0`) MUST already be an active, luminous hook — open immediately with the chrome headline inflating and the mercury hub + protagonist already visible on the studio grid (never an empty pearlescent canvas). Aim for `14.5s–16s` across `5` calm beats (`2.5s–3.2s` each). Build a `BEATS` table (`id, t0, t1, title, action, sounds`) before coding so visual morphs and audio cues read from one clock.

## 7. Transitions

1. **Liquid mercury morph + panel slide (`0.55s`).** The central mercury blob flows across the studio (`internal droplets wobble 4x`), while outgoing frosted panels glide `1300 px` out and incoming panels glide `1300 px` in (`easeInOut`).
2. **Headline-to-pill shrink (`0.45s`).** The opening inflated chrome title deflates smoothly into a `44 px`-tall frosted-glass corner header pill.
3. **Iridescent ribbon sweep (`0.4s`).** A glowing pastel ribbon sweeps across the frame, revealing the next diagram stage in its wake.

Never use abrupt hard cuts or generic crossfades.

## 8. Camera

Fixed studio stage (`1920x1080`) with subtle parallax between the foreground frosted-glass cards (`1.0x`), mid-ground mercury hub (`0.85x`), and background perspective grid/bubbles (`0.5x`), plus gentle studio environment rotation (`0.08 rad/s`) so every chrome surface shimmers continuously.

## 9. Sound

Synthesized `100%` via Web Audio API (`48000 Hz` stereo, `-19` to `-12` LUFS integrated, true peaks `<= -1 dBFS`, last stage `<= -4 dBFS`, no hard clipper, no silence `> 1.5s`). Picture and sound share the exact `BEATS` clock.

**Bed & Music.** Shimmering `90 bpm` major-7th electric-piano/sine pad chord bed (`-28 dB`, lowpass `1500 Hz`) over a soft airy studio room tone (`-38 dB`).

**Vocabulary & levels.**
- Chrome letter inflation: elastic `"boing"` sine sweep (`0.55x -> 1.0x` pitch in `70 ms`, `-16 dB`) + crisp pop, triggered every `2` letters along a pentatonic scale (`<= 10` events/s).
- Mercury droplet / bubble: `"plip"` sine jump (`2.1x` frequency in `45 ms`, `-18 dB`) on droplet merge.
- Blob morph: low undulating sine (`110 -> 160 Hz`) + warm brown noise (`380 Hz`, `-22 dB`).
- Frosted panel slide: soft airy filtered pink noise (`250–850 Hz`, `450 ms`, `-20 dB`, no harsh hiss).
- Glass tap / calibration detent: pure sine with soft fifth (`-17 dB`) on each knob step.
- Iridescent ribbon: bright sweeping bandpass (`700 -> 1700 Hz`, `-19 dB`).
- Error `✗`: rubbery downward `"bwomp"` (`340 -> 110 Hz` in `300 ms`, `-14 dB`).
- Climax (`0.3s` music drop before hit): warm `5`-voice crystal chord (`C4-E4-G4-B4-E5`, `1.2 s`, `-13 dB`, `0.35` reverb) + deep `65 Hz` sub thump landing on the final chrome reveal.

**Density & Mix.** Keep `3` to `10` audible events/s, max `3` simultaneous foreground voices, all sustained tones below `2 kHz`, and stereo pan `(x / 1920 - 0.5) * 1.2`.

## 10. Hero frame

The final frame (`t = duration - 0.5s`): pearlescent studio stage with rotating perspective grid, calm centered protagonist (`>= 360 px` tall) framed symmetrically by frosted-glass mini-tiles, giant inflated liquid-chrome takeaway/ratio inside a conical iridescent ring, drifting soap bubbles, `4`-point star sparkles, and house animals nestled in the studio corners, held `>= 1.2s`.

## 11. Style check

Before finishing, inspect rendered frames at `0%`, `10%`, `25%`, `50%`, `75%`, and `95%` of duration:
- [ ] Frame `0` is already active and luminous (chrome headline + mercury/protagonist visible immediately).
- [ ] Chrome surfaces show real height-field studio reflections, softbox glints, and grazing iridescence (no flat grey gradients, no speckled horizon on small text).
- [ ] Frosted-glass cards genuinely blur the background (`10px`) with `1.5px` white specular rims.
- [ ] Primary characters `>= 1/3` frame height (`>= 360 px`), showcased `2–4` at a time with `3–4` clear task icons per card.
- [ ] Calm, breathable pacing (`14.5–16s`, `<= 15%` identical consecutive frames, `0.3s` pre-climax stillness, `>= 1.2s` final hold).
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
