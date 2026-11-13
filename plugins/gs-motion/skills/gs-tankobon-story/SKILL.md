---
name: gs-tankobon-story
description: Animated film in the Tankobon Story style. Turns any subject into one finished 10 to 16 second animated film, a single HTML file with sound. Use when the user asks for an animated video, explainer or short in this style.
---

# Tankobon Story

Vídeo de mangá impresso em preto e branco: retícula, painéis inclinados e onomatopeias desenhadas.

Preview and details: https://gsartori.com/skills/tankobon-story

## How to use

1. If the user has not said what the film is about, ask once for the subject, the main character, the steps or items to show, any numbers and the closing line. Then go.
2. Follow the prompt below as your instructions. Put the user's subject in its "## Content" section and keep every other section exactly as written.
3. Deliver one self-contained `film.html` that plays in any browser, with sound. It exposes `window.film`, so it can also be captured frame by frame into an MP4.

## Prompt

# Tankobon Story

Build a short animated film that lives on the printed pages of a black-and-white manga volume. This is not cartoons with a comic filter. Ink and paper come alive: panels cut themselves, tone dots swell, pages turn, and every sound effect is both drawn on the page and heard. It must feel lavishly animated at every instant.

## 1. Style bible

**Materials.** Black ink and paper, nothing else. Paper `#F2EEE3` with faint fibres; ink `#14110F`. No color, no grey fill anywhere. Every grey the eye sees is made of real black marks: dots, lines or hatching. This one rule decides whether the film looks printed or fake.

**Line.** Pen-pressure line: thick where form turns away or takes weight, thin toward the light, always tapering to a point. Outer contours 5 to 8 px, interior 2 to 3 px, hair and hatching 1 to 1.6 px. Panel frames are ruled and even, 4 px.

**Four values.** Spot black (hair, shadows, clothing), tone (dot screens in gradation), hatching (hand strokes on round forms), bare paper. Plan each panel as black, grey and white shapes first. At least 15% of each spread is solid black, and real white is left around heads and balloons.

**Tone.** Dots stay visible, 7 to 10 px pitch. Past 50% coverage they merge and invert into white dots on black. Tone sweeps in gradation across a panel, never an even fill. Mood lives here: dense for burden, sparse for calm. Highlights are scratched out with a blade.

**Composition.** Read right to left, top to bottom; the story travels leftward. The 16:9 frame is an open two-page spread with a faint fold at center. Five to seven panels per spread, huge size contrast, slanted edges, one dominant panel. Gutters inside a tier are thin, about 12 px; gutters between tiers are two to three times wider. Some panels bleed off the page. Figures and lettering break frames. Shots change constantly: an eye, a hand alone, low angle, overhead, silhouette.

**Lettering.** Narration: rectangular boxes, thin border, serif. Speech: slightly lumpy hand-shaped ovals with a sharp tail; spiky bursts for shouts; clouds for thought. Sound effects: huge katakana drawn into the scene. Portuguese text reads left to right, but balloons are placed in right-to-left order.

**Numerals.** When a number matters it is enormous, hand-inked, and occupies the panel like a heavy object.

**What breaks the style:** opacity fades of any kind, soft shadows, `shadowBlur`, smooth grey gradients, any color, rounded app cards, even-width vector outlines, centered symmetrical grids, typed SFX, text laid over a drawing. Print has no fades: things arrive by cut, ink flow, blade, page turn, or tone density growing.

## 2. Technique recipes

Work on a 2304x1296 plate, then composite to 1920x1080 through a page camera (scale 0.833 to 1.0, plus drift and shake). Bigger pushes are done by drawing the subject bigger inside its panel, so dots stay print-sized. Stack per frame: tone plate, screening pass, ink plate, paper, camera.

**A. Real screentone by threshold.** The tone plate is an opaque canvas that starts black and stores tone amount by channel: red for fine dots, green for coarse dots, blue for parallel line-tone. `rgb(128,0,0)` means 50% fine dots, and normal canvas gradients from `rgb(0,0,0)` to `rgb(220,0,0)` give true graded dots. Each frame, screen it to ink pixels. The cosine spot function grows dots, reaches a checker at 50%, then inverts into white dots, as the tradition does.

