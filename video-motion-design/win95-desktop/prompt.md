# Win95 Desktop design system

A mid-1990s beige-box desktop operating system on a crisp pixel grid: bevelled grey chrome windows, navy title bars, aliased bitmap text, dotted pixel arrows and a classic taskbar with a waving four-pane flag. It works for landing pages, components, slides and videos. Every element lives inside the desktop.

## Identity

Teal desktop wallpaper (`#008080`) with a 24 px bottom taskbar, 2-pixel bevelled `#C0C0C0` window chrome (`#FFFFFF` / `#DFDFDF` top-left highlights, `#808080` / `#000000` bottom-right shadows), solid `#000080` active title bars (`#808080` when inactive), and aliased 1-bit pixel/bitmap typography.

**Three signatures every desktop scene shows** (a single component carries at least the bevelled chrome and the crisp pixels):

1. Authentic 2-pixel bevelled grey chrome (`#C0C0C0`) with solid `#000080` title bars, close/minimize/maximize bevel buttons, and a bottom taskbar with a `Start` button and a system clock.
2. A crisp pixel aesthetic: integer scaling with nearest-neighbor pixels, aliased bitmap text, 2x2 Bayer ordered dithering on any shaded panel, and dotted pixel arrows.
3. Active desktop interaction: an aliased pixel arrow (or hourglass) cursor clicking tabs, dragging windows, or triggering dialogs that open with 3-step outline-zoom rectangles.

**Three exclusions:** never smooth antialiased drop shadows or blurred glass; never linear gradients inside title bars; never unmotivated fade transitions or static dead frames.

## Pixels

Design on a low-resolution logical grid and scale it up by whole numbers (2x, 3x) with nearest-neighbor sampling (`image-rendering: pixelated` on the web, `imageSmoothingEnabled = false` on a canvas). Snap every coordinate to an integer pixel (`Math.round`). Never blur or smooth the pixels.

## Materials

- **Desktop & Chrome.** Teal `#008080` wallpaper. Chrome face `#C0C0C0`, highlight `#FFFFFF`, light `#DFDFDF`, shadow `#808080`, black `#000000`.
- **Bevels (2 px logical).**
  - `window`: outer TL `#DFDFDF`, BR `#000000`; inner TL `#FFFFFF`, BR `#808080`.
  - `button`: outer TL `#FFFFFF`, BR `#000000`; inner TL `#DFDFDF`, BR `#808080`.
  - `pressed`: outer TL `#000000`, BR `#FFFFFF`; inner TL `#808080`, BR `#DFDFDF`.
  - `field` (sunken): outer TL `#808080`, BR `#FFFFFF`; inner TL `#000000`, BR `#DFDFDF`.
- **Dithered Shading.** Use a 2x2 Bayer matrix (`[[0, 0.5], [0.75, 0.25]]`) to dither between palette bands on left wizard banners or active taskbar buttons (white/grey checker).
- **Palette.** Teal `#008080`, chrome `#C0C0C0`, navy `#000080`, white `#FFFFFF`, black `#000000`, shadow `#808080`, tooltip cream `#FFFFE1`, error red `#FF0000`, success green `#008000` (`#00A000` for the success icon), accent amber `#E8D050`, highlight cyan `#40A0D0`.
- **Lettering.** Crisp aliased bitmap system font for all UI chrome, tabs, status bars and badges, plus hard-thresholded `Inter` (700/800, alpha threshold > 120 snapped to 255/0) for large display headlines and key numbers. Minimum logical sizes: titles 22 px, essential labels 14 px, key numbers 32 px. Always place black text on `#FFFFFF`, `#C0C0C0` or `#FFFFE1` tooltip plates, or white text on `#000080` navy selection bars.
- **Finish.** Crisp 1 px logical outlines (`#000000`); an optional CRT bezel/scanline hint at most 3% alpha, never blurring the pixels.

## Time

Smooth cursor travel and window motion, paired with authentic stepped OS interactions: progress bars tick in discrete 7x10 px navy blocks, focus rectangles blink at 6–8 Hz, and a dragged error dialog redraws in laggy steps.

- **Something is always alive.** The cursor glides along eased paths, the clock, hourglass and LEDs pulse, progress blocks fill, data icons fly along dotted paths.
- **Three-beat action.** Dialogs and elements enter with 3-frame outline-zoom rectangles or a crisp pop-in with a 1-frame settle; active controls keep subtle idle feedback (blinking caret, spinning hourglass, pulsing status bar); elements leave by minimize/close or an outline-zoom collapse over `0.25–0.45 s`.
- **Reduced motion.** With `prefers-reduced-motion: reduce`, keep the stepped state changes and drop travel, zooms and blinking.

