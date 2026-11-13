---
name: gs-four-color-heroes
description: Animated film in the Four-Color Heroes style. Turns any subject into one finished 10 to 16 second animated film, a single HTML file with sound. Use when the user asks for an animated video, explainer or short in this style.
---

# Four-Color Heroes

Vídeo de gibi de super-herói clássico: retícula, quatro cores e uma capa no final.

Preview and details: https://gsartori.com/skills/four-color-heroes

## How to use

1. If the user has not said what the film is about, ask once for the subject, the main character, the steps or items to show, any numbers and the closing line. Then go.
2. Follow the prompt below as your instructions. Put the user's subject in its "## Content" section and keep every other section exactly as written.
3. Deliver one self-contained `film.html` that plays in any browser, with sound. It exposes `window.film`, so it can also be captured frame by frame into an MP4.

## Prompt

# Four-Color Heroes

Build an animated film that looks like a mid-1970s American newsstand superhero comic book come alive: brush-inked, hand-lettered, hand-separated into flat colors, letterpress-printed on cheap newsprint. Stay in that one era: nothing computer-colored, nothing from gallery Pop Art. All characters and costumes are original. Whatever story the content brief tells, it is told as an issue of this comic. The story and technical delivery follow this text; obey them exactly.

## The idea that organizes everything

The whole film happens on **one giant printed sheet** of comic pages laid edge to edge, 1920x1080 art pixels per page. The main figure of the story owns the center page; every other character or group the brief names owns a page around it (a 3x3 sheet holds a center and eight; use 2x2, 3x2 or 3x3 to fit the story, and leave unused pages as printed ads and letters columns). Each page is a classic **six-panel grid (3 across, 2 down)**, so every list item in the story is literally a comic panel. The camera never leaves this sheet, and every transition is something that physically happens on it.

## Style bible

**Line.** Drawn with a loaded sable brush and flexible nib, never a uniform stroke. Three weights: contour 7-10px, swelling and tapering; interior form 2-4px; texture hairlines 1-1.5px. Heavier on the shadow side. Lines overshoot at corners. Nothing inked is a perfect circle.

**Inks.** Black does the modelling, not color. One hard light from upper left. Spot big solid black shapes: under the chin and pectoral shelf, inner thigh, shadow side of every limb, underside of every machine and building. Where black meets color it breaks into **feathering**, combs of tapered spikes following the form. Crosshatch only on backgrounds, metal, cast shadows. Costume folds only at elbows, knees, armpits, waist. Hair and black materials get pale blue highlight shapes (C25 or C50) inside the black.

**Color.** No gradients, ever. The process limit is real: cyan, magenta, yellow, each at 0, 25, 50 or 100 percent, 64 combinations. Name colors by plates: red M100 Y100, hero blue C100 M50, night blue C100 M100, green C100 Y100, gold Y100 M25, orange Y100 M50, purple C50 M100, flesh M25 Y25, deep skin C25 M50 Y50, brown C25 M50 Y100, steel C25 M25. Backgrounds often drop to one wild flat behind an action figure. Unprinted paper is your only white.

**Composition.** Diagonals and low worm's-eye angles. Nothing stands straight. Heroes are 8.5 heads tall, fists and boots foreshortened to two or three times normal toward the viewer. Action breaks the panel border: the figure is drawn after the frame, and the frame cracks where overlapped.

**Lettering.** All hand-made capitals. Narration sits in pale yellow (Y25) caption boxes with wobbly ink borders. Sound effects are drawn objects living in the shot's perspective. At most five SFX words, in Portuguese comic spelling (KA-BRUUM!, TUMP!, VRRUM!, TLIM!, TÓC!).

**Paper.** Warm gray newsprint with fibers, yellowed edges, faint show-through, fold creases on page seams. Solid black has tiny pale specks where the press missed.

**What breaks the style.** Gradients, glows, additive blending, blur, motion blur, drop shadows, bevels, rounded cards, monoline strokes, pure #fff or #000, smooth 3D, neon, giant decorative polka dots, parallax puppets sliding like a motion comic.