```js
const T=16, tile=new Float32Array(T*T);        // periodic 45-degree screen
for(let y=0;y<T;y++)for(let x=0;x<T;x++){
  const u=(x+y+.5)/T*Math.PI*2, v=(x-y+.5)/T*Math.PI*2;
  tile[y*T+x]=.5-.25*(Math.cos(u)+Math.cos(v));
}
// per pixel: tv=red/255; a=ink alpha. Zero tone must stay clean paper.
const a = tv<.02 ? 0 : Math.min(1,Math.max(0,(tv-tile[((y+oy)&15)*T+((x+ox)&15)])*7+.5));
```

Add a 32 tile for green and a slanted line screen for blue; take the maximum of the three. Use `willReadFrequently` and one reused ImageData. Run the pass per panel with that panel's `(ox, oy)`, so its dots slide with it. Scratch highlights by painting zero with tapered strokes.

**B. Occlusion across plates.** Every solid thing paints both plates in one call: fill its silhouette black on the tone plate, `destination-out` it on the ink plate, then add its own tone and ink. Otherwise backgrounds show through figures.

**C. The pen stroke.** Never `stroke()` with `lineWidth` for drawing. Fill a polygon.

```js
function ink(c,pts,w,seed,tA=.15,tB=.35){      // pts: resampled spline
  const N=pts.length-1,L=[],R=[];
  for(let i=0;i<=N;i++){
    const s=i/N,p=pts[i],q=pts[Math.min(i+1,N)],r=pts[Math.max(i-1,0)];
    let nx=r.y-q.y,ny=q.x-r.x,m=Math.hypot(nx,ny)||1;nx/=m;ny/=m;
    const h=.5*w*Math.min(1,s/tA,(1-s)/tB)**.7*(.85+.15*noise(seed,s*3))+.25;
    L.push([p.x+nx*h,p.y+ny*h]);R.unshift([p.x-nx*h,p.y-ny*h]);
  }
  c.beginPath();[...L,...R].forEach(([x,y],i)=>i?c.lineTo(x,y):c.moveTo(x,y));c.fill();
}
```

Line boil: jitter control points 0.7 px with a seed from `floor(t*8)%3`, so held drawings breathe.

**D. Hatching on round forms.** Light comes from upper right for the whole film. From a shadow edge on a sleeve, cheek or fold, fire strokes along the cross-contour of the form, curved, 6 to 9 px apart, thick at the shadow and tapering to nothing toward the light, with seeded lengths so the edge feathers. Add a second bundle at a slight angle in the deepest area. On large surfaces use bundled patches of short strokes whose patches never cross; add directions to go heavier.

**E. Effect lines.** Focus lines: 150 to 260 wedges pointing at a focal point, starting outside an irregular ellipse and running off the panel, in uneven bundles, reseeded every two frames. Speed lines: parallel wedges tapered at both ends, some white over black. Dripping lines: uneven vertical strokes hanging from the panel top, for dread and burden.

**F. Drawn sound effects.** Kana subsets load on demand, so pass the characters: `await document.fonts.load('200px "Dela Gothic One"', allKanaUsed)`. Narration: Shippori Mincho B1 800. Balloons: Kaisei Tokumin 700. Never `fillText` an SFX to the frame. At `ready`, render each large on its own canvas, cut it into 2 px vertical strips, and redraw with shear, a sine bend and per-glyph scale, first character largest. Erase dry-brush streaks with thin tapered `destination-out` strokes, spatter drops, add a thick paper-white outline and, for the biggest, a black extrusion. Draw it behind the foreground figure and in front of the background, and let it shake and crumble with its impact.

**G. Living page.** Panels are polygons over shared movable nodes, so gutters keep their width while the layout changes. Page turn: slice the spread into 6 px strips rotating around the center fold with cosine foreshortening, and a band of coarse tone as shadow on the lifted paper.

