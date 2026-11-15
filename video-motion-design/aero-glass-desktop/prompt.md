# Aero Glass Desktop

Build one finished animated film as a late-2000s translucent glass desktop operating system rendered at native `1920x1080`: every element of the story lives inside frosted glass window frames with diagonal specular sheen, glowing aurora light ribbons, soft ambient shadows, smooth perspective window stacks, and a translucent bottom taskbar with a luminous circular start orb. The story and technical delivery follow this text.

## The film you must not make

The predictable version: flat 1990s grey pixel-art bevels, solid navy title bars, hard-edged 1-bit bitmap fonts, or static flat vector boxes with zero translucency. Also never crowd mini-windows so their borders overlap, never start frame 0 with an empty desktop, and never clip labels against screen edges or the taskbar. This film feels like a fluid, luminous glass desktop: silky `30 fps` perspective motion, layered frosted glass, aurora light flow, and warm crystalline chimes.

## 1. Identity

**Contract.** Native `1920x1080` smooth vector and glass rendering over a deep sapphire-to-emerald aurora desktop (`#081C2E` -> `#0D4A66` -> `#147A78`), framed by frosted translucent glass windows (`rgba(220, 238, 252, 0.18)` fill, `1.5 px` dark outer rim, `1 px` crisp white inner highlight, `45%` diagonal top gloss sheen, and `24 px` soft ambient drop shadow) and a floating translucent taskbar with a glowing circular start orb.

**Three signatures that any still frame must show:**

1. Translucent frosted glass windows: rounded `10 px` corners, `1 px` bright inner specular border, diagonal glossy reflection across the upper half, soft drop shadow, and glowing red/glass window-control capsules at top-right.
2. Flowing aurora & bokeh desktop: layered translucent cyan/emerald light ribbons (`8–16%` alpha) drifting smoothly across a deep sapphire-teal backdrop with subtle floating bokeh light orbs.
3. Fluid `30 fps` glass-desktop choreography: perspective window cascades, smooth `Aero` slide/flip transitions, live taskbar thumbnail previews, and glowing focus halos.

**Three exclusions:** never pixel-art nearest-neighbor scaling or hard 2-pixel grey bevels; never pure flat opaque `#C0C0C0` chrome; never overlapping cards or a blank/empty frame 0.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the glass desktop, never a stretch.

## 3. Material primitives

Pre-render the aurora light-ribbon backdrop, bokeh field, and glass-orb sprites into offscreen canvases before `ready` resolves; per frame, composite the flowing aurora background, draw the depth-sorted glass windows with shadows and specular sheen, and render crisp anti-aliased typography on top.

- **Aurora Backdrop.** Deep radial gradient (`#081C2E` center-top to `#0E3C56` mid to `#061523` edges) overlaid with 3–4 sweeping translucent Bezier aurora ribbons (`#38C6D9`, `#4FE3B5`, `#2D8CFF` at `8–14%` alpha) drifting at `12–22 px/s` + 18 soft seeded bokeh circles (`14–44 px` radius, `4–9%` alpha).
- **Frosted Glass Window.** Rounded rectangle (`r = 10 px`):
  - Drop shadow: `0 10px 28px rgba(4, 12, 24, 0.46)`.
  - Glass body: vertical gradient `rgba(235, 246, 255, 0.24)` to `rgba(180, 215, 240, 0.14)`.
  - Inner client card (when displaying bright content): soft frosted white plate `rgba(246, 250, 255, 0.92)` with `1 px` `rgba(255, 255, 255, 0.7)` border so characters and icons pop with high contrast.
  - Top specular sheen: clipped upper `42%` diagonal highlight (`rgba(255, 255, 255, 0.22)` -> `rgba(255, 255, 255, 0.02)`).
  - Double rim: `1.5 px` outer dark stroke (`rgba(10, 24, 42, 0.65)`) + `1 px` inner bright stroke (`rgba(255, 255, 255, 0.58)`).
