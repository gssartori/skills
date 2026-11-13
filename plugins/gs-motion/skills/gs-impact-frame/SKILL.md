---
name: gs-impact-frame
description: Animated film in the Impact Frame style. Turns any subject into one finished 10 to 16 second animated film, a single HTML file with sound. Use when the user asks for an animated video, explainer or short in this style.
---

# Impact Frame

Vídeo de mangá de luta: a página apanha, o obstáculo vira titã e cai em papel.

Preview and details: https://gsartori.com/skills/impact-frame

## How to use

1. If the user has not said what the film is about, ask once for the subject, the main character, the steps or items to show, any numbers and the closing line. Then go.
2. Follow the prompt below as your instructions. Put the user's subject in its "## Content" section and keep every other section exactly as written.
3. Deliver one self-contained `film.html` that plays in any browser, with sound. It exposes `window.film`, so it can also be captured frame by frame into an MP4.

## Prompt

# IMPACT FRAME

Build one animated film in the language of black-and-white battle manga: the page is the screen, and the page is being beaten up. Whatever story the content brief tells, its obstacles become things that can be hit, and every turn of the story is a strike. Nobody is hurt: obstacles are defeated and end as harmless falling paper. It must look like inked, printed pages come alive, never a cartoon with a grey filter. Numbers are decisions.

## 1. Style bible

**Two values only.** Ink `#0B0A09` on newsprint `#F2EEE3`. No grey, no spot colour. Mid-values are made of black marks: dots, hatching, dry brush. Forbidden: soft gradients, blur, glow, shadows, partial opacity. A thing is printed or absent, so nothing fades: it is cut, torn or struck away.

**Beta first.** Plan solid black before lines. Every frame carries 35 to 55% solid ink, massed in hair, coat shadow, sky and foreground, so white shapes hit like a blow.

**Line hierarchy at 1080p.** Figure contour 7 to 12 px, swelling on the shadow side. Inner forms 3 to 4 px. Folds and hatching 1 to 2 px. Backgrounds ruler-clean at 1.5 px, so wild figures feel violent against them. Every line tapers at both ends.

**Composition.** The canvas is one double-page spread. Dominant axes run at 25 to 65 degrees and horizons tilt. Cameras sit on the ground looking up, or high above looking down. A limb aimed at the viewer is 3 to 4 times the size of the head. Forward means leftward, because this page reads right to left: the workload stands left and our side attacks left. Only the final image reads left to right.

**Panels.** At least one side of most panels is diagonal. Gap between side-by-side panels 14 px, between stacked panels 34 px, border 6 px. Figures break the frame: a head, fist or coat crosses into the gutter. In act one the gutters are solid ink, for dread; they turn to paper when the allies arrive.

**Place.** The place the brief implies, staged as a battle arena at night and seen from below: a rooftop, a street, a field, a kitchen. Whatever it is, it gets a raised edge to stand on (parapet, curb, counter), three or four objects of that place scattered as cover, and worm's-eye background structures with ruled detail in true perspective. If the brief implies no place, use a city rooftop: parapet, vents, water tank, towers with ruled window grids.

**Lettering.** Sound effects are drawings inside the composition: behind a figure, cracking the ground, cut by a coat. Hero effects are Brazilian Portuguese: `TUM`, `CRÁÁS`, `BUUM`, `ZÁS`, `PÁ`, `VRUUM`, `TCHAK`, up to 60% of frame height at peak. Smaller katakana (`ドン`, `ゴゴゴ`, `バキ`) may ride beside them as graphic texture, never carrying meaning. Letters are slanted, unequal, growing along the impact direction, with a 10 px paper outline only where the background is busy.

**What breaks it:** Western comic starbursts and fonts, whole-frame halftone, tweened drift. Calm is allowed exactly once, near the end.

## 2. Technique recipes

Pre-render heavy art inside `film.ready`. Keep frames under 33 ms and avoid per-frame `getImageData`. All curves are splines resampled at about 6 px.

**Pen ribbon.** Never use `ctx.stroke()` for art. Fill a ribbon whose width follows pressure:

```js
function pen(c, pts, w, tIn = .22, tOut = .4) {
  const L = [], R = [], n = pts.length - 1;
  pts.forEach((p, i) => {
    const a = pts[Math.max(i - 1, 0)], b = pts[Math.min(i + 1, n)];
    const dx = b.x - a.x, dy = b.y - a.y, d = Math.hypot(dx, dy) || 1, u = i / n;
    const h = .5 * w * Math.max(Math.min(u / tIn, 1) * Math.min((1 - u) / tOut, 1), .02) ** .7;
    L.push([p.x - dy / d * h, p.y + dx / d * h]);
    R.unshift([p.x + dy / d * h, p.y - dx / d * h]);
  });
  c.beginPath();
  [...L, ...R].forEach(([x, y], i) => (i ? c.lineTo(x, y) : c.moveTo(x, y)));
  c.closePath(); c.fill();
}
```

**Dry brush and spatter.** A brush is many bristles. Walk `Math.ceil(w / 1.6)` parallel offset paths along the spine, each 2 px wide, each with a seeded `load` of 0.6 to 1. Skip a segment when `valueNoise(seed + i * .09) > load - dryness * u * u`, so streaks break apart toward the end. Use it for the N, the numeral, lettering tails and ink slashes. Each fast stroke ends in 40 to 120 drops with `r = 1 + 9 * rng() ** 4`, flung in a tight cone and stretched into teardrops.

**Tone.** A tile with dots at its corners and centre gives a true 45-degree screen:

```js
function tonePattern(c, s, density) {
  const t = new OffscreenCanvas(s, s), x = t.getContext('2d');
  const r = s * Math.sqrt(density / (2 * Math.PI));
  x.fillStyle = INK;
  for (const [a, b] of [[0, 0], [s, 0], [0, s], [s, s], [s / 2, s / 2]]) {
    x.beginPath(); x.arc(a, b, r, 0, 7); x.fill();
  }
  return c.createPattern(t, 'repeat');
}
```

Pitch 7 or 9 px, densities 0.12, 0.3, 0.5. Tone is cut to a form (hair, shirt shadow, sky) and moves with it. Never display a toned sprite below 70%, or moiré appears. Build gradation tone at load by varying dot radius with position. Sand tone (seeded specks) is for dust.

**Focus lines and flashes.** Wedges, not strokes: long thin triangles from a ring outside the frame to a point at radius `rIn * (.85 + rng() * rng() * 2.4)`, half-angle 0.001 to 0.007 rad, grouped in clumps of 2 to 8 so they look hand-ruled. Pre-render 3 variants of each and cycle at 8 fps so the page boils. Speed lines are the same wedges along one direction, densest beside the figure and crossing the gutter. Beta flash: solid ink with white needles stabbing out from a jagged inner edge. Uni-flash, for awe: hundreds of fine radial needles around a clean white burst.

**Impact frames.** The signature of the film. Each is a purpose-drawn image, not a filter. On a major hit: frame 1, full negative of the scene with a jagged shock outline. Frames 2 and 3, a bespoke graphic: pure black silhouette of the striker on paper, exploding radial shards, huge ink lightning that ignores anatomy. Frame 4, negative again with doubled lines. Then 3 to 6 frames of hit-stop on the most extreme drawing, canvas shaking with decaying offsets of ±24 px and ±1.2 degrees, lines still boiling. Then release. Use full-frame negatives on at most 3 flashes per second and at most 6 hits in the film, for viewer safety and because rarity gives weight. Lesser hits use a local negative inside one panel.

**Shattering panels.** Render the page to a buffer, cut it into 18 to 30 polygons (radial cracks from the impact plus 2 concentric breaks), and draw each shard by clipping that buffer. Each follows a closed-form path: `x0 + vx * age`, `y0 + vy * age + 700 * age * age`, `rot = spin * age`. Edge each shard with paper and ink.

**Aura.** Ink, not glow. A closed contour around the figure, radius by angle from three noise octaves scrolling upward in stepped time. Fill with paper, outline at 8 px, add flame ribs, let tongues detach on threes. Set it on solid ink so the figure reads as a cutout.