## Piece vocabulary

Turn any noun into a Win95 desktop piece:

- **Central Object / System.** An application window or tabbed Property Sheet with menu bar, group boxes (`etched` border + inset title), trackbar sliders, navy-block progress bars, and a 2-pane status bar whose gauges and controls change state.
- **Figure (Character).** Crisp pixel-art characters (16x16 to 48x48 logical sprites scaled cleanly 2x–4x) with distinct silhouettes, solid palette fills, 1 px black pixel outlines, blinking eyes (~0.14 s every ~3 s), and expressive reactions (sweat drop, raised arms, wide eyes).
- **List Item.** Desktop icons (`32x32` logical pixel art + centered label), file-explorer items, or sunken-bevel `#FFFFFF` mini-window cards inside a group box, each with a distinct pixel-art illustration of its task drawn inside the card.
- **Arrow / Connection.** Dotted pixel lines (`2x2` px dots spaced every `4 px`) that draw on progressively and end in a crisp pixel arrowhead, with data cards or signals stepping along the path.
- **Label.** Crisp aliased text on `#FFFFE1` tooltip boxes (`1 px` `#000000` border), `#000080` navy selection bars, or `#C0C0C0` bevelled buttons, always on top.
- **Counter.** A number inside a sunken `#FFFFFF` field or status bar, ticking upward along an ease-out curve and locking in a `#000080` navy highlight box.
- **Progress Graph.** Sunken `#FFFFFF` chart with dotted grey gridlines, a pixel-stepped green/navy line, square data markers, and a `#FFFFE1` tooltip on the final point.
- **Error Mark.** Classic `#FF0000` circle-X icon + `SYSTEM` error dialog (`bevel` frame) or a blinking `#FF0000` focus box + backward dotted red arrow; a dragged error box may smear a stair-step trail of 4–6 copies. **Fix / Success Mark:** `#00A000` green circle-check + navy highlight + classic info message box.
- **Emphasis.** A blinking `#FF0000` dotted focus rectangle or a zoom (`1.5x–2.0x`) framing the active group box.
- **Header.** A dialog title that outline-zooms into the main application's navy title bar.
- **Toggle.** A bevelled button that sinks (`pressed` bevel) when on, with a pixel indicator; never a rounded pill switch.

## Accessibility

- Real controls underneath the pixels: buttons, switches with `aria-checked`, keyboard focus shown as the dotted focus rectangle.
- Text stays real text where the medium allows; contrast follows the plate rules above.

# Win95 Desktop

Build one finished animated film as a mid-1990s beige-box desktop operating system rendered on a crisp pixel buffer and nearest-neighbor upscaled to 1920x1080: every element of the story lives inside bevelled grey chrome windows, navy title bars, aliased bitmap text, dotted pixel arrows, and a classic taskbar with a waving four-pane flag. The design system rules above set the look; this recipe turns them into a film. The story and technical delivery follow this text.

## The film you must not make

The predictable version: modern smooth rounded-corner CSS cards with drop shadows, antialiased gradients inside title bars, generic flat vector icons, or static screenshots that never move. All of that fails. This film feels like a real 1995 desktop computer in live operation: crisp 2-pixel bevels, solid navy title bars, nearest-neighbor pixel scaling, active cursor navigation, hard-disk chatter, and mechanical mouse clicks.

## 1. Rendering these rules on film

- **Buffer.** Render on a `640x360` logical buffer upscaled `3x` nearest-neighbor to `1920x1080` (`imageSmoothingEnabled = false`). Pre-render static bitmap font atlases (one per ink color) and dithered background panels before `ready` resolves; draw each frame onto the `640x360` offscreen buffer, then blit nearest-neighbor to the `1920x1080` output canvas. Bevels of 2 px logical are 6 px at 1080p.
- **Every still frame** shows the three signatures of the rules: bevelled chrome with navy title bars and the taskbar, crisp `3x` pixels, and the cursor in action.
- **Lettering at 1080p.** Effective minimums at `1920x1080`: titles >= 66 px (22 px logical at 3x), essential labels >= 42 px (14 px logical at 3x), key numbers >= 96 px (32 px logical at 3x), captions >= 40 px.
- **Time.** Smooth `30 fps` cursor travel, camera pan/zoom and window motion, with the stepped OS interactions of the rules. Every frame updates something; no more than 10% of frames may be identical to the previous frame, and nothing stays still for more than 4 frames. Smooth camera framing across the `640x360` buffer.
- **Scale of pieces.** The central Property Sheet is `628x328` logical. Figures are 16x16 to 48x48 logical sprites scaled 2x–4x inside the 640x360 buffer, so 100–380+ px tall at 1080p. Emphasis zooms the camera `1.5x–2.0x` on the `640x360` buffer. The opening header is `>= 66 px` effective.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the desktop windows, never a stretch.

