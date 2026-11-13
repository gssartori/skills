---
name: gs-gibi-da-rua
description: Animated film in the Gibi da Rua style. Turns any subject into one finished 10 to 16 second animated film, a single HTML file with sound. Use when the user asks for an animated video, explainer or short in this style.
---

# Gibi da Rua

Vídeo de gibi infantil brasileiro: a turma da rua, a banda de latas e a capivara na porta da padaria.

Preview and details: https://gsartori.com/skills/gibi-da-rua

## How to use

1. If the user has not said what the film is about, ask once for the subject, the main character, the steps or items to show, any numbers and the closing line. Then go.
2. Follow the prompt below as your instructions. Put the user's subject in its "## Content" section and keep every other section exactly as written.
3. Deliver one self-contained `film.html` that plays in any browser, with sound. It exposes `window.film`, so it can also be captured frame by frame into an MP4.

## Prompt

# Gibi da Rua

Build one finished animated film: a sunny Brazilian neighborhood street, painted like the deluxe cover of a newsstand children's comic and animated like a beloved TV special. Whatever story the content brief tells, it happens on this street, acted by a gang of neighborhood kids and played by a street band made of cans. The story and technical delivery follow this text.

## The film you must not make

The predictable version: flat vector kids with dot eyes on a pale background, emoji icons in a neat grid, page-flip transitions, halftone dots, an American "POW!" starburst, a ukulele loop with hits on top. All of that fails. So do plain circles with faces, empty sky, repeated houses, and a camera sliding across static cards. This film is warm, funny, crowded with real drawing, and looks painted by someone who loves these kids.

## Style bible

**Tradition.** The Brazilian children's comic: a gang of neighborhood kids, childhood played out on the street. Our target is its top shelf, the painted cover and animated special, not the cheap flat page. Same simple drawing, far richer finish.

**Line.** Thin, even, clean, confident. One constant width, round caps and joins, every shape closed. Characters and what they touch: ink `#1E1A24`, 3.5px on a kid 300px tall. Background objects: 2px tinted `#6B5A6E`. Distance: no line, only paint. That split separates figures from scene. No taper, hatching, spot blacks or sketchiness.

**Proportions (H = total height, kid H = 300px).** About 2.1 heads tall. Head 0.52H wide, 0.46H tall, cheeks fullest below the midline, small soft chin. No neck. Torso a soft bell, 0.26H at shoulders, 0.34H at hem, 0.28H tall. Legs short tubes, 0.18H. Big rounded shoes, 0.16H long. Arms soft elbowless tubes, 0.30H, ending in a stubby hand 0.09H across: three sausage fingers and a thumb.

**Faces.** Extremely simple; all the charm lives here. Eyes: two solid ink vertical ovals, 14x23px, close together (centers 38px apart), 52% down the head, each with one tiny white catch-light. Nose: a tiny 10px curved tick below the eye line. Mouth at 70%: a thin curve at rest, opening to a wide D with soft red interior and tongue when happy. Brows: short floating arcs. Ears: half-discs on the eye line. Soft rose blush under each outer eye. Turn the head by sliding all features together, up to 12% of head width. No realistic lips, nostrils or anime eyes.

**Expressions.** Happy, worried (raised brows, wavy mouth), straining (eyes shut as arcs), shocked (white ovals with tiny pupils, O mouth), dizzy (circling stars), calm (eyes closed as upward arcs). Cartoon symbols belong here: flying sweat drops, short curved shock lines, stars, hearts, round dust puffs.

**Hair and clothes.** Hair is one solid painted mass with two or three soft highlight strokes, never strands. Clothes are simple shapes with one or two honest details.

**Color.** Cheerful and clear, never neon or gray. Sky `#4FB3E8` to `#8FD6F2` to cream `#FFF1C9` at the horizon. Walls `#F9D9A0`, `#F6B8A8`, `#A9DFD8`, `#F3E6D0`, `#C7E3A6`. Roof tile `#C9623F`. Cobbles `#B9AFA6`. Foliage `#3E9E56` to `#8FD05E`. Skins `#FFD9B8`, `#F2BE8C`, `#C98A5B`, `#8A5636`. Shadows shift toward violet, lights toward warm cream, never black.

**Painted shading.** Every form has volume: airbrush-soft gradient with warm light from upper left, cool shadow lower right, warm bounce from the pavement along the bottom edge, one crisp cast shadow under hair, chin and arms, and a contact shadow on the ground. Soft inside the line, crisp at the line.

**The street.** One long, specific, loved place: cobbles, a black-and-white patterned Portuguese-style sidewalk, low pale stucco houses with tile roofs, iron gates, potted plants, blue water tanks on roofs, utility poles with a tangle of wires and a paper kite caught in them, a big mango tree, a yellow ipê in bloom, a small bakery, a newsstand with comics hanging on strings by clothespins, a popsicle cart, laundry, chalk hopscotch, two flip-flops as a goal. Signs say only generic words like PADARIA and BANCA. The two house animals described in the house animals brief are the recurring comedians: the capybara sits by the bakery door, the sloth hangs from the tangle of utility wires. Every house is individually composed.

