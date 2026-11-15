# VHS Camcorder Title

Build one finished animated film as an authentic analog magnetic-tape camcorder recording played back on a warm CRT monitor: every element of the story is captured through a camcorder lens, recorded onto magnetic oxide tape, and displayed through phosphor scanlines, Y/C chroma bleed, tracking bands, and crisp camcorder On-Screen Display (OSD) telemetry. The story and technical delivery follow this text.

## The film you must not make

The predictable version: flat digital vector cards with a static scanline PNG pasted on top, generic neon-pink/cyan cyberpunk RGB splits, heavy static snow that makes text unreadable, or elements popping on and off in a single frame. All of that fails. This film feels like a real 1990s consumer tape played on a calibrated CRT: physical tape transport, optical viewfinder framing, phosphor bloom, analog color bleed, and mechanical deck foley.

## 1. Identity

**Contract.** Warm charcoal CRT phosphor glass (`#141318`) with subtle barrel curvature, horizontal scanlines, Y/C luminance-chroma separation (chroma lagging 3 px right of luma edges), and crisp monospaced camcorder OSD telemetry (`PLAY ▶`, `SP`, running timecode, battery meter, recording date) framing the world.

**Three signatures that any still frame must show:**

1. Authentic analog CRT & tape signal: visible 4 px scanline pitch (12% alpha), 2–3 px horizontal Y/C chroma bleed (warm amber/red and cyan-blue fringes on high-contrast edges), and subtle phosphor bloom.
2. Active camcorder OSD frame: corner brackets, top-left transport indicator (`PLAY ▶` or `REC ●` with blinking dot), `SP` tape-speed badge, battery gauge, and bottom-right running `HH:MM:SS:FF` timecode in crisp monospaced lettering.
3. Physical tape & optical framing: scenes live inside the camcorder's recorded world—illustrated in bold, slightly soft-edged analog video paint—with magnetic tracking ripple, tape-head wobble (±1.5 px horizontal jitter), and seeded dropout flecks.

**Three exclusions:** never a pure `#000000` digital black or `#FFFFFF` harsh digital white; never a generic cyberpunk neon-purple/magenta grid; never a static, unmoving frame or instant single-frame pop-in.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the viewfinder frame, never a stretch.

## 3. Material primitives

Pre-render static CRT glass, phosphor mask, vignette, and noise tile sheets into offscreen canvases before `ready` resolves; per frame, composite the moving world, apply the tape-signal pass, and draw the crisp OSD layer on top.

- **CRT Glass & Background.** Deep phosphor charcoal `#141318` to `#1D1B24` radial falloff, never pure black. Corner vignette darkens outer 18% of the frame by 35%.
- **Signal & Y/C Bleed.** Draw the scene onto an offscreen world buffer, then composite with a faint horizontal chroma smear: shift a low-alpha (`0.18`) warm red-orange copy `+3 px` right and a cool cyan copy `-2 px` left on bright edges. Keep text and OSD sharp by rendering final OSD and essential labels on top with a subtle 1.5 px phosphor glow (`#FFF3D6` at 22% alpha).
- **Three Texture Scales.**
  1. Large: soft CRT phosphor vignette and slow 24 px vertical luminance hum bar drifting downward at 45 px/s (4% alpha).
  2. Medium: horizontal tape-tracking band (18 to 42 px tall) that sweeps during transitions or jolts, displacing scanline slices horizontally by ±6 to ±18 px using seeded sine+noise.
  3. Fine: seeded analog tape grain refreshed at 24 fps (6% alpha) plus 4 px horizontal scanline pattern (12% dark, 4% bright).
- **Palette.** Closed analog broadcast palette: CRT charcoal `#141318`, tape-slate `#262430`, warm phosphor cream `#F2EAD8`, camcorder amber `#F5A623`, VHS red `#E0483E`, phosphor cyan `#5AC8D8`, oxide sage `#6EB88A`, muted warm grey `#9B958C`. Every color stays within 15–88% luminance so CRT bloom never clips.
- **Lettering.** Google Fonts: `VT323` or `IBM Plex Mono` (600) for all camcorder OSD telemetry, counters, and timecodes; `Space Grotesk` (700) or `Archivo` (700) for bold titles and scene labels. Minimums at 1920x1080: titles >= 66 px, essential labels >= 42 px, key numbers >= 96 px, captions >= 40 px, OSD corner telemetry >= 32 px. Always back labels with a soft dark phosphor plate (`#141318` at 78% alpha, 10 px padding) or 3 px dark outline so text never drowns in scanlines.
- **Finish.** Subtle barrel edge shadow (28 px inner frame), 24 fps seeded tape grain, and occasional single-frame horizontal dropout streaks (2 to 4 seeded white/grey hairlines, 18 to 60 px wide, 25% alpha) active on every frame.