**Brush lettering.** Never type effects in a font. Store only the glyphs you need as stroke skeletons on a unit box and render them through the dry brush with shear and perspective:

```js
const GLYPH = { T: [[[0, .12], [1, .05]], [[.52, .08], [.46, 1]]],
  ド: [[[.35, 0], [.38, 1]], [[.4, .35], [.9, .6]], [[.72, .02], [.82, .16]], [[.9, 0], [1, .14]]] };
```

For small plain text (name plates, captions the brief asks for) load `Dela Gothic One` from Google Fonts.

## 3. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style, and never add a caption the brief did not ask for.

## 4. Characters

**Construction.** Pose a 3D skeleton of 16 joints and project it, so foreshortening is automatic: `k = f / (f + z)`, with screen position and limb width both scaled by `k`. Then ink in layers: (1) closed hulls for torso wedge, pelvis, tapered limbs and oversized hands, filled with paper; (2) beta on the side away from the light; (3) contour through `pen`, kinked at elbows and knees, notched where muscle or cloth overlaps; (4) fold clumps radiating from joints; (5) hatching that follows form; (6) tone. Hands have knuckles, four fingers and a thumb. Proportions: 7.5 heads, wedge torso. Pre-render 3 to 4 key poses per character and a bespoke face.

**Any figure the brief describes.** Color does not exist: dark hair is the 30% tone with an ink root mass at the crown, a white shine band and tapered tips; light hair is line only; a beard is a jaw-hugging solid shape broken at its edge into pen flecks. Whatever the brief says (age, hair, glasses, clothes, a carried object) becomes these marks, and they never change. The main figure gets three bespoke heads: strained with gritted teeth; extreme eye close-up with tiny iris, hatched socket and one sweat bead; calm near-smile.

**Allies.** When the brief brings in more characters, each is a human in stylised gear with an unmistakable thumbnail silhouette (one basic shape per character: vertical triangle, circle, jagged star, lopsided hunch, square, thin diagonal, cloud, black obelisk; cycle if there are more) and the tool of their job carried as a weapon. When the brief names a role or job, a plate with that word is stamped on landing.

**The obstacle.** Whatever weighs on the story becomes a titan made of the obstacle's own material, never alive enough to suffer: for work, towering shoulders of paper stacks, binders, boxes, envelopes and ringing phones; for weather, cloud and hail; for distance, road signs and suitcases. Two empty rectangular gaps for eyes. Three pre-rendered depth layers with hundreds of individual items. Chunks tear away when hit and turn into finished, harmless paper.

## 5. Story grammar

**Steps as strikes.** Map the brief's sequence onto acts. Each step is a strike, a landing or a break of the page: something hits, crashes, opens, tears. If a step would only get a caption, find the hit.

**A list of N things.** Never assume N. Each item is a small slanted manga panel with a thick ink frame: a point of view where a forearm or tool enters from a corner and does one job. When items belong to groups, the cuff shows the group by pattern: double stripe, beads, zigzag, dotted trace, hazard diagonals, pinstripe, small hearts, solid ink with one button (cycle if more). Write a separate drawing function per item, with no shared card template. Each has 3 pre-rendered phases cycled on threes so the action happens.

- N up to 8: items arrive one per beat, smashed into the spread like thrown cards.
- N from 9 to 30: items fan out in groups of up to 6 behind each ally as they land; in the attack, 3 per group come close enough to read and the rest whip past.
- N above 30: the first 6 to 8 at full size, the rest as a storm of tiny panels whipping past in the camera's slipstream.
- Two items that could be swapped without anyone noticing have failed: each needs its own object, gesture and sound.

**Numbers and short words.** A number or short word the brief puts on screen crashes down at a brutal angle, the height of the canvas, with an impact frame, and settles; when the story opens it, its strokes split and swing out like gate doors, and ink rivers flood at the viewer.

**Climax and ending.** Exactly one impact is the biggest in the film: everyone strikes at once, the obstacle explodes into paper rain, then white and near silence. The last image is built from the story's own elements (items fly in and tile the letters of the brief's last word or number; one loaded brush stroke writes; ink drops strike), held at least one second with only falling paper and slow boil, readable at a glance.