## Technique recipes

**Separated flats with real misregistration.** No per-pixel print filter. Paint each color as the plates printed it: one pattern per plate and tint, each with a small registration offset. Patterns follow the canvas transform, so dots belong to the sheet and grow when the camera pushes in. Dots are rigid and equal, like the period's mechanical tints.

```js
const INK={c:[0,156,214],m:[224,34,120],y:[250,220,44]};
const ANGLE={y:0,m:75,c:15}, DRIFT={y:[1.6,-.8],m:[-1.2,1.5],c:[.9,1.8]}, PITCH=7;
function tint(plate,pct){ // memoize by plate+pct
  const t=document.createElement('canvas'); t.width=t.height=PITCH;
  const g=t.getContext('2d'); g.fillStyle=`rgb(${INK[plate]})`;
  if(pct===100) g.fillRect(0,0,PITCH,PITCH);
  else{ g.beginPath(); g.arc(PITCH/2,PITCH/2,PITCH*Math.sqrt(pct/100/Math.PI),0,7); g.fill(); }
  const p=g.createPattern(t,'repeat');
  p.setTransform(new DOMMatrix().rotate(ANGLE[plate])); return p;
}
function flat(g,path,{c=0,m=0,y=0},paper='#ece0c3'){
  g.fillStyle=paper; g.fill(path);                  // knock out what lies beneath
  g.save(); g.globalCompositeOperation='multiply';
  for(const [k,v] of [['y',y],['m',m],['c',c]]){ if(!v) continue;
    g.save(); g.translate(...DRIFT[k]); g.fillStyle=tint(k,v); g.fill(path); g.restore(); }
  g.restore();
}
```

Ink goes last, in #17130f, with no offset, so color slips 1-2px past the line.

**The brush stroke.** Every inked line is a filled polygon around a spine, with pressure and seeded wobble. Build forms from point arrays (resampled Catmull-Rom, 12-40 points) so outlines can be sampled and feathered.

```js
function brush(g,pts,w,rnd,peak=.38){
  const L=[],R=[],n=pts.length-1;
  pts.forEach(([x,y],i)=>{ const t=i/n,[a,b]=pts[Math.min(i+1,n)],[c,d]=pts[Math.max(i-1,0)];
    const nx=d-b,ny=a-c,l=Math.hypot(nx,ny)||1;
    const s=t<peak?t/peak:(1-t)/(1-peak);
    const h=w*.5*Math.pow(s,.65)*(.82+.36*rnd());
    L.push([x+nx/l*h,y+ny/l*h]); R.unshift([x-nx/l*h,y-ny/l*h]); });
  g.beginPath(); [...L,...R].forEach(([x,y],i)=>i?g.lineTo(x,y):g.moveTo(x,y));
  g.closePath(); g.fill();
}
```

**Form shadow plus feathering.** The shadow is the form minus a copy shifted toward the light. Then break its edge with spikes.

```js
function formShadow(g,shape,lx,ly){
  g.save(); g.clip(shape);
  const m=new Path2D(); m.rect(-9e3,-9e3,2e4,2e4);
  m.addPath(shape,new DOMMatrix().translate(lx,ly));
  g.fill(m,'evenodd'); g.restore();
}
function feather(g,edge,nx,ny,len,step,rnd){ // edge: shifted outline, n: toward light
  for(let i=0;i<edge.length;i+=step){ const [x,y]=edge[i];
    const l=len*(i%3?.55:1)*(.75+.5*rnd());
    brush(g,[[x-nx*5,y-ny*5],[x+nx*l*.5+ny*2,y+ny*l*.5-nx*2],[x+nx*l,y+ny*l]],4.5,rnd,.05); }
}
```

Apply to every muscle mass, face, machine and building, with spikes of 14-40px. A figure with no feathering is a coloring-book page and fails.