Pre-render heavy drawings at `ready` as paired tone and ink sprites, three boil variants per pose. Cache only what does not depend on time.

## 3. Priorities

The content brief you receive decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style.

## 4. Characters

Forbidden for anything alive: `arc`, `ellipse`, `rect`. Each figure is a hand-plotted list of strokes in its own box, 120 to 260 strokes at hero size, head about 1/6 of body height. Poses are the same stroke arrays with different control points, stepped at 12 fps: drawing animation, not a puppet.

**Building any figure the brief describes.** Three-quarter view, facing the direction the story travels (leftward).

1. Head contour in separate strokes: forehead, brow notch, cheekbone, jaw corner, chin, heaviest under the jaw.
2. Eye line at 52% of head height. Near eye 17% of head width, far eye 12%: heavy tapered upper lash arc, thin broken lower line, tall iris cropped by the lid, solid pupil, one large and one small catchlight, tone under the lid.
3. Nose: a small wedge tick. Mouth: one line, a corner tick, three hatches beneath.
4. Hair and facial hair as clumped tufts in graded tone with a scratched highlight band. Color never exists: dark hair is 45 to 70% tone, light hair is bare paper edged with fine strokes, grey hair is 20% fine tone. Beards are fine tone edged with 60 to 90 short tapered strokes.
5. A solid black wedge under the chin, ear, neck, clothing in one flat tone value plus folds at elbow and shoulder.

Whatever the brief says about a figure (age, hair, glasses, build, clothes) becomes these marks, and they stay identical in every shot. Give each figure three acting poses that fit the story's arc, drawn from this vocabulary: **Crushed** (head sunk below shoulders, knit brow, half-lidded, sweat), **Struck** (looking up, tiny pupils, hair lifted), **Calm** (upright, wide shoulders, soft corner smile), plus one pose of the figure doing its own work.

**Several figures.** Each must be identifiable as a solid black silhouette alone: change one strong attribute per figure (hair mass, build, a carried object, a garment shape), never only a caption. Figures that belong to a main figure trail a thin ink thread from the collar back to it, so relationships read as drawn lines.

## 5. Story grammar

The style does not know the story. These rules say how any story lands on the page.

**Movements.** Map the brief's sequence onto spreads. Two story steps per spread is normal; one spread per step only when a step is a turn of the story. Each step gets one verb that the ink and paper perform: press, fall, cut, pour, turn, tie, gather. If a step would only get a caption, it is not on the page yet: find what the ink does.

**A list of N things.** Never assume N. Each item is a real miniature manga panel: slanted inked frame, its own tone, a small katakana sound, a hand or sleeve at the near edge working on one dominant object, with perspective, cast shadow and a background. Draw at 640x440; it must still read at 200 px.

- N up to 8: panels fire open one by one, right to left, top tier then bottom, one every 5 to 8 frames.
- N from 9 to 30: group items into spreads of up to 6, and turn the page between groups; inside a spread, panels fire every 3 to 5 frames.
- N above 30: show the first 6 to 8 at full size, then let the rest arrive as a riffle of small panels at 2 frames each, and finally as tone texture filling the spread.
- Every item uses the same entry (blade cut, panel opens, figure breaks the frame) and the same exit (panel folds along its gutter). Variety comes from the drawn object and its sound, not from a different animation.
- Two items that could be swapped without anyone noticing have failed: each needs a different object, gesture and sound.

**Groups.** When the brief groups items (teams, places, chapters), each group gets its own spread layout so groups read apart before any text: radiating fan, strict ledger grid, scattered tilted panels, tall columns, diagonal conveyor tiers, narrowing funnel, soft rounded frames, stacked drawers. Cycle through them in this order; never repeat a layout on consecutive spreads.

**Numbers and short words.** A number or short word the brief puts on screen is enormous, hand-inked, carved, hatched, graded, with a solid extruded side, and it lands like a heavy object: inverted impact, focus lines, ink splash.