## 4. Material time

Smooth 30 fps camera and character motion paired with 24 fps analog tape grain and 2 Hz blinking OSD indicators (`REC ●` dot).

- **Continuous Motion.** Every property moves slightly on every frame: handheld camcorder breathing (seeded low-frequency sway ±4 px X, ±3 px Y, ±0.004 rad tilt), tape-head micro-jitter (±0.8 px on horizontal lines), drifting dust/tracking flecks, and phosphor hum bar travel. No more than 10% of frames may be identical to the previous frame, and nothing stays still for more than 4 frames.
- **Three-Beat Action.** Elements enter over at least 0.35 s with anticipation, ease-out overshoot (+8% scale or +12 px slide), and spring settle—accompanied by a brief 0.15 s tape-tracking ripple as the signal locks. While on screen, every piece keeps a gentle idle drift or subtle pulse. Elements exit by shrinking, sliding out of viewfinder bounds, or being swept away by a tracking/rewind band over 0.3–0.5 s. Never pop in or vanish on one frame.

## 5. Piece vocabulary

Turn any noun of the brief into a physical piece recorded on tape:

- **Central Object / System.** A physical camcorder-world focal structure: a glowing CRT tape deck, a multi-reel magnetic console, or a central broadcast switchboard with spinning tape reels, VU needle meters, and indicator lamps that physically change state (reel speed, lamp color, meter level) as the story progresses.
- **Figure (Character).** Bold, clean vector-painted silhouettes with warm rim light and slight analog softness (no tiny 1 px hairlines). Distinct silhouettes, clear clothing/prop accents, expressive eyes that blink (~0.14 s every ~3 s) and track the action, plus reaction squash/stretch.
- **List Item.** A physical VHS cassette label, tape sleeve, or viewfinder picture-in-picture monitor window with its own miniature animated scene, bordered by crisp 3 px phosphor frames (`#F2EAD8`) and an individual channel/index badge (`CH-01`, etc.).
- **Arrow / Connection.** An animated phosphor signal trace or coaxial/ribbon cable that draws on along its length (`0.3–0.6 s`) with a traveling bright pulse bead (`#5AC8D8` or `#F5A623`) moving along the path.
- **Label.** Crisp `IBM Plex Mono` / `Space Grotesk` tag on a `#141318` (78% alpha) phosphor backing plate with a 2 px amber or cream border, drawn in a top pass so nothing covers it.
- **Counter.** Seven-segment or monospaced OSD counter (`>= 96 px`) that ticks upward along an ease-out power curve, locking with a brief phosphor flash.
- **Progress Graph.** Analog LED/phosphor bar-graph VU meters or segmented tape-counter bars that light up step by step with rising pitch ticks.
- **Error Mark.** Tracking loss: horizontal tearing, VHS red `#E0483E` `TRACKING ERR` OSD flash, wavy signal distortion traveling backward along the connection path to the central deck. **Fix / Success Mark:** manual tracking knob/slider settles, horizontal sync snaps crisp, green/sage `#6EB88A` `SYNC LOCK` lamp lights.
- **Emphasis.** Camcorder optical zoom-in (`1.0x -> 1.25x`) with focus-ring reticle tightening around the key subject and a warm amber highlight ring.
- **Header.** Opening title card (`>= 80 px`) that scales down to 40–45% and docks into the top-center or top-left OSD bar after the hook.

## 6. Story grammar

### Cast construction

- **Design.** Characters are drawn in bold, readable shapes with warm rim lighting, clear facial features, and consistent proportions from frame 0 to the end.
- **Scale Rule.** In main scenes, the figure in focus occupies at least one third of frame height (`>= 360 px` at 1080p) with a face of at least `50 px`. When the story has more than 4 characters, never shrink everyone onto one crowded screen: pan/cut the viewfinder to show 2 to 4 characters at a time in clear medium shots, and gather the full cast only at the reunion/ensemble moment—where no face falls below `24 px`, grouping overflow characters behind one large representative if needed.
- **Differentiation.** Distinguish multiple characters by silhouette, wardrobe color from the palette, and a distinct prop or activity—never by text label alone.
- **Originality.** No real people, copyrighted characters, brands, or logos.

