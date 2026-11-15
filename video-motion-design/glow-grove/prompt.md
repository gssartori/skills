# Glow Grove

Build one finished animated film set in a tabletop miniature: a patch of mossy forest floor at dusk, shot like a stop-motion set through a macro lens, lit by mushrooms whose gills glow like lamps. Whatever the content brief tells is acted by soft clay-and-felt mushroom critters who pop out of the moss, hop, wiggle and puff glowing spores. The story and technical delivery follow this text.

## The film you must not make

The predictable version: flat green ground, mushrooms made of a sphere on a cylinder, red caps with white dots, a dark night lit only by neon glow, critters sliding instead of hopping, bloom smeared over everything, a music-box loop. All of that fails. This film looks like a handmade miniature set, warm and clearly lit, where every critter has weight, contact and a readable face.

## 1. Identity

**Contract.** A real-looking miniature built from clay, felt, moss and bark, rendered in Canvas 2D with light computed per pixel once and composed every frame. Dusk, never night: a lilac sky fading to apricot at the horizon, a warm low key light from behind left, and glowing mushroom lamps that pool light on the moss.

**Three signatures that any still frame must show:**

1. Mushrooms built like real mushrooms: a lathe-shaped cap with a rolled margin, radial gills underneath glowing brightest at the rim, a ring on the stem and a bulbous base sunk in moss.
2. Critters of soft matte clay with a felt sheen: a cap, a stem body with a little belly, stubby arms, tiny feet, two glossy eyes with white catchlights and blush cheeks.
3. Glowing spores, apricot and mint, drifting on slow curling paths through the whole frame.

**Three exclusions:** never a dark or near-black frame; never red caps with white spots; never a critter floating without a contact shadow.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the set, never a stretch.

## 3. Material primitives

Build every primitive once, before `ready`, into offscreen canvases. Per frame, only compose, transform and add light.

- **Lit clay sprite.** Every rounded part (cap, body, arm, foot, cheek, pebble, moss mound) is authored as a height field on an offscreen canvas: an analytic dome, capsule or lathe profile. From the height field compute a normal per pixel, then shade once: Lambert from the key light direction (behind left, elevation 25 degrees), a cool fill from front right at 35%, a rim term `pow(1 - n.z, 3)` tinted by the key color, and a soft sheen `pow(1 - n.z, 1.5) * 0.25` in cream for felt. Add seeded fingerprint-scale noise (amplitude 3% on the height) so the clay looks handled, never perfectly smooth. Bake the result with its alpha; this is the sprite.
- **Glow.** Gills, cap rims, freckles and spores glow. Draw them in a separate pass with `globalCompositeOperation = 'lighter'`: the glowing shape at full color, plus one pre-rendered soft halo sprite (radial falloff, quadratic) at 18 to 30% of the shape's brightness, 3 to 4 times its size. Only glowing things get halos. Nothing else blooms.
- **Pooled light.** Each lamp lights the moss and critters near it: before the glow pass, draw a large radial pool sprite in the lamp color with `lighter` at 10 to 22%, clipped to the ground and to the near side of each critter. A critter standing next to a lamp is visibly tinted on that side.
- **Moss.** A displaced ground of mounds (seeded value noise, 3 octaves) covered with 6,000 to 9,000 tiny tufts, each a cluster of 3 to 5 tapered strokes, darker at the root and lighter at the tip. Bake the ground once into 3 depth layers (far, mid, near) for parallax; the near layer has the largest tufts and a soft out-of-focus edge made by drawing it at 50% size and scaling up.
- **Set dressing.** Fallen leaves (bent shapes with a midrib and serrated edge, russet and ochre), pebbles, a fallen birch log (white bark with black lenticels, a broken end showing growth rings, a shelf of moss), a curled fern frond (a spiral spine with 20 to 26 pairs of leaflets), all baked once.
- **Backdrop.** The sky gradient (lilac `#B9A6D6` at the top, rose `#E7B3C0`, apricot `#F6C9A0` at the horizon) with soft lavender-grey tree silhouettes (`#7B6E9A`, hazed to 40%), already soft by construction.
- **Contact shadow.** Under every critter and object on the ground, a soft ellipse in moss shade `#3E6640` at 45%, 90% of its footprint wide; it shrinks and fades with height during hops.
- **Lettering.** Google Fonts: `Gluten` (600) for titles and big words, `Quicksand` (700) for captions and labels. Light text in warm cream `#FFF7EC` with a soft plum shadow (`rgba(74,50,96,.45)`, blur 18 px, offset 4 px down), or plum text `#4A3260` on a cream felt tag with stitched edges. Minimums at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px.
- **Palette.** Moss `#6E9A4E`, tips `#A9CF6A`, shade `#3E6640`; soil `#7A5440`; leaves `#C2653A`, `#D9A44A`; fern `#5E8C4A`; birch `#EDE6DA`, lenticels `#3A3330`; lamps apricot `#FFB070` with gills `#FFE0A8`, mint `#8FF0C8` with gills `#DFFFF0`; critter caps cream `#F2E3C8`, butter `#F5D27A`, lilac-grey `#B8A9C9`, cinnamon `#B5713F`, sage `#A7C49A`, rose `#E8A5A0`, slate `#8E9BB5`, ochre `#D9A44A`; bodies `#F3E9D6`; blush `#F2A08C`; eyes `#2A1E24`; spores `#FFD39A`, `#BFF7DE`.
- **Finish.** A very light film grain (seeded, 2% amplitude) re-drawn 12 times per second, and a warm vignette at 12% in the corners. Never darker than that.