**Weight, release, result.** Burden is dense tone and dripping lines; release is tone draining to bare paper; a result is a full-bleed page at full ink strength.

**Climax and ending.** Exactly one impact is the biggest in the film: the moment the brief's key image lands. The last image is a full-bleed page, held at least one second with only line boil and tone breathing, and it must read alone as a thumbnail.

**Pacing by duration.** Hook within the first 2 s. Something changes every 1 to 2 s. At about 10 s use 3 spreads and 2 page events; at 13 to 15 s use 4 spreads and 3. Write a beat table before drawing: one row per beat with start, end, exact on-screen text, what carries over from the previous beat (or which transition and why), and the main sounds. Picture and sound both read times from that table.

## 6. Animation language

Grammar: key pose, anticipation, a violent move of one to three frames, overshoot, then a *moving hold*. Drawing steps at 12 fps for snap; effects, shake and particles run at 30 fps. Fast moves use hand-drawn smears: the limb stretched along its path with a tail of speed lines, one or two frames. Impact: two frames of the page inverted, one of bare white, then eight frames of decaying shake with panels jolting on their nodes.

Every second, at least four of these run: line boil; a figure acting; hair and cloth following; effect lines reseeding; tone swelling; gutters drifting; lettering trembling; sweat, spatter, sheets of paper, steam; threads pulsing. No panel ever sits still.

**Transitions, all physical, all from the page:**

- **Page turn:** a hand grabs a page corner and turns it (0.4 to 0.6 s); the new spread is revealed behind the lifted paper.
- **Blade:** a cut runs along a line and the page opens like a book at that spine; ink pours out and becomes the next gutters.
- **Ink drain:** tone drains to bare paper; one small panel remains and grows into the next spread.
- **Threads:** panels fold along their gutters and run up ink threads into the object that comes next.

The swap always happens while the page is covered (mid-turn, mid-cut). No fades, no slides, no plain cuts.

**Hero frame.** The full-bleed final page is the hero frame: strong black, grey and white design, the brief's last words or number huge, a small figure at the foot. It must also be the image a viewer remembers from the opening.

## 7. Sound design

This world has no score. Manga is silent; the reader hears paper, pen, and the imaginary thunder of the lettering. So the soundtrack is exactly that: close-range desk sounds and huge drawn impacts. No melody, arpeggio, pad or EDM riser. Its musical shape is one idea: a clock in the first shot ticks the pulse (14 frames) that later drives the whole film, and every struck object is tuned to one open stack, D, A, E, G, C. As items and groups arrive, the film becomes a chord.

Use one `buildGraph(ctx)`. Noise buffers (white, pink, brown) come from the seeded generator. Reverbs are seeded decaying-noise impulse responses: 0.25 s room, 1.6 s hall. Render the mix in `OfflineAudioContext` during `ready`; Play uses that same buffer, and the picture clock is `audioCtx.currentTime`. Start every noise burst a quarter sample after a sample boundary.

**Kit:**
- **Nib:** white noise, bandpass 3.4 kHz Q 2.5, amplitude from a seeded irregular 6 to 9 Hz envelope, 5 ms attacks. Lasts exactly as long as the stroke on screen.
- **Paper slap:** noise, bandpass 1.2 kHz Q 0.8, 60 ms decay, plus 90 Hz sine thump, 70 ms.
- **Page flip:** noise, bandpass sweep 600 Hz to 3.5 kHz over 180 ms, crackle impulses at 150/s, ending in a paper slap.
- **Blade:** highpassed noise sweeping 6 to 2 kHz in 90 ms, plus a 7.1 kHz sine ping, 60 ms.
- **Wood:** sine f plus 2.7f at -9 dB, 40 ms decay, 2 ms noise click.
- **Metal:** partials at 1, 2, 2.76, 3.76, 5.4 times f, higher ones decaying faster, 0.4 to 1.2 s.
- **Ratchet:** wood clicks at 30 Hz, pitch-jittered.
- **Bubbles:** 20 to 40 ms sine blips rising 300 to 900 Hz at seeded times, lowpassed.