### A list of N things

Never hardcode N. Handle any N gracefully:

- **N up to 8:** Each item enters as its own viewfinder monitor window or labeled tape card every `0.2–0.35 s`, arranged in a clean adaptive grid or traveling along a tape-transport rail toward the central deck.
- **N from 9 to 30:** Group items into clusters of 4–6 mini-monitors per area/channel; the camcorder pans smoothly across clusters (`0.6–0.9 s` per sweep) so each mini-window remains readable (`>= 180 px` wide when in focus).
- **N above 30:** Show the full mosaic/wall of N miniature live-animated screens pulsing in unison (each distinct by its internal animated glyph/motion), while the camera glides across a representative close-up row before pulling back to reveal the whole wall.
- Every item enters, animates continuously, and exits or resolves with the same material physics.

### Steps

Each step of the brief is a **tape recording or playback chapter**: `REC ●` captures the setup, `PLAY ▶` runs the action, `FF ▶▶` accelerates through parallel work, and `STILL ❚❚` (with live tape-head flutter, never a frozen frame) or `LOCK` marks the resolution. Keep continuous elements (the central subject, the OSD timecode, the ambient tape grain) alive across steps so scenes feel like one continuous cassette.

### Cause, error and fix

Cause travels visibly as a bright phosphor signal pulse along a drawn cable or tape path. Obstacles trigger a localized tracking tear that ripples back to the central deck; adjusting the deck's tracking/focus brings the image back into crisp sync.

### Climax and ending

Exactly one peak moment: a dramatic turning point where background music drops out for `0.25–0.35 s`, followed by a deep tape-deck thump (`50–85 Hz`), a quick camcorder push-in (`1.0x -> 1.18x`) with a 4-frame phosphor flare, and all elements locking into a unified wide composition. The final image displays the brief's closing words or key symbol largest in frame (`>= 140 px`), with the OSD showing `PLAY ▶` and the two background house animals (if applicable) tucked cleanly in the corner, held for at least `1.2 s` while gentle scanlines, timecode ticks, and handheld breathing keep the frame alive.

### Pacing by duration

Frame 0 is already the hook—tape rolling, OSD active, central subject immediately visible in a strong opening composition (never an empty black screen waiting to build). Vary shot sizes across beats (close-up -> wide reveal -> two-shot/cluster -> insert close-up -> wide ensemble). For `10–15 s` films: 3 to 4 main visual blocks with 2 to 3 physical transitions. Write a beat table first (start, end, exact on-screen text, camera/tape transition, and audio cues) so picture and sound share one clock.

## 7. Transitions

Every scene or location change (`0.4–0.8 s`) is a physical camcorder or VHS tape event—never a generic crossfade or unmotivated hard cut:

1. **Tracking Sweep.** A horizontal static-noise bar (`60–110 px` tall) sweeps top-to-bottom across the frame over `0.5 s`; the new scene is revealed cleanly behind the bar as it passes.
2. **Fast-Forward Whip (`FF ▶▶`).** Horizontal motion smear + accelerated tape-flutter lines + OSD `FF ▶▶` flash as the camera whips sideways across a continuous world to the next area over `0.5–0.7 s`, settling back to `PLAY ▶`.
3. **Optical Zoom Push / Pull.** The camcorder lens zooms smoothly (log-interpolated) into a monitor window or pulls back from a close-up to reveal the full wall of monitors (`0.6–0.8 s`), accompanied by subtle autofocus breathing.
4. **Tape Cut Flash (Time Jump Only).** At most once per film for a true jump in time: a 6-frame bright phosphor-white/static flash (`0.2 s`) with a mechanical splice click.

## 8. Camera

Handheld camcorder perspective with continuous micro-sway (`±4 px` X, `±3 px` Y, `±0.004 rad` rotation). Keyframed pans and log-scale optical zooms (`0.85x` to `1.45x`) with smooth ease-in-out. Scanlines and CRT bezel stay locked to the screen; world textures and ink lines stay locked to world coordinates, with stroke widths and essential labels counter-scaled so no text drops below minimum readable size.

## 9. Sound

Synthesize 100% of audio in Web Audio API (`48000 Hz` stereo), sharing the exact beat clock with the visual animation. Every sound lands within 1 frame (`33 ms`) of its visual contact/peak. Sample peaks in the final stage must stay at or below `-4 dBFS` (no hard clipper) so the exported MP4 sits around `-16 LUFS` with true peaks below `-1 dBFS`.