**Energy crackle.** Energy is not glow. Inside a flat bright stream with a paper-colored core, scatter clusters of solid ink blobs: irregular, merging, power-law sizes from 2 to 34px, some ring-shaped, with tiny satellites and jagged ink tendrils at the edge. Reseed from `floor(t*10)` and stream position so it boils forward.

**SFX and block letters.** Load Bangers from Google Fonts and draw glyph by glyph, each with its own rotation and scale along a perspective fan. Extrude by stamping 20-40 offset copies toward one vanishing point in a side color, then a thick ink contour, then a front face split into two flats along a jagged line, then an outer paper-colored contour. Draw the huge N, the 1 and the colon as your own polygons, not font glyphs, with chiseled facets, feathered shadow planes and a deep perspective side.

**Paper pass.** Pre-render a 2400x1350 layer of fibers, foxing, edge yellowing, seam creases and a reversed ink ghost at 4 percent. Multiply it over each finished frame in screen space, with a speck mask for ink-starved solids.

## Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style, and never add a caption the brief did not ask for.

## Cast construction

Build one rig, not a cartoon per character. In head-units: ribcage egg, pelvis box, 18 joints with x, y, z; scale joints by depth so near limbs swell. Limbs are tapered outlines with muscle bulges (deltoid teardrop, biceps, forearm wedge, quad sweep, calf diamond), drawn back to front. Shoulders 3 heads wide on men, 2.4 on women, waist 1.5. Ink the pectoral shelf, serrated ribs, abdominal blocks, lat flare, kneecap. Fist: block, four knuckle arcs, thumb wedge. Order: line of action, masses, costume, flats, shadow, feathering, contour. Pre-render four cels per figure (anticipation, action, follow-through, hold) at about 900px tall.

**The main figure.** Whatever the brief says (age, hair, beard, glasses, clothes) becomes a three-quarter head with a strong brow, hair as black brush clumps over a flat plate color, facial hair as a clean flat mass with a feathered edge, and a locked everyday outfit in two process colors with one honest detail. Bare head. No mask, cape or chest symbol: the main figure is the ordinary person among heroes. Reuse the same head construction in every shot.

**Every other character the brief names becomes a hero, readable by silhouette alone.** No chest letters, insignia or real heroes. Only a caption tag with the word the brief uses for them. Give each one a silhouette shape and a power drawn from their job's tool, cycling through this list: tall flaring triangle with a long split coat and a staff; low wide block with a bandolier of their tool; S-curve flying horizontally with a gauntlet; many-limbed machine with a lens head; top-heavy wedge holding a heavy load overhead; hat disc with a whirling weapon; broad embracing arc of wings; column beside a slab-like shield. Vary age, body type and skin across the cast.

## Story grammar

**Steps.** Map the brief's sequence onto the sheet: each step happens on one page or across a gutter. Each step needs something the printed page physically does (a page torn, a gutter broken, a flap folded, a panel dealt like a card, a parcel thrown across pages). If a step would only get a caption, find the print event.

**A list of N things.** Never assume N. Each item is a panel: a first-person view where a gloved hand in its owner's color enters from a lower corner, doing one job. Bake static art at 640x540 and 320x270; draw the moving part live on held poses. Give each a flat background differing from its neighbors, hatching or speed lines, a hand-ruled frame, and a bold object silhouette readable at 200px.

- Up to 6 items per page in the six-panel grid; more items take more pages.
- N up to 8: panels are dealt onto the page one per eighth note.
- N from 9 to 54: one page per group, dealt as the group's hero lands.
- N above 54: the first pages at full size, the rest printed as tiny frames in the margins of the final cover.
- Two panels that could be swapped without anyone noticing have failed: each needs its own object, motion and sound.

**The relay.** When the story moves from one character or step to the next, the camera follows a crackling gold parcel thrown between pages, one beat per page: 0.3s held hit, then 0.15s whip. Each hero passes it with their own power, and each pass breaks a gutter. Camera scale about 0.8, so neighbors stay in view and all panels keep working.