**Lettering.** Google Fonts: `Titan One` for sound effects, `Patrick Hand` for captions. Balloons are big, rounded, white, with a soft tail. Captions are cream rounded boxes. Sound effects are fat, cute Portuguese words, each letter rotated a few degrees: `CATAPLOFT!`, `FLUPT!`, `POF!`, `TOIN!`, `TOC!`, `PLIM!`.

**What breaks the style.** Halftone dots, superhero anatomy, manga speed effects, sharp angles, realistic hands, neon glow, vector gloss, thick sticker outlines, empty white space.

**Originality.** No child wears a plain red or plain yellow dress. No oversized front teeth, stuffed toys, straw hats, green hair, lab coats, blue pets or speech quirks. No real logo or brand.

## Technique recipes

**1. Painted volume on a clean line.** Build every part as a `Path2D`, paint inside a clip, then stroke once.

```js
function paint(g, path, b, ramp) {
  g.save(); g.clip(path);
  const r = g.createRadialGradient(b.x+b.w*.3, b.y+b.h*.24, b.w*.08,
                                   b.x+b.w*.46, b.y+b.h*.46, b.w*.92);
  r.addColorStop(0, ramp.light); r.addColorStop(.5, ramp.base); r.addColorStop(1, ramp.shade);
  g.fillStyle = r; g.fillRect(b.x, b.y, b.w, b.h);
  // then: linear warm bounce on the bottom 28%, rgba(255,190,120,.28) fading upward
  g.restore();
}
```

Make `ramp(hex)` in HSL: shade moves hue toward 265, lightness down 16, saturation up 6; light moves hue toward 50, lightness up 12. Cast shadows are crisp shapes in `rgba(90,74,154,.24)` inside the clip.

**2. Even line under squash.** Never stroke inside a scaled transform:

```js
const p = new Path2D(); p.addPath(shape, new DOMMatrix().translate(x,y).rotate(a).scale(sx,sy));
g.lineWidth = LINE; g.lineJoin = g.lineCap = 'round'; g.strokeStyle = INK; g.stroke(p);
```

**3. Gouache background.** Pre-render the street as a long offscreen strip. Lay each big area with 200 to 400 seeded overlapping strokes: long soft bands at 12% alpha, following the form. Paint foliage as hundreds of leaf dabs, shade side first, sun side last. Multiply a seeded 512px paper tooth tile. Render the street twice, high white noon and golden late afternoon with long violet shadows, and crossfade them from 8.5s to 11s. Use three parallax depths: far tree tops, houses, foreground props sliding past the lens.

**4. The giant N.** A fat, heavy, padded painted letter with rounded corners, not a font. Draw its outline by hand, 700px tall. Build depth by drawing it 50 times down-right in a deep tone, then paint the face tomato to orange, with a cream highlight on upper edges, a band of stitching, and a ribbon bow around its diagonal. Its strokes hinge and unfold like a carpenter's folding rule, each segment shadowing the next.

**5. Sound effect words.** Pre-render: a scalloped cloud (arcs around an ellipse), then letters in three passes: `strokeText` ink at 26px offset down-right, `strokeText` white at 14px, `fillText` with a vertical gradient. Animate per letter with a stagger.

## Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style, and never add a caption the brief did not ask for.

## Cast construction

The style does not know who is in the story. It says how anyone the brief describes becomes a character of this street.

- **Kids** share the head construction above. Each must be identifiable by silhouette alone: change one strong attribute per kid (hair mass, a big prop, a garment shape) and give each one a color from the palette for clothes, ribbon and frames. Mix skin tones from the palette across the gang.
- **Grown-ups** are built in kid logic: about 400px tall, 2.7 heads, head 165 wide and 150 tall, broader shoulders, longer legs, the same simple eyes. Whatever the brief says about a grown-up (age, hair, beard, glasses, clothes) becomes painted masses and honest details; a beard is a painted mass along the jaw, one step lighter than the hair, with a softly scalloped edge.
- When the brief names roles, groups or jobs, the kid wears a cardboard sign on a string with that word, in `Patrick Hand`, and carries one prop that says the job without the sign.
- Every character keeps the same marks from first frame to last.
- **Originality.** No plain red or plain yellow dress, no oversized front teeth, stuffed toys, straw hats, green hair, lab coats, blue pets or speech quirks.

## Story grammar

**Steps.** Map the brief's sequence onto the street. Each step is a place on the street (a house, the bakery, the newsstand, the corner, the mango tree) and a gag that physically causes the next step. If a step would only get a caption, find what the street does: something falls, rolls, is kicked, is tied, opens.