- **Palette.** Deep sapphire `#081C2E`, aurora cyan `#38C6D9`, aurora mint `#4FE3B5`, aero blue `#2D8CFF`, glass ice `#EAF4FC`, slate ink `#182638`, alert coral `#E8544A`, success emerald `#2EC27E`, warm amber `#F5B041`.
- **Lettering.** Google Fonts: `Segoe UI` / `Plus Jakarta Sans` (600, 700, 800) for clean modern glass UI titles and labels, `JetBrains Mono` (600) for counters and system tray clock. Minimums at `1920x1080`: titles >= 66 px, essential labels >= 42 px, key numbers >= 96 px, captions >= 40 px. Always ensure `>= 18 px` horizontal/vertical padding inside glass plates and `>= 56 px` safe margin from screen edges and taskbar so no text ever clips or crowds.
- **Finish.** Subtle `4%` soft vignette, gently drifting bokeh motes, and crisp `1 px` specular edge glints on every glass frame.

## 4. Material time

Silky `30 fps` continuous motion—nothing steps or freezes.

- **Continuous Motion.** Every frame updates multiple properties: aurora ribbons undulating smoothly, bokeh motes rising/drifting (`10–18 px/s`), subtle glass reflection shimmer, gentle camera parallax/drift, and live progress/pulse indicators inside every open window. Less than `5%` of frames may be identical to the previous frame, and nothing stays still for more than 4 frames.
- **Three-Beat Action.** Glass windows and cards enter over `0.35–0.50 s` with smooth scale (`0.88 -> 1.02 -> 1.0`), `20 px` vertical glide, and opacity ramp (`0 -> 1`). Active elements breathe gently; elements exit by sliding into the taskbar orb or receding in perspective depth over `0.3–0.45 s`. Frame 0 is already an active, composed hook (never an empty desktop waiting for a window to spawn).

## 5. Piece vocabulary

Turn any noun of the brief into a sleek `Aero` glass-desktop piece:

- **Central Object / System.** A hero frosted-glass dashboard window (`1100–1480 px` wide) with glowing progress meter, live sidebar gadget, and luminous glass core whose aurora tint and meter bars respond physically to the story.
- **Figure (Character).** Smooth, clean modern vector-illustrated characters with subtle cel-shaded depth, warm rim highlights, crisp dark-slate outlines (`2.5 px` `#182638`), expressive eyes that blink (`~0.14 s` every `~3 s`), and natural posture shifts.
- **List Item.** Translucent glass live-tiles or taskbar thumbnail preview cards (`>= 180x110 px` in close-ups, `>= 120x72 px` in full-grid walls), always laid out with **explicit non-overlapping grid math (`>= 14 px` horizontal and vertical gutters)**, each rendering its own distinct animated vector illustration in **local coordinates inside its clipped glass client area**.
- **Arrow / Connection.** Smooth luminous cyan/mint Bezier light ribbons (`3.5 px` stroke + `10 px` soft glow) that draw on along their path (`0.35–0.6 s`) with glowing data beads gliding smoothly from start to end.
- **Label.** Crisp `Plus Jakarta Sans` text inside a frosted pill badge (`rgba(14, 34, 54, 0.84)` with `1.5 px` `#38C6D9` rim, `16 px` padding), drawn in a top pass with collision-free spacing.
- **Counter.** Smoothly rolling glass odometer/counter (`>= 96 px`) easing out to its target value with a soft cyan glow pulse on lock.
- **Progress Graph.** Translucent dark-glass chart panel with soft horizontal gridlines, smooth glowing emerald/cyan area curve, and a floating glass callout pill at the peak.
- **Error Mark.** Translucent coral-red glass alert toast (`#E8544A` glow) + localized glass shake + luminous red pulse traveling backward along the connection ribbon to the central gadget. **Fix / Success Mark:** `#2EC27E` emerald glass pulse + crisp check badge + smooth aurora shift to calm mint-blue.
- **Emphasis.** Soft optical depth-of-field / scale-up (`1.0x -> 1.15x`) on the focal glass window while background windows dim slightly (`85%` -> `55%` opacity).
- **Header.** Hero glass title (`>= 72 px`) that glides smoothly into the top-left glass header bar after the opening hook.

## 6. Story grammar

### Cast construction