## 3. Story grammar

### Cast construction

- **Design.** Characters are built in crisp pixel art with 1 px `#000000` outlines, clear facial features, and consistent proportions from frame 0 to the end.
- **Scale Rule.** In main scenes, the figure in focus occupies at least one third of frame height (`>= 360 px` at 1080p, i.e., `>= 120 px` in the `640x360` buffer) with a face of at least `50 px` at 1080p (`>= 17 px` logical). When the story has more than 4 characters, pan the camera or switch property-sheet tabs to show 2 to 4 characters at a time in clear medium shots, gathering the full cast only at the reunion/ensemble moment where no face falls below `24 px` at 1080p (`8 px` logical).
- **Differentiation.** Distinguish multiple characters by pixel-art silhouette, outfit palette color, and held prop/role badge—never by text label alone.
- **Originality.** No real people, copyrighted characters, brands, or logos.

### A list of N things

Never hardcode N. Handle any N gracefully:

- **N up to 8:** Each item appears as a desktop icon or sunken-field card in an adaptive 2–4 column grid inside a group box, popping in every `0.15–0.3 s`.
- **N from 9 to 30:** Group items into property-sheet tabs or explorer folders of 4–6 items each; the cursor clicks across tabs or the camera pans across groups so every icon remains crisp and readable.
- **N above 30:** Render a full file-explorer / tiled desktop mosaic of N miniature sunken-field windows (`>= 36x24` logical each, with a distinct pixel-art glyph drawn in local coordinates inside each box—never at `(0, 0)`!), while the camera glides over a close-up row before pulling back to show all N windows together.

### Steps

Each step of the brief is a **desktop action**: an opening dialog, a file-explorer reveal, a property-sheet tab clicked by the cursor, a progress bar filling, an error dialog/fix, and a final celebratory message box. Keep the desktop, taskbar, and cursor continuous across steps.

### Cause, error and fix

Cause travels along dotted pixel arrows (`#000080`) with stepped flying cards. Obstacles trigger a red error dialog or red dotted arrow flowing backward to trackbar sliders, which snap in discrete steps before turning `#008000` green.

### Climax and ending

Exactly one peak moment: a `0.25 s` pause before the climax, followed by a bold camera zoom + celebratory message box / system banner (`>= 120 px` effective closing symbol/words) with navy highlight, `#FFFFE1` tooltip callout, and full ensemble desktop view, held at least `1.2 s` while the cursor, taskbar clock, and subtle background activity stay alive.

### Pacing by duration

Frame 0 is already the hook—desktop loaded, first dialog/character immediately in motion (never an empty screen). Vary camera framing across `1.0x` wide desktop and `1.5x–2.0x` close-ups on active windows/figures (while keeping all essential labels inside safe margins so nothing clips at zoom). For `10–15 s` films: 3 to 4 main blocks with 2 to 3 physical OS transitions. Write a beat table first so picture and sound share one clock.

## 4. Transitions

Every scene or beat change (`0.3–0.6 s`) is a physical Win95 OS event—never a generic dissolve:

1. **Outline-Zoom Rectangles.** Three staggered `#C0C0C0` 2 px outline rectangles expanding or shrinking from an icon/dialog/taskbar button to the target window bounds over `0.25–0.4 s`.
2. **Cursor Tab Click.** The pixel arrow cursor glides to a property-sheet tab (`0.35 s`), clicks (tab pops forward, previous tab sinks), revealing the new page.
3. **Camera Pan / Zoom Across Desktop.** Smooth eased pan/zoom (`0.4–0.7 s`) across the `640x360` buffer to frame a new window or cluster, snapped cleanly on nearest-neighbor pixels.
4. **Error Cascade / Window Drag.** An error dialog pops up and is dragged across the screen, leaving a stair-step trail of frozen copies that clears on the next window focus.

## 5. Camera

Virtual camera panning and zooming over the `640x360` logical pixel buffer (`1.0x` to `2.0x` zoom, nearest-neighbor upscaled to `1920x1080`). Keep all text and icons inside safe margins (`>= 24 px` logical from edges) so zoomed shots never clip headlines or taskbar elements.