**Rules:**
- Sound lands on contact, never at the start of a motion: on the frame a panel edge finishes cutting, a figure's foot lands, a number's last stroke appears. With the 12 fps drawing grid, round sound times to the same drawn frame.
- **Burden:** mono, close, small room. Nib, quiet clock tick on each beat (wood, 2.2 kHz), each landing weight a paper slap plus a low thump growing heavier (sine 70 to 42 Hz, 350 ms). Room tone at -52 dB.
- **Before the big impact:** cut everything for 5 to 7 frames except a 5.2 kHz sine at -56 dB. That is シーン. It must be real silence, and it is the only silence in the film.
- **Big impact (ドン):** sine 110 to 38 Hz in 120 ms, decaying over 0.9 s; membrane of sine 180 to 96 Hz plus triangle at 1.59 ratio, 250 ms; 4 ms click; paper slap; large hall send. Stereo opens from mono to wide on the first one.
- **Rumble (ゴゴゴ):** brown noise lowpassed at 160 Hz with 11 Hz tremolo, depth 0.6, plus saws at 41 and 41.7 Hz through lowpass 220 Hz and soft saturation; stops dead on the next cut.
- **Each item:** blade plus a 90 Hz panel thump (80 ms), then the sound of the object drawn in that panel, made from the kit (wood knock, metal partials, paper, ratchet, nib, bubbles), tuned to its group's note. Groups take the notes of the stack in order and cycle when there are more than five. Pan each item to its panel's x position (±0.6).
- **Many at once:** when everything runs together, every voice plays on a sparse 16-step pattern, wide stereo, highpassed at 300 Hz and 6 dB down, so many small sounds become a shimmering machine rather than mud. The heavy lows are gone. The clock sits in tune inside the texture.
- **Ending:** riffle of accelerating page flicks; a final ドン on the hero frame with bowl and bells on D, A, E ringing through the hold; half a second later, one quiet pen-cap click.
- **Density:** 5 to 15 audible events per second; at most 3 foreground sounds at once; repeated ticks at most 12 per second and they skip 30 ms before to 90 ms after any landing.

**Mix:** duck the bed 8 dB for 200 ms on each impact by scheduled automation. Effects stay in front, each one nameable by ear. Master: gentle compressor (threshold -14 dB, ratio 3), `tanh` soft clip, static gain to meet the loudness and peak targets.

## 8. Density, the film to avoid, and self-check

The predictable film: a neat even grid of straight rectangles, soft heads built from circles, emoji-like icons in rounded cards, grey fills under a uniform dot overlay, katakana typed flat over the art, panels easing in and fading out, a slow zoom on a still, a synth loop with whooshes. Every part of that fails.

Instead, each panel has three depths: foreground object or figure, subject, and a real background in ruled perspective (shelves, blinds, rooftops, hatched walls, drifting paper). Add cables, stacked papers, ink spatter in the margins, sheets crossing gutters. Hands have knuckles and fingers. The two house animals from the house animals brief live in the margins and backgrounds, inked with the same pen line and tone. Each frame must read as a strong black, grey and white design at thumbnail size and reward inspection at full size. The frames at 50% and 80% of the duration are where the film proves itself.

On-screen text is only what the brief asks for, plus the drawn sound effects. No existing character, brand, logo or company may appear or be recognizable.

**Before delivering, check:**

- Any single frame reads as a printed manga page with no caption: ink, tone dots, slanted panels.
- No color, no grey fill, no fade, no `shadowBlur`, no typed sound effect anywhere.
- Every step of the brief has something the ink or paper does, not only a caption.
- Every item of every list is a different drawn object with its own sound.
- Every transition is a page turn, blade, ink drain or thread, with the swap hidden mid-gesture.
- Exactly one biggest impact; the final page holds at least one second.
- Each sound lands on the drawn frame of contact; nothing plays on top of the シーン silence.
- Text sizes on 1920x1080: titles at least 66 px, essential labels 42 px, key numbers 96 px.

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