- **Design.** Characters are sleek modern vector illustrations with clean shading, distinct hairstyles/outfits, and consistent proportions from frame 0 to the end.
- **Scale Rule.** In main scenes, the figure in focus occupies at least one third of frame height (`>= 360 px` at 1080p) with a face of at least `50 px`. When the story has more than 4 characters, use a **Flip-3D / Carousel** sweep showing 2 to 4 large character glass cards at a time in clear medium shots, gathering the full cast only at the reunion/ensemble moment where no face falls below `24 px`.
- **Differentiation.** Distinguish multiple characters by silhouette, outfit accent color from the aurora/glass palette, and a held prop/role badge—never by text label alone.
- **Originality.** No real people, copyrighted characters, brands, or logos.

### A list of N things

Never hardcode N. Handle any N gracefully with **strict non-overlapping layout**:

- **N up to 8:** Each item is a frosted glass live-tile in a balanced 2–4 column grid (`>= 24 px` gutters), entering sequentially every `0.15–0.25 s`.
- **N from 9 to 30:** Group items into `2–4` translucent glass Flip-3D panels or Aero Peek groups of 4–6 items each; the camera or Flip-3D stack sweeps smoothly across groups so every tile stays crisp.
- **N above 30:** Render a clean, non-overlapping **Live Thumbnail Wall** (`>= 14 px` gutters between every tile, zero overlap!) where each miniature glass tile runs its own distinct animated icon inside its clipped frame, while the camera glides smoothly across a close-up row (`1.35x` zoom) before pulling back to `1.0x` to reveal the entire wall.

### Steps

Each step of the brief is a **glass-desktop choreography**: an overloaded desktop/gadget stack (already active at frame 0), a central prism/orb unfolding into Flip-3D glass flows, a 2-page Carousel/Flip-3D showcase of characters, a gliding Live Thumbnail Wall, and a unified glass ensemble finale.

### Cause, error and fix

Cause travels as glowing beads along curved aurora ribbons. Obstacles trigger a coral-red glass alert + backward pulse to the central gadget, which recalibrates smoothly into emerald-mint harmony.

### Climax and ending

Exactly one peak moment: a `0.25 s` calm breath (music drops out, aurora dims slightly), followed by a crystalline chime + warm glass burst (`1.0x -> 1.08x -> 1.0x` settle) locking all glass wings symmetrically around the calm central figure and a bold hero glass badge (`>= 140 px` closing symbol/words), held for at least `1.4 s` while aurora ribbons, bokeh motes, and taskbar clock continue moving smoothly.

### Pacing by duration

Frame 0 is already the hook—frosted glass window and focal figure immediately visible and moving. Vary framing across wide desktop (`1.0x`), Flip-3D perspective cascades, and smooth close-up glides (`1.25x–1.35x`), keeping all labels inside `56 px` safe margins. For `10–15 s` films: 3 to 4 main blocks with 2 to 3 fluid glass transitions. Write a beat table first so picture and sound share one clock.

## 7. Transitions

Every scene or beat change (`0.45–0.75 s`) is a fluid glass-desktop motion—never a hard cut or 90s pixel wipe:

1. **Flip-3D Cascade.** Foreground glass windows tilt and glide smoothly backward/sideways along a 3D perspective arc while the next glass window sweeps forward into focus.
2. **Aero Peek Slide.** Background glass layers fade smoothly to frosted outlines as a new glass panel glides up from the glowing taskbar orb.
3. **Smooth Optical Camera Glide.** Continuous eased pan and zoom (`1.0x -> 1.35x -> 1.0x`) over a wide glass wall or constellation.

## 8. Camera

Smooth `30 fps` eased pan and log-scale optical zoom (`0.95x` to `1.38x`) at native `1920x1080`. Keep all essential titles, badges, and the bottom taskbar (`56 px` height) inside safe margins so zoomed shots never clip text or collide with the system tray clock.

## 9. Sound

Synthesize 100% of audio in Web Audio API (`48000 Hz` stereo), sharing the exact beat clock with the visual animation. Every sound lands within 1 frame (`33 ms`) of its visual contact/peak. Sample peaks in the final stage must stay at or below `-4 dBFS` (no hard clipper) so the exported MP4 sits around `-16 LUFS` with true peaks below `-1 dBFS`.

