# Flat Folks

Build one finished animated film in modern flat illustration: a small, warm world of geometric people who act out whatever the content brief tells, with real walks, real hand-overs and real eye contact, and with every object, icon and number drawn in the same flat language as the people. The story and technical delivery follow this text.

## The film you must not make

The predictable version: corporate figures with tiny heads and stretched purple limbs, a grid of clip-art icons from another style, people gliding across the floor without walking, a fade or slide between every scene, white backgrounds, a ukulele-and-claps loop. All of that fails. This film looks like a top editorial illustrator drew every frame, and like a character animator acted every gesture.

## 1. Identity

**Contract.** Flat vector shapes on calm colored grounds, lit by one implied light from the upper left. No line work: form comes from color, overlap and one hard shadow shape per color.

**Three signatures that any still frame must show:**

1. People built from circles, capsules and rounded rectangles, with natural proportions (head one sixth of body height) and a minimal face.
2. Every color shape carries exactly one hard-edged shadow shape in the same hue, 8 to 12% darker, on the side away from the light.
3. Ideas appear as flat icons inside white speech bubbles with tails, springing out of the person who has the idea.

**Three exclusions:** never an outline around a filled shape (face strokes excepted); never a gradient, glow, blur or drop shadow; never a figure whose head is smaller than one seventh of its height.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the scene, never a stretch.

## 3. Material primitives

Everything in the film is built from these, and nothing else.

- **Ground.** Each scene has one flat background color and a floor band below a ground line at 76% of frame height, 6 to 8% darker than the background. No texture, no vignette, no paper grain.
- **Shape.** Circles, capsules, rounded rectangles (corner radius at least 10 px) and soft blobs made of circular arcs. Build each as a `Path2D` once; reuse it.
- **Shadow.** For each shape, one crisp shadow shape clipped inside it: the same path offset 6 to 14% of the shape's size toward the lower right, filled with the base color darkened 8 to 12% in lightness (convert to HSL, never multiply with black). Small shapes under 20 px get no shadow.
- **Contact.** Anything standing on the floor gets a flat ellipse under it, floor color 10% darker, 80% of its footprint wide and 14% as tall. It shrinks and lightens with height when the thing jumps.
- **Strokes.** The only strokes in the film: eyebrows, mouths, eyelid closures, and motion arcs. Round caps, ink color, 4 px at a 380 px figure. Strokes scale with the figure, never with the camera.
- **Lettering.** Google Fonts `Figtree` (600 for captions and labels, 800 for titles and numbers). Text sits on white rounded pills (padding 0.45 em by 0.8 em) or directly on calm ground at high contrast. Minimums at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px, captions 44 px.
- **Palette.** A closed set of 12, chosen per film from this family and then frozen: ink `#1F2A44`, white `#FFFFFF`, peach `#FFE3D3`, mint `#D6F1E4`, butter `#FFF0C2`, sky `#DCEBFF`, lilac `#ECE3FF`, coral `#E85A4F`, saffron `#F2B84B`, cobalt `#3E7BFA`, leaf `#3FAE64`, berry `#C2417A`. Skins from `#F6C9A6`, `#E3A67C`, `#B97A52`, `#8D5A3B`, `#5E3A26`. Hair from ink, `#6B3E26`, `#B8742E`, `#D9D2C5`. Every color in the film comes from these lists.
- **Finish.** None. The crispness is the finish: anti-aliased edges, no noise, no grain, nothing glowing.

## 4. Material time

Figures move on ones (30 fps) with closed-form motion; there is no boiling line and no grain to redraw. Every motion uses one of three curves: `easeInOutCubic` for gestures and camera, `easeOutBack` (overshoot 1.4) for anything that pops in, and a closed-form damped spring (damping 0.6, 2 Hz) for anything that lands or wobbles. Secondary parts (hair tufts, hat brims, ties, leaves, bubble tails) follow the part they hang from with a 60 ms lag. A figure is never perfectly still: idle breathing moves the torso 2 px at 0.25 Hz, and eyes blink (closed for 0.12 s) every 2.2 to 3.4 s on a seeded schedule.

## 5. Piece vocabulary

Turn any noun of the brief into one of these pieces. Each has an entrance, a rest and an exit.