**Pacing by duration.** Hook within the first 2 s. Something changes every 1 to 2 s. 150 BPM: a beat is 0.4 s, 12 frames. At about 10 s use 3 acts; at 13 to 15 s use 4 to 5 acts. Picture and sound read one `EVENTS` array of `{t, kind, x}` built from a beat table (start, end, exact on-screen text, the hit that causes the cut, main sounds), so every hit lands on the same frame.

## 6. Animation language

**Stepped time.** Figures move on threes: `Math.floor(t * 10) / 10`. Only shake, speed lines, particles and shards run at 30 fps. Extreme poses snap, with 1 smear frame: a dry-brush streak with 2 to 3 echoes. No eased tweens between drawings.

**Tame and release.** Hold before a hit; show windup and aftermath, keep contact brief.

**Camera.** Moves are hits: whip pans over a still drawing, crash zooms in 3 frames, tilts snapped to a new diagonal, depth layers in parallax.

**Causal transitions only.** Something crushes the page, a shape opens like gates, a character punches through a panel, a thrown item slices to the next area, a blast whites the page, paper falls into the final image. The swap happens while the page is covered. No crossfades, slides or wipes.

**Always alive.** Every second has at least 5 independent motions: boil, tumbling paper, dust, spatter, aura, coat and hair flutter, items running, cracks spreading. Lettering arrives at 140%, snaps to size in 2 frames, shakes ±6 px for 6 frames, then is cut or torn away. Everything is a closed-form function of `t`.

## 7. Sound design

Manga's sounds are drawn. So this world's sound is **the drawn hit made audible, played by a wooden stage ensemble**: taiko, wooden clappers, a plucked shamisen-like string, and the page's own materials: paper, brush, ink. No pad, no electronic beat, no melody on top. One function renders on any `BaseAudioContext`. `renderAudio()` runs it offline; Play starts that cached buffer, and picture time reads the `AudioContext` clock. Seed all noise. Reverb is a stage hall: 1.4 s decaying noise impulse, 18 ms pre-delay, low-pass 3.5 kHz. Each sound lands on the drawn frame of contact, on the same 10 fps step as the picture.

**Instruments**

- `don` (taiko): sine from `2.1f` to `f` in 45 ms, sagging to `.86f` by 0.5 s; attack 3 ms, decay 0.62 s. Add partial at `1.59f` for 90 ms at 35%, slap of noise band-passed 850 Hz Q 1.2 for 16 ms, stick click above 3 kHz for 4 ms, `tanh` drive. Default `f` 74 Hz.
- `ka` (rim): noise band-passed 1.9 kHz Q 6, 30 ms.
- `tsuke` (wood on board, the crack that punctuates a stage pose): noise burst through parallel band-passes at 1180, 2650, 4100 Hz, Q 18, decay 50 ms; 240 Hz thud for 70 ms; softer second hit 28 ms later.
- `bachi` (pluck): Karplus-Strong string, preceded by a skin slap of noise band-passed at 1.4 kHz, with soft waveshaper buzz. Scale: D, Eb, G, A, Bb.

**Effects**

- **Weight:** brown noise low-passed 90 Hz; creaks of the obstacle's material (noise at 300 to 700 Hz with irregular ticks, 12 to 30 per second).
- **Cracks:** low thud plus dry 2 to 5 kHz grains.
- **Eye strip:** an inhale, noise band-passed rising 500 to 1400 Hz in 0.3 s.
- **Clapper accelerando:** before the first big crash, `tsuke` intervals shrink from 0.38 s to 0.03 s, then dead silence for the 2 frames before the hit.
- **Big crash, stacked:** reversed noise swell over the prior 0.3 s; sine sub 64→28 Hz over 0.9 s; two `don` at 58 Hz; driven high-passed noise crack, 12 ms; 40 debris grains over 0.9 s; card-tear tail.
- **Gates opening:** wooden groan (saw at 38 Hz with 7 Hz roughness, band-passed 200 to 800 Hz), then a rising noise rush with paper flutter (15 Hz tremolo above 1.5 kHz).
- **Brush stroke:** noise band sweep 700→2400 Hz through a 9 ms comb, feedback 0.5, peaking at 60% of its length; lasts exactly as long as the stroke.
- **Ink spatter:** sine 300→90 Hz in 30 ms plus low-passed wet noise.
- **Shatter:** thick card snapping, 14 to 20 clicks at 2 to 6 kHz. No glass.
- **Item flight:** short noise sweep up and down, panned by `x`.
- **Aura:** two detuned saws at 55 Hz, low-pass 120→900 Hz, 22 Hz tremolo, sparse crackle.