**The relay object.** One physical object carries the story from step to step and drives the camera: a football by default, or a kite, a popsicle cart, a paper boat in the gutter, if the brief suggests one. It is passed on in a personal way by each character. Its kite line can thread things together as it passes.

**A list of N things.** Never assume N. Each item is a printed comic panel: white paper edge, 5px color frame, hand-ruled ink border, hung by a wooden clothespin on a line. Inside, a point of view: two stubby hands with color cuffs enter from the bottom and do one job on a small painted scene. Author each at 300x225 with at least eight painted shapes and a silhouette unlike its neighbors. Cache `base(g)` offscreen once, then draw `live(g, phase)` every frame: one looping action, in the middle third, readable at 140px wide.

- N up to 8: panels are pulled out one by one like a fan, one per 16th note.
- N from 9 to 30: group them on clotheslines between houses, up to 6 per line, one line per group or per step; the relay object passes each line and its panels spring open.
- N above 30: the first 6 to 8 at full size, the rest as a long streaming bunting that fills the sky.
- Every panel enters, lives and leaves the same way. Variety comes from the painted scene and its sound. Two panels that could be swapped without anyone noticing have failed.

**Gathering.** When the brief brings everything together, the clotheslines and bunting arc around the main figure in half-ellipse rings, each group owning a wedge with its kid sitting in it, kite lines running from the main figure to the kids and out to their panels. Panels at 140px wide, swinging, never overlapping.

**Numbers and short words.** A number or short word the brief puts on screen is a big painted, padded object of the street's material, built from things on the street if possible (footballs, crates, laundry), and it lands with squash, rebound and wobble.

**Climax and ending.** Exactly one impact is the biggest in the film, and it is the moment the brief's key image lands. Before it, a breque: the band stops dead and everyone freezes on the beat, holding their breath; only the capybara keeps chewing. The last image is a painted cover: the brief's last words or number largest in frame, readable at thumbnail size, characters landed around it, held at least one second with only a blink, the capybara chewing, the sloth's slow head turn and a drifting kite.

**Pacing by duration.** Hook within the first 2 s. Something changes every 1 to 2 s. At about 10 s use 3 places and 2 relay passes between them; at 13 to 15 s use 4 places. Write a beat table before drawing: one row per beat with start, end, exact on-screen text, the physical cause that moves us there, and the main sounds. Picture and sound both read times from that table, on the 120 BPM grid below.

**Transitions.** Each thing physically causes the next, like a good gag: a kick, a fall, a tug on a ribbon, a ball bonking a head, a whip of the camera following the relay object. Never use a page flip, wipe or dissolve to change idea.

## Animation language

- Characters animate on twos: quantize their pose time to 15fps. Camera, particles and panels stay at 30.
- Squash and stretch preserves volume (`sx*sy = 1`). Anticipation of 3 to 5 frames before big moves, overshoot and settle after, fast moves in 2 to 3 frames with a one-frame smear. Hair, cape, braid, signs and ties follow through late.
- Bounces are round, each lower and quicker. Motion lines are short and curved.
- Each kid has an idle: hop, blink, look at the next kid. Nobody is ever a frozen sprite.
- At every moment at least five independent things move: wires, kite tail, laundry, leaves, clouds, dust, panels, the sloth swaying on the wires. Plant gags: a popsicle falls onto the capybara's head and it only blinks, the sloth reaches for the kite after it has gone, a sign flips around, a prop gets dizzy.

## Sound

No synth score. This is a hot quiet street that fills with people, and the sound tells the story by itself: one footstep alone becomes a full street band. The music is a samba batucada on instruments and cans, 2/4 at 120 BPM: bar 1.0s, 16th 0.125s. Every event sits on that grid. Each sound lands on the drawn frame of contact (foot down, ball on head, stamp on paper), quantized to the same 15fps pose grid.

**Helpers.** `thump(t,f0,f1,dur,lvl)`: sine with exponential pitch drop. `nz(t,kind,filter,f,Q,a,d,lvl)`: seeded white, pink or brown noise. `tone(t,wave,f0,f1,a,d,lvl)`. `bell(t,f,ratios,d,lvl)`: inharmonic sines. Levels in dB. Do not attempt speech or a choir: they sound uncanny.

**Street bed.** Cicadas: white noise through bandpass 5200Hz Q9 and 7100Hz Q7, amplitude-modulated at 38Hz with a 1.6s swell, -28dB. Sparse sparrow chirps. Slap off the houses: 90ms delay, lowpass 2500Hz, -16dB.