- **Figure.** See Cast construction. Enters walking or stepping in from the edge, never fading.
- **Central object** (the thing the story is about: a tool, a device, a machine, a place). A flat object with one part that physically changes when the story changes: a screen that lights, a lid that opens, a gauge whose needle swings, a door, a dial. Built at least 400 px wide when it is the subject.
- **Icon.** Drawn in the figures' language: two to five flat shapes with their shadows, no outlines, 96 to 160 px. Never a glyph, emoji or icon font. Any noun becomes an icon by its most recognizable silhouette plus one color cue.
- **Speech bubble.** White rounded rectangle, radius 28 px, with a triangular tail toward the speaker's mouth. Holds one icon, an icon plus a short number, or up to five words. Springs out of the speaker's head (scale 0 to 1 with `easeOutBack`, 0.35 s), stays at least 1.4 s, deflates back toward the mouth (0.2 s). It never covers a face.
- **Caption pill.** The brief's narration line, centered on a white pill at 89% of frame height. The old line lifts 12 px and fades out over 0.25 s while the new one rises 12 px over 0.35 s. On screen at least 1.6 s. The caption band is kept free of figures and props.
- **Arrow or link.** A flat capsule 14 px thick in ink or a palette color that grows from its start to its end over 0.3 to 0.5 s; the triangular head pops in only when the shaft arrives.
- **Label.** A white pill with ink text, attached to what it names by a 3 px ink tick. Always drawn in a last pass above everything else.
- **Counter.** Big `Figtree 800` digits on a white or butter pill. Rises along an ease-out power curve (exponent 2.5) and settles; each change ticks on screen, at most 12 ticks per second, and locks with a spring pop of 12%.
- **Error mark.** The central object's changing part turns coral, the figure shrugs or scratches its head, and a small coral cross icon pops in a bubble. **Success mark:** the part turns leaf green, a check icon pops, and the figure gives a small hop (12 px).
- **Emphasis.** One flat ring in saffron, 10 px thick, drawn around the key element over 0.4 s, at most once per scene.

## 6. Story grammar

### Cast construction

The style does not know who is in the story. It says how anyone the brief describes becomes a figure.

- **Adult figure, 380 px tall** (scale for other ages: a child is 260 px with a head one fifth of height). Head: a 64 px circle. Neck: a short capsule hidden by the collar. Torso: a rounded trapezoid 110 px wide at the shoulders, 92 at the hips, 150 tall. Arms and legs: two-segment capsules (arms 24 px wide, legs 30 px wide), solved every frame with analytic two-bone inverse kinematics toward hand and foot targets, so hands really hold things and feet really plant. Hands: 15 px circles. Shoes: half-ellipses 46 px long.
- **Face:** two 7 px ink dots for eyes at 52% of head height, set 22 px apart; short floating brows; a 4 px round-capped mouth stroke. Expressions come only from brows, mouth and head tilt: calm, worried (brows tilted up inward, mouth a flat wave), strained (eyes closed as short arcs, mouth a tight line), delighted (mouth an open half-disc in coral with a white tooth band), surprised (eyes 9 px, mouth a small circle).
- **What the brief says about a person** (age, hair, beard, glasses, clothes, job) becomes one or two blob shapes or a single prop: hair as one or two blobs over the head; a beard as one blob along the jaw, one step lighter than the hair; glasses as two thin ink rings with a bridge (the only other stroke allowed); a job as one prop held in the hand.
- **Scale.** In main scenes the figure in focus is at least one third of frame height with a face of at least 50 px. With more than 4 figures, show 2 to 4 at a time as the camera passes, and gather everyone only at the reunion moment, where no face is under 24 px; whatever does not fit becomes a group with one large representative.
- **Several figures:** each one is identifiable by silhouette and one dominant clothing color from the palette, never by a caption alone. Mix skin tones and hair across the cast. Every figure keeps the same marks from first frame to last.
- **Acting.** Anticipation (a 3 to 5 frame wind-up) before every gesture, follow-through after. Heads tilt 6 degrees toward whoever acts or speaks. When two figures exchange anything, their eyes meet and their hands overlap on the object for at least 0.2 s. Walks are closed-form: 1.6 steps per second, hip bob 6 px twice per stride, legs swing ±24 degrees, arms swing opposite ±18 degrees, the planted foot never slides.
- **Originality.** No real person, mascot or cartoon character; no logo; no corporate tiny-head figure; no lavender-skinned people.

### A list of N things