**Ally signatures.** Each landing is `tsuke` + `don` + one rising `bachi` note (D3 up the scale) plus one signature from the ally's tool, in order of appearance: bronze bell (partials 1, 2.76, 5.4, 8.9 × 180 Hz); rattle of 8 wood ticks; clipped megaphone blare (saw band-passed 1.3 kHz, 0.2 s); servo whine and key burst; chain rattle and metal crate thud; hand bell and whip crack; double heart thump with small bells; gavel on a hard block with short ring. Cycle if there are more allies.

**Item sounds.** Each item that comes close enough to read gets a distinct sound under 0.2 s on the frame it acts, built from the effects above to match the drawn object.

**Arc**

- **Burden:** sparse and low. Quiet `don` heartbeat every 0.8 s, rumble, creaks.
- **First crash:** silence, the biggest low end so far, then the flood.
- **Allies:** the ensemble wakes: `don` on beats, `ka` on offbeats, rising `bachi`.
- **Attack:** double-time taiko roll, a 2-bar `bachi` ostinato on D, Eb, A, item sounds on top.
- **Together:** final build, peak hit (the single biggest of the film), then the rug pull: 0.35 s of near silence with a thin 3.2 kHz ring and reverb tail. Paper patter enters like rain. One bamboo-flute note on D (sine plus breath noise, bending up a quarter tone, slow vibrato) brings calm, over many tiny ticks merging into a soft purr.
- **Ending:** each stroke of the final image is a brush stroke and `don`; ink drops are `tsuke`; the last stroke is `don`, bell and `bachi` D together, ringing through the hold.

**Density.** 5 to 15 audible events per second outside the rolls; at most 3 foreground sounds at once; repeated ticks at most 12 per second.

**Mix.** Sub 30 to 70 Hz only for big hits; taiko 70 to 400 Hz; wood and strings 1 to 4 kHz; paper above 3 kHz. Duck the music bus 6 dB for 40 ms at each hit. Leave 1 to 2 empty frames before a major hit. Pan by `(x / 1920 - .5) * 1.4`. If two effects collide, delay or drop the lesser. After rendering, measure K-weighted gated loudness in JavaScript, gain toward -16 LUFS, soft-limit below -1 dBFS.

## 8. Density, and how this fails

**The predictable version, which you must not make:** white screen with thin outlines; round-headed stick figures; a grid of rounded rectangles with emoji; a comic burst saying POW in a Western font; a grey filter; a red accent; smooth zooms; crossfades; a stock taiko loop with generic whooshes and a pad.

**Instead,** every frame stacks at least four depths: foreground debris or a huge cropped form, characters, obstacle or items, inked background. Empty paper exists only as a deliberate shape. The two house animals from the house animals brief watch the fight from the cover, inked with the same line and tone, untouched by every blast. Every item is recognisable when paused.

**Before finishing:** any paused frame must look like a printed spread worth hanging on a wall. Remove every picture use of `globalAlpha`, `shadowBlur`, `filter` and non-ink colours. A recurring character must plainly be the same person at 5% and at 85% of the duration. Every step of the brief has a hit, not only a caption. Exactly one biggest impact; the final image holds at least one second. Text sizes on 1920x1080: titles at least 66 px, essential labels 42 px, key numbers 96 px. Finish the entire file with compact helpers: no placeholder, stub, or unwritten character or item.

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