**Weight and burden.** Footsteps `thump(70→45Hz, 0.16s, -8)` with brown noise lowpass 400Hz and a flip-flop slap (white, bandpass 1800Hz, 25ms, -16). A swaying load creaks: sawtooth 110 to 170Hz with seeded wobble, bandpass 900Hz Q6, 250ms, -18, then 3 to 5 rattle ticks. Effort grunt: saw 130→95Hz through formants 500 and 1400Hz, 180ms. Sweat drop: sine 1400→2600Hz, 50ms, -24.

**Something falls.** Slide whistle down: sine 1800→180Hz, 6Hz vibrato, breath noise, -24 to -10; cut everything to silence 0.12s before the landing.

**Big landing.** `thump(58→28Hz, 0.9s, -3)`, brown noise lowpass 180Hz 0.7s, white highpass 1200Hz 40ms, wood modes 143 and 311Hz, 30 seeded debris ticks, a 0.55s wobble (sine 210Hz with 12Hz pitch swing of ±30Hz), glass tinkle of 5 sines 3 to 7kHz, the sloth's wire creaking a beat late. One lone cicada resumes timidly 0.6s later.

**Release and call.** Ribbon rip: bandpass noise 1000→3000Hz chopped at 60→20Hz, 0.2s. Paper pour: pink noise bandpass sweeping 500→2500Hz, paper flutter at 18 to 30Hz, stereo wide. The panpipe call of the Brazilian street knife-sharpener (12 quick notes up a major scale from G5 and half back down, triangle plus breath, 60ms each) calls everyone outdoors.

**The band builds one voice per character or group, in order of appearance.** The relay object's kicks are a muted surdo on every beat, so nothing is ever empty. Assign instruments in this order and cycle if there are more than eight:

1. Samba whistle: 2900Hz trilled at 45Hz, three blasts.
2. Coins in a can: 16ths of white highpass 5000Hz, 35ms, accent every 4th.
3. Cuíca: triangle plus noise through bandpass, pitch 380→720→420Hz, 120ms, in laughing hiccups.
4. Two tin cans as agogô: 830 and 1110Hz, ratios 1, 2.76, 5.4, 140ms.
5. Open surdo on beat 2 at 52Hz, the pitch of the first footstep.
6. Pandeiro: thumb 200Hz on 1, jingles bandpass 7000Hz, 40ms, on other 16ths.
7. Cavaquinho: Karplus-Strong in pure JS, tuned D4 G4 B4 D5, quick 16th strums, one chord per bar (E7, Am, D7, G).
8. Tamborim on wood: 700Hz click, 30ms, on steps 0 2 4 5 7 9 11 13 14 of a 16-step cycle.

**Item foley.** Inside each panel's moment, up to three tuned hits on 16ths, 5dB above the band, made from the helpers to match the painted action: woodblock `toc` at 900Hz, coin drop, beeps at 1800Hz, key ticks, shutter click, gear ratchet, rising hiss, bulb horn (saw 330→300Hz, bandpass 1200Hz), belt rattle, pen tick, phone ring (20Hz gated 1400 and 1700Hz), clap, brass bell, box pop, double heartbeat thump, chime, gavel at 200Hz wood, stamp thud, padlock click. Pan each to its panel.

**Everything together.** The whole band with a fife on top: triangle, breath, 6Hz vibrato, on steps 0 2 3 5 6 of each bar (A5 C6 E6 D6 C6, then F#5 A5 C6 B5 A5). Cicadas fade, evening crickets appear softly.

**Breque and end.** The band stops dead; silence except one small cuíca squeak as the joke. Then `PLIM`: bell at 3100Hz, ratios 1, 2.4, 3.9, and the full band hits one G chord with surdo, whistle, fife rising to G6 and a let-ring strum. Letter landings follow on 16ths. It rings out to crickets, and a three-note great kiskadee call (sines near 2200, 2600, 1900Hz) closes the film.

**Density.** 5 to 15 audible events per second; at most 3 foreground sounds at once besides the band; repeated ticks at most 12 per second.

**Mix.** Buses for street, foley, band and fife, panned to screen position (±0.6). Duck the band 4dB around foley hits by scheduled gain. Effects always read above music. Master with a gentle `DynamicsCompressor` and a hard-knee final stage. In `renderAudio`, measure K-weighted gated loudness, set gain to reach -16 LUFS, confirm peaks below -1 dBFS, and play the film from that same buffer so sound and picture share one clock.

## Final check

Never ship a stub or "similar for the rest": every item, character and place the brief asks for must exist, each drawn. A long file is expected. Then inspect the frames at 10%, 25%, 50%, 75% and 95% of the duration:

- Could this frame be a painted comic cover, with volume, paper tooth and a full scene?
- Is every kid distinct by silhouette, and every recurring character the same character?
- When everything is together, are all items visible, separate and alive?
- Does every step of the brief have something the street does, not only a caption?
- Is there exactly one biggest landing, and does the last image hold at least one second?
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