- **Bed.** Subtle 60 Hz / 180 Hz analog transformer hum (`-42 dB`) + soft magnetic tape hiss (pink noise bandpass `1.2–4.5 kHz`, `-36 dB`), fading in/out over `0.3 s`.
- **Music (optional/minimal).** Warm lo-fi analog synth pad (detuned triangle/sine through `900 Hz` lowpass, `-22 dB`) playing slow seventh chords at `84 BPM`, ducked `-4 dB` under foreground hits and muted completely `0.25 s` before the climax.
- **Vocabulary (10+ distinct foley sounds):**
  1. **Cassette Clunk (Hook / Start):** mechanical plastic+spring snap (bandpass noise `800–1400 Hz`, `35 ms` + low thud `95 Hz`, `80 ms`, `-10 dB`).
  2. **Capstan Whir (Zoom / Pan):** pitch-swept motor hum (triangle `140->210 Hz`, `400 ms`, `-18 dB`).
  3. **OSD Piezo Beep (Mode Switch / Label Lock):** crisp `1950 Hz` sine ping (`35 ms`, `-14 dB`), no harsh shrill above `2.5 kHz`.
  4. **Tracking Static Burst (Transition Sweep):** filtered white/pink noise (`600–2800 Hz`, `280 ms` envelope matching sweep velocity, `-12 dB`).
  5. **FF Tape Chatter:** rapid pitched flutter clicks (at most `10/s`, bandpass `1.1–2.0 kHz`, `-15 dB`).
  6. **Signal Pulse (Cable / Flow):** warm analog synth blip (`320->640 Hz` sine, `65 ms`, `-14 dB`), panned by screen X.
  7. **Window Pop-In (List Item):** soft CRT degauss/pop (`180->90 Hz` sine + `1.2 kHz` click, `45 ms`, `-15 dB`), pitch rising `+1` semitone per item.
  8. **Counter Tick:** soft relay tick (`1350 Hz`, `18 ms`, max `12/s`, `-16 dB`).
  9. **Tracking Error Buzz:** dissonant `110 Hz + 117 Hz` sawtooth buzz through `550 Hz` lowpass (`220 ms`, `-11 dB`).
  10. **Sync Lock Chime:** warm major-fifth analog chime (`440 Hz + 660 Hz`, `240 ms`, `-11 dB`).
  11. **Climax Impact:** deepest deck thump (`55 Hz` sine drop + brown noise lowpass `220 Hz`, `350 ms`, `-4.5 dBFS` peak) + wide warm 4-note analog chord.
  12. **Ending Resolve:** 3-note warm synth arpeggio (`60 ms` apart) resolving on tonic, followed by a soft tape-stop power-down click (`0.4 s` before end).
- **Density & Mix.** `4` to `14` audible events per second, max `3` foreground sounds simultaneously, pan `(x / 1920 - 0.5) * 1.2`, compressor (`-16 dB` threshold, `3:1`, `4 ms` attack, `180 ms` release), master gain `0.88`.

## 10. Hero frame

The closing wide shot (held `>= 1.2 s`): the CRT screen framed by subtle bezel vignette and crisp `PLAY ▶` / `SP` / final timecode OSD, showing the resolved central composition with the brief's closing title/number largest in frame (`>= 140 px`), warm Y/C chroma fringes, active scanlines, and any subtle background elements cleanly visible. It must read unmistakably as a VHS camcorder recording with zero explanation.

## 11. Style check

Before finishing, inspect rendered frames at `0%`, `10%`, `25%`, `50%`, `75%`, and `95%`:
- Is frame 0 already a strong, active hook with the OSD and central subject visible?
- Are scanlines, Y/C chroma bleed (`2–3 px`), and OSD corner telemetry visible on every frame?
- Does every element move continuously (entering, living, exiting over `>= 0.3 s` with no single-frame pops and `< 15%` static frames)?
- Are figures in main scenes `>= 1/3` frame height with faces `>= 50 px`, and crowded casts split into `2–4` per shot until reunion?
- Is all text above minimum sizes (`66 px` title, `42 px` label, `96 px` key number) and backed by a dark phosphor plate so scanlines never hurt readability?
- Are transitions physical tape/camcorder events (tracking sweep, FF whip, optical zoom) rather than generic fades?
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