## 4. Material time

The miniature is lit and smooth (30 fps), but critters animate on twos like stop-motion puppets: quantize critter pose time to 15 fps, while spores, lamp breathing, light and camera stay at 30. Lamps breathe ±12% on their own 2 to 3 s sine. Every critter blinks (eyelids closed 0.12 s) at most once every 2 s. Ambient spores (80 to 140) drift from the first frame on seeded closed-form curl paths, rising 20 to 40 px per second.

## 5. Piece vocabulary

Turn any noun of the brief into one of these.

- **Critter.** See Cast construction. Enters by popping up out of the moss.
- **Lamp mushroom.** The grove's light source and its natural "central object": a hero lamp (cap radius about 0.18 of frame height) at the back and smaller lamps in clusters. Its changing part is the glow: it brightens 15 to 25% when the story succeeds, flickers when it fails, and new gills light up in a sweep around the cap when something is gained.
- **Item token.** A small glowing button cap (40 to 90 px) with one pictogram pressed into its top as a darker clay relief, so it reads by silhouette: an arrow, a coin, a gear, a letter, a heart, a chart, a key, a bell. Any noun becomes a token by its most recognizable silhouette.
- **Arrow or link.** A trail of spores flowing along a curve, or a thin root of clay that grows along the moss; the head is a glowing bead that lands last.
- **Label.** A cream felt tag with stitched edges, hung from a critter or token by a thread, plum `Quicksand` text. Always drawn in a last pass, on top of everything.
- **Counter.** Digits shaped from clay coils standing on the moss, re-rolled for each change: the old digit squashes down into the moss and the new one pops up, at most 12 changes per second, settling with a spring.
- **Error mark.** The lamp nearest the problem flickers (3 dips in 0.5 s, never more than 3 per second), the critter droops (cap tilts 15 degrees, arms down) and a single grey puff of dull spores sinks. **Success mark:** the lamp swells and a ring of fresh mint gills lights around its cap, the critter hops and puffs bright spores.
- **Emphasis.** A slow halo of spores that circles the key element once in 0.8 s.

## 6. Story grammar

### Cast construction

The style does not know who is in the story. It says how anyone the brief describes becomes a critter of this grove.

- **A critter, 0.16 to 0.32 of frame height.** A cap of its own shape (low dome, wide flat parasol with raised scales, tall conical bell, round bun, puffball sphere with tiny warts and no separate cap), with a thin ring of gills visible underneath when it has a cap. A body that is the stem: a capsule with a little belly. Two stubby clay arms with rounded hands, two tiny feet peeking out at the base. A face just under the cap rim: two glossy eye domes with a white catchlight and a slight lid curve, blush cheeks, a small mouth that opens to an O to puff.
- **What the brief says about a person** becomes clay and felt on a critter: hair as the cap's color and texture, a beard as a soft felt tuft under the face one step lighter than the cap, glasses as two thin wire rings, age as size and posture, a job as one small prop held in the hands or a felt tag. A main character is the tallest critter, about 0.32 of frame height.
- **Scale.** In main scenes the critter in focus is at least one third of frame height with a face of at least 50 px. With more than 4 critters, show 2 to 4 at a time as the camera passes, and gather everyone only at the reunion moment, where no face is under 24 px; whatever does not fit becomes a group with one large representative.
- **Several critters:** each distinct by cap shape and cap color from the palette, never by a caption alone. Every critter keeps the same cap, colors and marks from first frame to last.
- **Motion vocabulary.** Pop-up: starts as a bump in the moss, springs up (damping 0.45, 12% overshoot, about 0.6 s); the tufts around the hole bend outward and settle; 10 to 14 soil crumbs hop out on short arcs. Wiggle: a shimmy of ±10 degrees at 3 Hz for 0.5 s with the cap lagging 0.08 s. Puff: squash to 0.85 tall and 1.1 wide for 0.12 s, stretch, mouth opens, 30 to 40 spores burst from under the cap and rise. Hop: a parabola of 0.08 of frame height in 0.35 s, landing with a 0.85 squash. Look: eyes and head turn toward whoever acts.
- **Originality.** No real game or cartoon creature, no red cap with white spots, no teeth, no horror eyes.