Never assume N. The brief's list becomes a set of **cards**: white rounded rectangles (radius 18 px, 5% darker shadow shape along the bottom edge) each holding one icon that performs its job in a short loop (a gear that turns, a chart whose bars grow, a letter that folds, a bell that swings). Pre-render each card's static base once; draw only its moving part per frame. Cards are 200 to 320 px wide when shown alone. Two cards that could be swapped without anyone noticing have failed: each needs a different silhouette and action.

- **N up to 8:** cards spring out of the figure that owns them one by one, every 0.15 to 0.25 s, landing in a fan or a row, each with its own small sound.
- **N from 9 to 30:** cards are grouped. Each group belongs to one figure and appears on a panel behind that figure: a flat device screen, a shelf, a noticeboard or a window of a building, whatever the world offers. Inside a group the cards fill an adaptive grid (2 or 3 columns, rows grow with the group size), revealed in reading order every 0.08 to 0.12 s.
- **N above 30:** the first group is shown at full size; the rest appear as a dense, ordered mosaic of small cards (at least 60 px wide), each still moving, with the counter telling the total. Only the first cards get labels.
- Every card enters, lives and leaves the same way. The owning figure reacts to each arrival (a nod, a pointing hand, a 5% pulse of its panel).

### Steps

Each step of the brief gets a **verb the world performs** (something is picked, carried, dropped, opened, typed, handed over, switched on) and a **place**: a split-screen half, a desk, a doorway, a device screen. Group two steps per place when they share one. Something always continues from one step into the next: an object carried across, a figure walking in, a screen that keeps glowing.

### Cause, error and fix

Cause is shown by something that travels: a carried object, a growing arrow, a ball of color sliding along a path. If the brief has an obstacle or a mistake, use the error mark, show the signal travelling back along the same path to the part that must change, show the physical fix (a hand turns the dial, a lid is closed, a card is swapped), then the success mark.

### Numbers and short words

A number or short word the brief puts on screen is a big flat object: thick `Figtree 800` letters built as filled shapes with their hard shadow shape, at least 96 px for numbers and 140 px when it is the key image, landing with the spring (12 to 18% overshoot).

### Climax and ending

Exactly one moment is the biggest in the film: the brief's key image. Before it, 0.3 s of near-stillness (figures hold their pose, music drops out). At the moment, the key image lands with the spring, a flat burst of 8 to 12 radiating capsules in saffron and coral pops behind it, and every figure reacts in the same frame. The last image shows the brief's last words or number largest in frame, readable at thumbnail size, the figures standing calmly beside it, held at least 1.2 s with only blinks and idle breathing.

### Pacing by duration

Hook within the first 1.5 s: the main figure is already on screen and doing something. Something changes every 1 to 2 s. About 10 s: 3 places. 13 to 16 s: 4 places. Before drawing, write a beat table: one row per beat with start and end time, the exact on-screen text, the physical cause that moves us to the next beat, and the main sounds. Picture and sound both read their times from that table.

## 7. Transitions

Every change of place is a physical event of this flat world, 0.4 to 0.8 s long, and the swap happens while the frame is covered.

1. **Push into a screen.** A figure raises a device; the camera pushes into its screen until the screen's color fills the frame (log-scale zoom, `easeInOutCubic`). The new place is inside the screen.
2. **Color flood.** A button, a door or a bubble is tapped and its color grows as a circle from the tap point until it covers the frame; the circle then opens onto the next place, which uses that color as ground.
3. **Split and slide.** A vertical wall edge divides the frame into two grounds for two figures; it slides to merge them into one scene when they meet.
4. **Walk through.** A figure walks out of frame and the camera follows on a long continuous floor to the next place.

Never use a dissolve, a page flip, a generic wipe or a hard cut to change idea.

## 8. Camera

Mostly still, framed so figures stand on the ground line. At most 6 camera moves in 15 s, each eased with `easeInOutCubic`; zoom interpolated in log scale between 0.85 and 1.35, with one push-in up to 2.5 when entering a screen, and one pull-back at the gathering moment that shows everything. Shape sizes and strokes scale with the world; text that must be read is counter-scaled so it never drops below the minimums. The edge of the world never shows: grounds extend past every framing.

## 9. Sound

A warm, light studio sound for flat illustration: soft, round, wooden and plucked, never metallic or digital. Picture and sound share one clock; every sound lands on the frame of visible contact (foot down, card landing, button pressed), found from the animation curve, within one frame.