- **Bed.** Soft airy studio glass-room ambience: warm filtered pink noise (`650 Hz` lowpass, `-38 dB`) + subtle shimmering harmonic drone (`C3 + G3` sine at `-40 dB`), fading in/out over `0.4 s`.
- **Music (light/crystalline).** Warm Rhodes-like electric piano / glassy sine-triangle pad at `92 BPM` (`-22 dB`), playing gentle maj9 chords, ducked `-4 dB` under hits and muted `0.25 s` before the climax.
- **Vocabulary (10+ distinct foley sounds):**
  1. **Glass Window Open:** smooth crystalline whoosh (bandpass `400->1600 Hz`, `220 ms`) + soft glass tap (`980 Hz` sine, `40 ms`, `-14 dB`).
  2. **Aero Orb Chime (Start/Hook):** warm 3-note glassy bell (`G4-B4-D5`, `90 ms` spacing, `-12 dB`, `0.35` reverb).
  3. **Flip-3D Whoosh:** silky stereo-panned air glide (`300->1100->400 Hz`, `350 ms`, `-15 dB`).
  4. **Glass Tile Pop-In:** clean water-drop marimba/glass plink (`600->900 Hz` sine, `55 ms`, `-15 dB`), panned by X.
  5. **Light Ribbon Pulse:** soft harmonic shimmer (`880 Hz + 1320 Hz` sine, `90 ms`, `-16 dB`).
  6. **Taskbar Preview Hover:** delicate `1450 Hz` glass tick (`22 ms`, `-17 dB`).
  7. **Counter Roll Tick:** gentle muted wood/glass tick (`1100 Hz`, max `12/s`, `-18 dB`).
  8. **Alert Toast (Error):** warm low resonant marimba dissonance (`F3 + F#3`, `200 ms`, `-11 dB`) + soft thud (`110 Hz`).
  9. **Sync Resolve (Fix):** bright ascending glass fifth (`C5 -> G5`, `240 ms`, `-11 dB`).
  10. **Climax Crystalline Chord:** deep warm sub-drop (`65->42 Hz`, `400 ms`, `-4.5 dBFS` peak) + lush 5-note maj9 glass bell chord (`C4-E4-G4-B4-D5`) with long stereo reverb.
  11. **Ending Shimmer:** gentle descending harp/glass arpeggio (`G5-E5-C5`, `120 ms` apart), fading cleanly `0.15 s` before end.
- **Density & Mix.** `4` to `14` audible events per second, max `3` foreground sounds simultaneously, pan `(x / 1920 - 0.5) * 1.2`, compressor (`-16 dB` threshold, `3:1`, `4 ms` attack, `180 ms` release), master gain `0.88`.

## 10. Hero frame

The closing wide shot (held `>= 1.4 s`): the luminous aurora desktop at `1920x1080` showing the glowing central glass stage with the calm figure and bold hero badge (`>= 140 px`), flanked by two symmetrical non-overlapping wings of live glass tiles, the translucent taskbar with glowing orb and unclipped clock at bottom, and the two house animals tucked cleanly in the corners.

## 11. Style check

Before finishing, inspect rendered frames at `0%`, `10%`, `25%`, `50%`, `75%`, and `95%`:
- Is frame 0 already a full, active glass-desktop hook (never an empty screen)?
- Are frosted glass translucency, `1 px` white inner rims, diagonal top sheen, soft drop shadows, and the glowing taskbar orb visible on every frame?
- Are all mini-windows/tiles laid out with **zero overlap** (`>= 14 px` gutters) and local-coordinate animated graphics inside each tile?
- Are characters `>= 1/3` frame height in main scenes with faces `>= 50 px`, and crowded casts split into `2–4` per shot until reunion?
- Is all text crisp, well-padded inside plates/tray, and never clipped by camera zoom?
- Are transitions fluid glass/perspective motions (`Flip-3D`, `Aero Peek`, smooth camera glides) rather than pixel-art or hard cuts?
- Does the climax stand clearly above the rest in both visual scale and audio peak, with final peaks `<= -4 dBFS`?

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