### A list of N things

Never assume N. Items become item tokens.

- **N up to 8:** each token pops up out of the moss one by one, every 0.15 to 0.25 s, in an arc in front of the critter that owns them, each with its own tuned sound.
- **N from 9 to 30:** tokens are grouped. Each group grows as a fairy ring of small glowing caps around the critter that owns it (one ring per critter, tokens spaced evenly, inner ring then outer ring when a group passes 8). Rings light up token by token in a sweep, 0.06 to 0.1 s apart.
- **N above 30:** the first group is shown close; the rest light up as a carpet of small glowing caps across the whole grove floor, receding into the far layer, with the counter giving the total. Only the first tokens carry labels.
- Every token enters, glows and pulses the same way. Variety comes from the pictogram and its sound. Two tokens that could be swapped without anyone noticing have failed.

### Steps

Each step of the brief gets a **verb the grove performs** (something pops up, is carried on a cap, rolls down the log, is puffed into the air, is lit) and a **place on the set**: the front of the moss, the birch log, under the fern, beneath the hero lamp. Group two steps per place when they share one. Something always continues from one step to the next: a token carried on a critter's cap, a spore trail, a critter hopping across.

### Cause, error and fix

Cause travels as a spore trail or a rolling token. If the brief has an obstacle or a mistake, use the error mark, show the dull puff travelling back along the trail to the lamp or critter that must change, show the physical fix (a critter turns its cap, nudges a token into place, puffs on a lamp), then the success mark.

### Numbers and short words

A number or short word the brief puts on screen is built from fat clay coils in cream or butter with a glowing apricot edge, standing on the moss at least 96 px tall (140 px or more when it is the key image), popping up with the spring.

### Climax and ending

Exactly one moment is the biggest in the film: the brief's key image. Before it, 0.3 s of hush: critters freeze mid-pose and the music stops. At the moment, every critter puffs at once, a cloud of 250 to 350 spores spirals up around the key image, and every lamp brightens 20% over 0.6 s and stays there. The last image is a complete composition: the brief's last words or number largest in frame, readable at thumbnail size, the critters gathered in a semicircle around the hero lamp, spores hanging in the air, held at least 1.2 s with only breathing lamps, drifting spores and blinks.

### Pacing by duration

Hook within the first 1.5 s: the grove is already lit and something is moving in the moss. Something changes every 1 to 2 s. About 10 s: 3 places on the set. 13 to 16 s: 4 places. Before drawing, write a beat table: one row per beat with start and end time, the exact on-screen text, the physical cause that moves us to the next beat, and the main sounds. Picture and sound both read times from that table.

## 7. Transitions

Every change of place is an event of this miniature, 0.4 to 0.8 s long, and the swap happens while the frame is covered.

1. **Spore cloud.** A big puff fills the lens with glowing spores; the camera moves behind it and the cloud thins onto the next place.
2. **Falling leaf.** A large russet leaf tumbles past the lens in the near layer, covering most of the frame for 0.2 s; the view behind it has changed.
3. **Dolly along the set.** The camera glides along the birch log or the moss to the next place, near layer fast, far layer slow.
4. **Rack of light.** The hero lamp swells to fill the frame with warm glow and fades onto the next place.

Never use a dissolve, a page flip, a generic wipe or a hard cut to change idea.

## 8. Camera

A macro view a little above the moss, looking slightly up past the critters to the hero lamp. At most 6 moves in 15 s, eased in and out; zoom in log scale between 0.9 and 1.3, with one pull-back at the gathering that shows the whole grove. A slow drift of 6 to 8 px per second keeps it alive. Three parallax layers (far backdrop at 0.2, mid set at 0.6, near moss and leaves at 1.3) sell depth without 3D. The edge of the set never shows.