**Numbers and short words.** A number or short word the brief puts on screen is a colossal red chiseled object: it smashes through the top of a page, tearing frame and paper, with two frames of pure black figures on Y100 and a sheet jolt. When the story opens it, its strokes crack and swing apart like vault doors, with crackle pouring out in the heroes' colors.

**Climax and ending.** Exactly one impact is the biggest in the film. To end, the pages fold onto the center, flap by flap every 0.09s with a shaded squash at each hinge, as the camera pushes in; the last flap's reverse is the final cover: red and yellow sunburst, the main figure calm in front, the other characters in a V behind, a monumental masthead with the brief's last words or number in the same chiseled letters, and the story's items as tiny frames around the edge. A corner box with the main figure's head and "Nº 1" is fine; no publisher mark. It settles in 0.3s, then holds at least one second. Only sunburst crackle may flicker.

**Pacing by duration.** Tempo is exactly 133.33 BPM: one beat is 0.45s. Hook within the first 2 s; something changes every 1 to 2 s. At about 10 s use 3 acts; at 13 to 15 s use 4 to 5. Write a beat table before drawing (start, end, exact on-screen text, the print event that causes the cut, main sounds); picture and sound read the same constants.

## Animation language

Comics move in poses. Figures animate on threes with hard holds, one-frame ink-streak smears, and anticipation before every action. Camera, flying objects and paper run at 30fps. Speed lines, never blur. Impacts get a 2-frame sheet shake, a cracked border, ink debris. Crackle, speed lines and SFX edges boil on threes; figures stay stable. Every second needs at least four independent motions: pose, panel task, crackle, debris or paper, SFX. Every transition is something that happens to the printed sheet; the swap happens while the page is covered.

## Sound design

This world has three voices: **the printing press that makes the page, the paper it lives on, and a 1970s TV action pit band** of brass, timpani, snare and electric bass, in D Mixolydian. Render everything once in an OfflineAudioContext during `ready`, play that buffer live, and take film time from the audio clock. Noise comes from the seeded generator. Each sound lands on the drawn frame of contact, on the same threes as the figures.

**Buses.** Foley, dry. Band: highpass 80Hz, lowpass 7.5kHz, short room convolver from 0.6s of decaying seeded noise, dipped 6dB for 180ms under big hits so effects read. Impact, dry and full range. Master: compressor at -14dB, 3:1, 5ms attack, 120ms release, then tanh soft clip. Measure a K-weighted gated estimate on the rendered buffer and set one trim for -16 LUFS, peaks below -1 dBFS.

**Instruments.**
- *Press:* 12ms 1.4kHz square burst through bandpass Q6, then sine 92→61Hz in 110ms plus 60ms of 300Hz bandpassed noise.
- *Paper flick (each whip):* white noise, bandpass Q1.2 sweeping 900→5200Hz in 110ms, attack 8ms, decay 130ms, gated by a jittered 180Hz pulse, plus sine 190→110Hz in 35ms.
- *Paper tear:* 60 noise grains of 1-3ms, highpass 1.8kHz, density rising over 0.35s, panned along the tear.
- *Timpani:* sines f, 1.5f, 2f, pitch 1.06f→f in 60ms, decay 700ms, plus a 15ms tick lowpassed at 700Hz.
- *Snare:* noise bandpass 2.4kHz Q0.7 plus triangle 185Hz, decay 120ms.
- *Crash:* six inharmonic squares at 600-2400Hz, highpass 6kHz, plus noise, decay 1.4s.
- *Brass:* per note two saws detuned ±6 cents plus a square an octave down at -12dB. Lowpass 500→3200→1400Hz in 35 and 120ms, Q1.2. Attack 18ms, scoop from -40 cents in 30ms, release 90ms, light tanh. Voice in open fourths and fifths.
- *Bass:* triangle plus saw, lowpass 650Hz, decay 220ms.
- *Crackle:* 58Hz saw through a resonant filter jumped by seeded 18Hz sample-and-hold, plus pulse-gated noise.