## 6. Sound

Synthesize 100% of audio in Web Audio API (`48000 Hz` stereo), sharing the exact beat clock with the visual animation. Every sound lands within 1 frame (`33 ms`) of its visual contact/click. Sample peaks in the final stage must stay at or below `-4 dBFS` (no hard clipper) so the exported MP4 sits around `-16 LUFS` with true peaks below `-1 dBFS`.

- **Bed.** Beige PC tower under the desk: soft brown-noise room tone (`320 Hz` lowpass, `-36 dB`), subtle `60/120/180 Hz` mains hum (`-42 dB`), and quiet `520 Hz` fan air (`-38 dB`), fading in/out over `0.35 s`.
- **Music (optional/light).** Minimal retro FM/triangle chord pad (`88 BPM`, `-24 dB`), muted `0.25 s` before the climax.
- **Vocabulary (10+ distinct foley sounds):**
  1. **Mouse Click (Down + Release):** crisp `2600 Hz` bandpass plastic snap (`12 ms`) + `240->150 Hz` thump, followed `90 ms` later by a lighter `3200 Hz` release click (`-12 dB`).
  2. **Soft UI Click:** duller `1400 Hz` bandpass click (`14 ms`, `-16 dB`) for buttons/cards landing.
  3. **Outline-Zoom Sweep:** smooth pink-noise bandpass sweep (`300->900 Hz` opening, `900->300 Hz` closing, `250 ms`, `-18 dB`).
  4. **Hard-Disk Chatter:** seeded burst of `420 Hz` brown-noise head-seek thunks + `1700–2600 Hz` tiny read clicks (`-15 dB`, panned `+0.35`) during loading/copying.
  5. **Progress Block Tick:** crisp `2300 Hz` bandpass tick (`16 ms`, max `12/s`, `-17 dB`) per progress-bar block.
  6. **Icon Pop-In:** short `620->280 Hz` sine pop + `3000 Hz` air click (`-15 dB`), panned by X.
  7. **Dotted Arrow Complete:** soft `1100 Hz` UI lock tick (`-16 dB`).
  8. **Trackbar Notch:** dry `900–1140 Hz` wooden/plastic tock (`50 ms`, `-14 dB`) per slider step.
  9. **System Error:** two-note descending `square` wave (`E3 -> C3`, `130 ms + 220 ms`, lowpass `1400 Hz`, `-10 dB`) + `110 Hz` low thud.
  10. **System Chime (Info / Success):** gentle sine + 2x triangle bell motif (`E5->B4` for question, `C5-E5-G5` for success, `-12 dB` with `0.3` reverb).
  11. **Climax Fanfare:** `120 Hz` impact thud + 4-note brassy detuned sawtooth arpeggio through sweeping lowpass (`900->2400->1200 Hz`) + `C3` triangle bass (`-4.5 dBFS` peak).
  12. **Ending Resolve:** soft `G4 -> C5` chime + subtle `C4` triangle sustain, fading cleanly `0.1 s` before end.
- **Density & Mix.** `4` to `15` audible events per second, max `3` foreground sounds simultaneously, pan `(x / 640 - 0.5) * 1.2`, compressor (`-16 dB` threshold, `3:1`, `4 ms` attack, `180 ms` release), master gain `0.88`.

## 7. Hero frame

The closing wide shot (held `>= 1.2 s`): the full `Win95 Desktop` at `1920x1080` showing the resolved main application window, the celebratory message box with bold display headline (`>= 120 px` effective), the taskbar with `Start` button and clock, crisp 2-pixel bevels, aliased bitmap text, and the two background house animals tucked cleanly in the desktop corners.

## 8. Style check

Before finishing, inspect rendered frames at `0%`, `10%`, `25%`, `50%`, `75%`, and `95%`:
- Is frame 0 already a strong, active desktop hook (never an empty teal screen)?
- Are 2-pixel bevels, solid `#000080` navy title bars, nearest-neighbor `3x` pixels, and the bottom taskbar visible on every frame?
- Does every miniature window/icon draw its internal graphic in local coordinates inside its own box (never piled at `(0,0)`)?
- Are characters `>= 1/3` frame height in main scenes with faces `>= 50 px` effective, and crowded casts split into `2–4` per shot until reunion?
- Is all essential text readable (`>= 66 px` titles, `>= 42 px` labels, `>= 96 px` key numbers at 1080p) and never clipped by camera zoom?
- Are transitions physical OS events (outline-zoom rectangles, cursor tab clicks, camera pans) rather than generic fades?
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