## 9. Sound

The sound of a miniature: soft, woody, close-miked, intimate. Picture and sound share one clock; every sound lands on the frame of visible contact (the pop, the landing, the puff), within one frame.

**Helpers.** `pop(t, f0, f1, dur, lvl)`: sine with fast pitch drop. `pluck(t, f, dur, lvl)`: Karplus-Strong in plain JS, soft damping. `nz(t, kind, filter, f, Q, a, d, lvl)`: seeded white, pink or brown noise. `chime(t, f, ratios, d, lvl)`: inharmonic sines. Levels in dB. No speech, no choir.

**Bed.** Dusk crickets: white noise bandpass 4800 Hz Q8 and 6200 Hz Q10, pulsed at 18 Hz in 1.2 s phrases, -30 dB. A distant soft owl, two notes near 380 and 320 Hz, once. A faint breeze of brown noise lowpass 500 Hz at -32 dB.

**Music.** A gentle lullaby groove at 96 BPM: a kalimba (pluck plus a 3.1 ratio partial, short decay) playing a pentatonic figure in D, a soft felt-piano pad (sines through lowpass 1200 Hz), and a brushed shaker on 8ths at -28 dB. It starts with the kalimba alone and gains one voice per scene.

**Vocabulary.**

- Moss bump: brown noise lowpass 250 Hz, 80 ms, -20 dB.
- Pop-up: `pop(180→520 Hz, 90 ms)` plus 10 crumb ticks (white noise bandpass 3000 Hz, 6 ms, seeded spacing over 0.25 s), -12 dB.
- Hop landing: soft clay thud, sine 120→80 Hz, 70 ms, plus a felt dab of pink noise lowpass 900 Hz, -14 dB.
- Wiggle: a rubbery squeak, triangle 600→900→700 Hz through bandpass 1200 Hz, 140 ms, -20 dB.
- Puff: breathy pink noise bandpass 1600 Hz, 0.25 s, followed by a sparkle (6 chime grains 3 to 6 kHz over 0.6 s), -14 dB.
- Token light-up: one kalimba note on a rising pentatonic scale per token, -12 dB.
- Lamp swell: a warm felt-piano chord swelling over 0.6 s, -12 dB.
- Error: a dull low pluck falling a minor third and a sinking breath, -14 dB. Success: three rising kalimba notes and a sparkle, -10 dB.
- Counter digit: a soft clay plop, 40 ms, at most 12 per second; the final lock is a kalimba chord.
- Falling leaf: dry rustle, pink noise bandpass 2500 Hz chopped at 20 Hz, 0.4 s.
- Climax: the music stops 0.3 s before; then all critters' puffs at once, a deep soft boom (sine 60→40 Hz, 0.7 s, -5 dB), a wide sparkle wash, and the full lullaby chord.
- Ending: the kalimba plays the opening figure once more, slower, and rings out under the crickets.

**Density.** 4 to 12 audible events per second; at most 3 foreground sounds at once besides the music and bed; repeated ticks at most 12 per second; the climax is the single loudest moment.

**Mix.** Music ducked 4 dB for 120 ms under each foreground hit by scheduled gain; pan by screen position, `(x / 1920 - 0.5) * 1.2`; a small room reverb (convolver from 0.4 s of seeded decaying noise) on everything except the bed. Loudness and peaks as the technical delivery asks.

## 10. Hero frame

The last frame: the critters in a semicircle around the hero lamp, every lamp at full glow pooling light on the moss, spores hanging in the air, the brief's closing words or number largest in frame in cream clay or glowing letters. It must read as this style with no caption.

## 11. Style check

Never ship a stub or "similar for the rest": every character, item and place the brief asks for must exist, drawn. A long file is expected. Inspect frames at 0%, 10%, 25%, 50%, 75% and 95% of the duration:

- Is the very first frame already lit, colored and showing the grove, with something moving?
- Do the mushrooms show gills, a rolled rim, a ring and a bulbous base, and do only lamps and spores glow?
- Is every critter a mushroom creature with cap, face, arms and feet, lit like clay, with a contact shadow?
- Is every critter distinct by cap shape and color, and does each keep its marks all film?
- Do pop-ups, hops and puffs squash and settle?
- When everything is together, are all tokens visible, separate and glowing, with no empty slot?
- Are the two house animals present as clay figures of this set, readable at their size?
- Is there exactly one biggest moment, and does the last frame hold at least 1.2 s with the closing text the largest element?
- Text at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px, never smaller, always on a calm area or a felt tag.

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