**Scored moments.**
- *Burden:* no band. A load groaning: 38Hz saw through bandpass 420Hz Q14, jittered center, stick-slip bursts at 7-13Hz. Strained breath: noise bandpass 900Hz, two cycles. Timpani heartbeat at 58Hz. Press thunks at half speed, laboring. A muted trombone D sags 20 cents.
- *The big arrival:* an accelerating snare roll, rising chromatic brass, timpani crescendo; on the hit, sub sine 90→40Hz in 300ms, timpani on D, crash, tutti stab, big tear. Then 200ms of near silence with debris clatter. A vault groan when it opens: saw 45→120Hz through a sweeping bandpass, crackle swelling.
- *Heroes arriving:* brass stabs climb D E F# G A B C D, one per hero on the eighths, each layered with the hero's signature and panned to their leap.
- *The relay:* full band. Bass ostinato, press on eighths as hi-hat, snare on 2 and 4, bongo fills, an eight-note brass line (5, 5, ♭7, 1, 5, ♭7, 1, 2), paper flick on each whip, signature on each hit.
- *All together:* the band drops out and the **foley becomes the music**: press, ticks, stamps, teletype, engines, bells lock into the groove while low brass holds a soft D and the timpani heartbeat returns, slow and steady, mirroring the opening. Paper flaps for each fold, rising in pitch.
- *Ending:* flap slap, two brass buttons (ba-BAM) on an open D with timpani and crash, the band tails out over the hold, one last press thunk.

**Hero signatures.** Each hero's sound comes from their power, in the order the silhouettes are assigned: rising sine 1300→1950Hz with 7Hz vibrato and cloth snap; register bell (2350, 3520Hz, decay 500ms) with six plastic ticks; shouted "HA" (saw through formants 700 and 1800Hz) with 30 micro claps; 20Hz square teletype ticks with a servo saw 220→440Hz; 65Hz diesel saw with 18Hz pulse and an air horn of saws at 233 and 311Hz; whirl (noise bandpass 700Hz, AM accelerating 9→16Hz) and bell (1760, 2640, 4430Hz, decay 1.1s); wingbeat (lowpassed noise 350Hz, 140ms swell) with a soft major-third chime; stamp on wood (600, 1130Hz, 30ms, 110Hz thud) with shield ring (430, 1170, 2260Hz, decay 400ms).

**Item sounds.** Each panel's job gets one short sound under 0.2s on the frame it acts, built from the instruments above to match the drawn object.

**Density.** 5 to 15 audible events per second outside the rolls; at most 3 foreground sounds at once besides the band; repeated ticks at most 12 per second.

Every whoosh is paper, every thud is press, wood or metal, and every SFX word has a matching sound on the same frame.

## Density, and the film to avoid

The predictable version is flat cartoon figures with thin outlines, a polka-dot background, POW starbursts, rounded rectangles of icons sliding in a grid, a gradient sky, and a cheap synth fanfare with stock whooshes. If it could pass as a modern explainer with a comic filter, start over.

Every shot has foreground, figure and environment, and every surface carries ink. Backgrounds are real places the brief implies, drawn as 1970s comic places: rooftops, pipes, skyline windows, streets, kitchens, machinery full of knobs. Add small drawn life: tiny figures looking up, flying papers, and the two house animals from the house animals brief, inked and flatted in this medium. Blank flat area is allowed only as a deliberate color drop behind an action figure, and even then it carries speed lines or crackle.

Pre-render heavy art in `ready`, yielding between pieces, under about 400MB of bitmaps. Any frame you seek to must look like a comic someone would pay to read.

**Before finishing:** every step of the brief has a print event, not only a caption; every item is a different drawn object with its own sound; exactly one biggest impact; the final cover holds at least one second; text sizes on 1920x1080 are at least 66 px for titles, 42 px for essential labels and 96 px for key numbers.

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