**Helpers.** `pluck(t, f, dur, lvl)`: Karplus-Strong in plain JS with soft damping. `mallet(t, f, lvl)`: marimba-like, sine at f plus 4f at -14 dB, attack 2 ms, decay 0.35 s. `pop(t, f0, f1, dur, lvl)`: sine with fast exponential pitch drop. `nz(t, kind, filter, f, Q, a, d, lvl)`: seeded white, pink or brown noise. Levels in dB. No speech, no choir.

**Music.** A light groove at 112 BPM (16th = 0.134 s): muted upright pizzicato bass (pluck through lowpass 900 Hz) on beats, a two-mallet marimba figure on offbeats, a soft shaker (white noise bandpass 6000 Hz, 30 ms) on 16ths at -26 dB, finger snaps on 2 and 4. The groove starts sparse (bass and shaker) and gains one voice per scene.

**Vocabulary (9 to 20 sounds).**

- Footstep: soft felt thump, brown noise lowpass 300 Hz, 60 ms, -18 dB, panned to the foot.
- Bubble pop-in: `pop(900→1500 Hz, 70 ms)` plus a high mallet, -12 dB.
- Bubble deflate: `pop(1200→500 Hz, 90 ms)`, -20 dB.
- Card landing: wooden mallet tuned to the card's index on a pentatonic scale (C D E G A, rising), -10 dB.
- Icon action loops: one tiny tuned sound per card on its contact frame (gear ratchet as 3 noise ticks, bell as an inharmonic mallet, paper fold as a pink-noise flick, chart bar as a rising pluck), -14 dB.
- Arrow grow: pink noise bandpass sweeping 600→1800 Hz over the grow time, -22 dB; the head lands with a short mallet.
- Phone or button tap: two quick clicks (white noise highpass 3000 Hz, 8 ms, 40 ms apart), -14 dB.
- Screen push: airy noise swell, bandpass sweeping 400→2400 Hz, starting 0.4 s before the cover, peaking on it.
- Color flood: a soft whoomp, sine 90→60 Hz with pink noise lowpass 700 Hz, 0.45 s, -10 dB.
- Counter tick: mallet at 1600 Hz, 25 ms, -18 dB, at most 12 per second; the lock: chord C-E-G on mallets, -8 dB.
- Error: two low plucks falling a minor third (E3 to C#3), -12 dB. Success: three rising mallets G-B-D, -10 dB.
- Shrug or effort: a quick breathy whoosh, pink noise bandpass 1000 Hz, 120 ms, -22 dB.
- Climax: the music cuts 0.3 s before; then a big round thump (sine 70→40 Hz, 0.6 s, -4 dB), a full mallet chord and pizzicato strum, a shaker burst, and the burst capsules each with a tiny tick.
- Ending: the groove resolves on the tonic with a let-ring mallet chord and fades over the hold.

**Density.** 4 to 12 audible events per second; at most 3 foreground sounds at once besides the music; the climax is the single loudest moment. If two sounds collide, delay or drop the lesser.

**Mix.** Music bus ducked 4 dB for 120 ms under each foreground hit by scheduled gain; pan by screen position, `(x / 1920 - 0.5) * 1.2`. Loudness and peaks as the technical delivery asks.

## 10. Hero frame

The last frame: the brief's closing words or number largest in frame on a calm ground, the main figure and the cast standing on the ground line beside it, every shape with its hard shadow, one saffron ring or burst behind the key word. It must read as this style with no caption.

## 11. Style check

Never ship a stub or "similar for the rest": every person, item and place the brief asks for must exist, drawn. A long file is expected. Inspect frames at 0%, 10%, 25%, 50%, 75% and 95% of the duration:

- Does the very first frame already show the scene and a figure?
- Is every filled shape flat, with exactly one hard shadow shape and no outline, gradient or glow?
- Are heads one sixth of body height, faces made of dots and short strokes, and every figure distinct by silhouette and color?
- Do hands touch what they hold and do feet stay planted while walking?
- Is every icon drawn in the figures' language, never a glyph or emoji, and does every card show its own action?
- Do bubbles and labels never cover faces, and does the caption band stay clear?
- When everything is together, are all items visible, separate and alive, with no empty slot or blank card?
- Is there exactly one biggest moment, and does the last frame hold at least 1.2 s with the closing text the largest element?
- Text at 1920x1080: titles 66 px, essential labels 42 px, key numbers 96 px, captions 44 px, never smaller.

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
