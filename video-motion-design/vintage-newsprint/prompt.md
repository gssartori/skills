# Vintage Newsprint

Build one finished animated film in the **Vintage Newsprint** (Print & Editorial) visual style: A 1950s broadsheet newspaper front page and science supplement on aged, edge-darkened newsprint (#EFE6D2) with noisy ink coverage thresholds (50% ± 17%), 7.5% blurred mirror show-through from the reverse page, 45° halftone dot screens on illustrations, column rules, and reader wax-pencil red markup. The story and technical delivery follow this text.

## The film you must not make

The predictable version: a clean modern blog layout on flat white with crisp digital photos, smooth CSS fades, or tiny cramped cards. All of that fails. This film looks like real 1950s rotary newsprint on a dark reading desk: yellowed paper edges, 45° halftone dots proportional to sqrt(darkness), reverse-page bleed-through, physical page-turn transitions, and grease-pencil red rings.

## 1. Identity

**Contract.** A 1950s broadsheet newspaper front page and science supplement on aged, edge-darkened newsprint (#EFE6D2) with noisy ink coverage thresholds (50% ± 17%), 7.5% blurred mirror show-through from the reverse page, 45° halftone dot screens on illustrations, column rules, and reader wax-pencil red markup.

**Three signatures that any still frame must show:**

1. Aged newsprint sheet (#EFE6D2 darkening 120 px near margins, 0.25% pulp specks, horizontal fold crease, and 7.5% mirrored reverse-side show-through) resting on a dark desk border.
2. 45°-rotated halftone dot screens (`radius = cell * sqrt(darkness)`) for portraits and illustrations, paired with noisy thresholded ink (2.5% micro-voids and paper-colored label halos that cut cleanly across diagram arrows).
3. Reader wax-pencil crimson (`#C83228`) hand-drawn emphasis rings and a physical 0.7 s left-edge page turn casting a moving shadow across the sheet below.

**Three exclusions:**
- Never use full-color photographic bitmaps or smooth gradients: only newsprint paper, worn black ink `#1E1C1A`, faint blue-grey show-through `#6E7885`, and red grease pencil `#C83228`.
- Never let diagram arrows slice through label text without a paper-colored halo cutout.
- Never crowd more than 4 halftone column cards into one camera framing.

## 2. Priorities

The content brief decides subject, facts, characters, on-screen language and duration. This style decides only how it is drawn, moved and heard. If the brief locks a sequence of events, keep every event, its order and its meaning; vary only the treatment. Never invent story facts to fit the style and never add a caption the brief did not ask for. A requested aspect ratio is a recomposition of the stage, never a stretch.

## 3. Material primitives

Pre-render static paper/glass/substrate layers and reusable material buffers once into offscreen canvases at init so `seek(t)` executes in `< 20 ms` per frame.

- **Palette.** Newsprint center `#EFE6D2`, aged edge `#DACBAd`, rotary black ink `#1E1C1A`, show-through blue-grey `#6E7885`, reader red wax pencil `#C83228`, reading desk `#231F1C`.
- **Lettering.** Google Fonts: `UnifrakturMaguntia` or `Playfair Display` (900) for masthead & stretched broadsheet headlines, `IBM Plex Serif` (600) for body columns, `IBM Plex Mono` (600) for datelines and infographic numbers. Minimums at `1920x1080`: headlines `72 px–120 px`, essential labels `42 px–54 px`, key numbers `96 px–140 px`, captions `38 px`. Keep all text inside safe margins (`x = 80..1840`, `y = 65..1015`).
- **Finish.** Full-frame material finish pass running on every frame from `t = 0` to `duration`.

## 4. Material time

Smooth, deliberate, and continuous at `30 fps`. Every element enters over `>= 0.3 s`, breathes with secondary motion while on screen, and exits with a physical cause. Give every major beat `2.2 s–3.2 s` of calm breathing room, limit simultaneous showcase cards to `2–4` at a time, and keep consecutive identical frames `<= 15%`.

## 5. Piece vocabulary

Turn any noun of the brief into a native piece of **Vintage Newsprint**:
- **Central hub (the system).** Physical centerpiece constructed from the style's core material primitives that visibly changes state when calibrated.
- **Figure.** See Cast construction.
- **Card / Station.** Well-spaced showcase unit (`~350x520` for groups of 2–4, or `~145x105` for grid tiles) carrying `3` unmistakable material-drawn task icons in local `(x, y)` coordinates.
- **Connector / Arrow.** Drawn progressively along its arc length (`0.3 s–0.5 s`) in the medium's native stroke.
- **Counter.** Non-linear eased numeric readout (`>= 96 px`) locking with a physical emphasis mark.
- **Error / Success mark.** Physical material state change on error returning along the connector to `3` calibration controls, followed by a clear reward seal.

## 6. Story grammar

### Cast construction

- **Scale.** In main scenes the figure in focus is at least one third (1/3) of frame height (`>= 360 px` at `1080p`) with a face of at least `50 px`. With more than `4` figures, show `2` to `4` at a time with `3` clear task icons per card, and gather everyone only at the final reunion where no face is under `24 px`.
- **Consistency.** Keep the protagonist's silhouette, beard, hair, and outfit marks identical from frame `0` to the final frame.

### A list of N things

Never assume `N`.
- **N up to 8:** Each item enters as its own material card every `0.25 s`.
- **N from 9 to 24:** Group items into `2` to `4` calm cards (`3` clear icons per card) across sequential beats, holding `>= 1.8 s` per group.
- **N above 24:** Showcase top-level roles in `4`-card groups first, then reveal a breathable matrix of `24` well-spaced mini-tiles (`18 px` gutters, `1` clear glyph per tile) paired with a rising progress chart.

### Steps

Each step of the brief is a physical construction stage in the material, accumulating cleanly with `>= 0.6 s` settle time before any transition.

### Cause, error and fix

Cause travels visibly along connectors. An obstacle triggers the error mark and travels back to calibrate `3` physical controls before locking in the fix.

### Numbers and short words

Set key numbers at `>= 96 px` (`130 px+` for the hero ratio) and keep on-screen text to concise labels — never full-sentence subtitles.

### Climax and ending

Pause background motion and music for `0.3 s` just before the climax hit. On the climax beat, center the protagonist (`>= 360 px` tall) flanked symmetrically by active mini-tiles, lock in the largest closing ratio/takeaway with the style's signature emphasis, and hold for at least `1.2 s`.

### Pacing by duration

Frame `0` (`t = 0`) is ALREADY an active, populated hook. Before drawing, write a beat table (start, end, on-screen text, physical cause, and main sounds) so picture and sound share one clock.

## 7. Transitions

1. **Reader's eye camera pan & zoom (0.55s–0.75s):** Smooth `ease.inOutCubic` travel from the top banner headline down into the multi-column infographic.
2. **Broadsheet page turn (0.7s):** The front page lifts 22 px from the right, curls across the left spine casting a soft shadow, and reveals the inside science supplement page.
3. **Wax-pencil circle & double-rule stamp (0.35s):** Crimson grease-pencil ring draws around the hero statistic.

## 8. Camera

Reader's-eye camera moving across 6 to 10 eased keyframes (`zoom 0.92x` full broadsheet to `1.55x` column close-up), keeping column rules crisp and counter-scaling labels.

## 9. Sound

Quiet reading room tone with crisp newsprint paper rustle on camera moves (bandpass pink noise 1.2–2.6 kHz, -20 dB); knuckle tap on the page (160 -> 85 Hz thump + 700 Hz paper pat, -16 dB); dry pen scratch matching diagram arrow duration; crumbly wax-pencil drag (850–1350 Hz grains) on red rings; 0.7 s page turn whoosh + settle slap; climax linotype 7-hit burst and deep rotary press chord.

## 10. Hero frame

Full broadsheet science page framed on the dark desk: central 45°-halftone protagonist portrait (>= 360 px tall) flanked symmetrically by column boxes with crisp infographic glyphs, bold stretched banner headline, crimson wax-pencil ring around the key ratio, and halftone house animals in the masthead/corner ear boxes, held >= 1.2 s.

## 11. Style check

Inspect frames at `0%`, `10%`, `25%`, `50%`, `75%`, and `95%` of duration:
- [ ] Frame `0` is already active and readable (zero blank screens).
- [ ] All three identity signatures are visible in every still frame.
- [ ] Primary figures `>= 1/3` frame height (`>= 360 px`) with `>= 50 px` faces; `2–4` cards per view with `3` clear task icons each.
- [ ] Zero overlapping cards, zero clipped HUD text, and `<= 15%` identical consecutive frames.
- [ ] `renderAudio()` outputs `48000 Hz` stereo within `-19` to `-12` LUFS, true peaks `<= -4 dBFS`, zero silence `> 1.5 s`.

## Reference Engine (`Motion`)

```js
// Motion Engine, version 1.
// Rule of the engine: a frame is a pure function of (time, seed). There is no clock, no
// accumulated state and no system randomness, so any instant can be drawn in any order.
;(function (root) {
  'use strict'

  const TAU = Math.PI * 2

  // Numbers
  const clamp = (value, low = 0, high = 1) => Math.min(high, Math.max(low, value))
  const mix = (from, to, amount) => from + (to - from) * amount
  const remap = (value, fromLow, fromHigh, toLow = 0, toHigh = 1) =>
    mix(toLow, toHigh, clamp((value - fromLow) / (fromHigh - fromLow)))
  const snap = (value, step) => Math.floor(value / step) * step

  // Movement curves. Every curve maps 0 to 0 and 1 to 1.
  const OVERSHOOT = 1.70158
  const ease = {
    linear: (v) => v,
    inQuad: (v) => v * v,
    outQuad: (v) => 1 - (1 - v) * (1 - v),
    inOutQuad: (v) => (v < 0.5 ? 2 * v * v : 1 - 2 * (1 - v) * (1 - v)),
    inCubic: (v) => v * v * v,
    outCubic: (v) => 1 - (1 - v) ** 3,
    inOutCubic: (v) => (v < 0.5 ? 4 * v * v * v : 1 - 4 * (1 - v) ** 3),
    outExpo: (v) => (v >= 1 ? 1 : 1 - 2 ** (-10 * v)),
    outBack: (v) => 1 + (OVERSHOOT + 1) * (v - 1) ** 3 + OVERSHOOT * (v - 1) ** 2,
    outBounce: (v) => {
      const rest = 1 - v
      if (rest < 1 / 2.75) return 1 - 7.5625 * rest * rest
      if (rest < 2 / 2.75) return 1 - (7.5625 * (rest - 1.5 / 2.75) ** 2 + 0.75)
      if (rest < 2.5 / 2.75) return 1 - (7.5625 * (rest - 2.25 / 2.75) ** 2 + 0.9375)
      return 1 - (7.5625 * (rest - 2.625 / 2.75) ** 2 + 0.984375)
    },
    outSpring: (v) => (v >= 1 ? 1 : 1 - Math.cos(v * 9) * Math.exp(-5.5 * v)),
    stepped: (v) => (v >= 1 ? 1 : Math.floor(v * 6) / 6),
  }

  // Progress of `time` through a range. The ends are exact, so `span(...) > 0` is a safe test.
  function span(time, start, end, easing = ease.linear) {
    const amount = clamp((time - start) / (end - start))
    if (amount === 0 || amount === 1) return amount
    return easing(amount)
  }

  // An envelope for something that strikes at `at`: 0, up to 1 over `attack`, back to 0 over `release`.
  function hit(time, at, attack, release) {
    if (time <= at) return 0
    if (time < at + attack) return (time - at) / attack
    return clamp(1 - (time - at - attack) / release)
  }

  // Seeded randomness
  function hashText(text) {
    let hash = 2166136261
    for (const character of String(text)) hash = Math.imul(hash ^ character.codePointAt(0), 16777619)
    return hash >>> 0
  }

  function stream(seed) {
    let state = typeof seed === 'number' ? seed >>> 0 : hashText(seed)
    function float() {
      state = (state + 0x6d2b79f5) | 0
      let word = Math.imul(state ^ (state >>> 15), 1 | state)
      word = (word + Math.imul(word ^ (word >>> 7), 61 | word)) ^ word
      return ((word ^ (word >>> 14)) >>> 0) / 4294967296
    }
    return {
      float,
      range: (low, high) => mix(low, high, float()),
      int: (low, high) => low + Math.floor(float() * (high - low + 1)),
      pick: (list) => list[Math.floor(float() * list.length)],
      chance: (probability) => float() < probability,
      fork: (label) => stream(hashText(`${state}:${label}`)),
    }
  }

  // Smooth value noise, always between 0 and 1.
  function lattice(x, y, seed) {
    const mixed = Math.imul(x, 374761393) + Math.imul(y, 668265263) + Math.imul(seed, 2147483647)
    const word = Math.imul(mixed ^ (mixed >>> 13), 1274126177)
    return ((word ^ (word >>> 16)) >>> 0) / 4294967295
  }

  function noise(x, y, seed = 0) {
    const cellX = Math.floor(x)
    const cellY = Math.floor(y)
    const blendX = ease.inOutCubic(x - cellX)
    const blendY = ease.inOutCubic(y - cellY)
    const top = mix(lattice(cellX, cellY, seed), lattice(cellX + 1, cellY, seed), blendX)
    const bottom = mix(lattice(cellX, cellY + 1, seed), lattice(cellX + 1, cellY + 1, seed), blendX)
    return mix(top, bottom, blendY)
  }

  function fractal(x, y, seed = 0, octaves = 4) {
    let total = 0
    let weight = 0.5
    let scale = 1
    let sum = 0
    for (let octave = 0; octave < octaves; octave += 1) {
      total += noise(x * scale, y * scale, seed + octave) * weight
      sum += weight
      weight *= 0.5
      scale *= 2.03
    }
    return total / sum
  }

  // Color
  function channels(color) {
    const value = Number.parseInt(color.slice(1), 16)
    return [(value >> 16) & 255, (value >> 8) & 255, value & 255]
  }

  function blend(from, to, amount) {
    const start = channels(from)
    const end = channels(to)
    const mixed = start.map((channel, index) => Math.round(mix(channel, end[index], amount)))
    return `rgb(${mixed.join(',')})`
  }

  const fade = (color, alpha) => `rgba(${channels(color).join(',')},${alpha})`

  // Story time
  function timeline(story) {
    const beats = story.beats
    const duration = beats[beats.length - 1].end
    function at(time) {
      const clamped = clamp(time, 0, duration)
      const found = beats.findIndex((beat) => clamped < beat.end)
      const index = found === -1 ? beats.length - 1 : found
      const beat = beats[index]
      return { index, beat, progress: span(clamped, beat.start, beat.end), local: clamped - beat.start }
    }
    return { duration, beats, at }
  }

  // Off-screen layers: paint once, stamp many times. Materials live here so they never flicker.
  function surface(width, height, paint) {
    const layer = new root.OffscreenCanvas(Math.ceil(width), Math.ceil(height))
    paint(layer.getContext('2d'), layer)
    return layer
  }

  // Lines
  function measure(points) {
    let total = 0
    const lengths = [0]
    for (let index = 1; index < points.length; index += 1) {
      total += Math.hypot(points[index][0] - points[index - 1][0], points[index][1] - points[index - 1][1])
      lengths.push(total)
    }
    return { total, lengths }
  }

  // Point at a fraction of the path, with the direction of travel there.
  function along(points, progress) {
    const { total, lengths } = measure(points)
    const wanted = total * clamp(progress)
    let index = 1
    while (index < points.length - 1 && lengths[index] < wanted) index += 1
    const from = points[index - 1]
    const to = points[index]
    const piece = lengths[index] - lengths[index - 1] || 1
    const amount = (wanted - lengths[index - 1]) / piece
    return { x: mix(from[0], to[0], amount), y: mix(from[1], to[1], amount), angle: Math.atan2(to[1] - from[1], to[0] - from[0]) }
  }

  function trace(context, points, progress) {
    if (progress <= 0) return
    const { total, lengths } = measure(points)
    const wanted = total * clamp(progress)
    context.beginPath()
    context.moveTo(points[0][0], points[0][1])
    for (let index = 1; index < points.length && lengths[index - 1] < wanted; index += 1) {
      if (lengths[index] <= wanted) context.lineTo(points[index][0], points[index][1])
      else {
        const tip = along(points, progress)
        context.lineTo(tip.x, tip.y)
      }
    }
    context.stroke()
  }

  // Split a straight run into a hand-drawn one. `shift` re-rolls the wobble: change it on a
  // stepped clock and the line boils the way redrawn animation frames do.
  function wobble(points, amount, seed, shift = 0, step = 18) {
    const result = []
    for (let index = 0; index < points.length - 1; index += 1) {
      const [startX, startY] = points[index]
      const [endX, endY] = points[index + 1]
      const count = Math.max(1, Math.round(Math.hypot(endX - startX, endY - startY) / step))
      for (let part = 0; part < count; part += 1) {
        const amountAlong = part / count
        const drift = part === 0 ? 0 : amount
        result.push([
          mix(startX, endX, amountAlong) + (noise(index + part * 0.61, shift * 3.1, seed) - 0.5) * 2 * drift,
          mix(startY, endY, amountAlong) + (noise(index + part * 0.61, shift * 3.1 + 40, seed) - 0.5) * 2 * drift,
        ])
      }
    }
    result.push(points[points.length - 1])
    return result
  }

  // Text
  function fitText(context, text, maxWidth, size, family, weight = '') {
    let fitted = size
    context.font = `${weight} ${fitted}px ${family}`.trim()
    while (context.measureText(text).width > maxWidth && fitted > 8) {
      fitted -= 1
      context.font = `${weight} ${fitted}px ${family}`.trim()
    }
    return fitted
  }

  // Camera: shake, drift and zoom applied around a focus point.
  function camera(context, view, paint) {
    const { x = 0, y = 0, zoom = 1, turn = 0, focusX = 0, focusY = 0 } = view
    context.save()
    context.translate(focusX + x, focusY + y)
    context.rotate(turn)
    context.scale(zoom, zoom)
    context.translate(-focusX, -focusY)
    paint()
    context.restore()
  }

  // Film and paper grain as a short loop of pre-rendered tiles.
  function grainTiles(width, height, seed, count = 4, strength = 26) {
    const random = stream(seed)
    return Array.from({ length: count }, () =>
      surface(width, height, (context) => {
        const image = context.createImageData(width, height)
        for (let index = 0; index < image.data.length; index += 4) {
          const shade = random.int(0, 255)
          image.data[index] = shade
          image.data[index + 1] = shade
          image.data[index + 2] = shade
          image.data[index + 3] = random.float() * strength
        }
        context.putImageData(image, 0, 0)
      }),
    )
  }

  // Styles and scenes
  const styles = {}
  const REQUIRED = ['slug', 'materials', 'showcase', 'story']

  function defineStyle(style) {
    const missing = REQUIRED.filter((key) => !style[key])
    if (missing.length > 0) throw new Error(`style is missing: ${missing.join(', ')}`)
    styles[style.slug] = style
    return style
  }

  function createScene(style, kind, options) {
    const part = style[kind]
    if (kind !== 'showcase' && kind !== 'story') throw new Error(`unknown scene kind: ${kind}`)
    const width = style.width ?? 1280
    const height = style.height ?? 720
    const seed = options.seed ?? 1
    const clock = timeline(options.story)
    const scene = {
      kind,
      part,
      width,
      height,
      seed,
      story: options.story,
      clock,
      duration: kind === 'story' ? clock.duration : part.duration,
      random: stream(seed),
      materials: null,
      beat: null,
      beatIndex: 0,
      progress: 0,
    }
    scene.materials = style.materials(scene)
    return scene
  }

  function drawFrame(scene, context, time) {
    const place = scene.clock.at(time)
    scene.beat = place.beat
    scene.beatIndex = place.index
    scene.progress = place.progress
    scene.random = stream(scene.seed)
    context.save()
    scene.part.draw(context, time, scene)
    context.restore()
  }

  // Browser player: play, pause, scrub, loop and keyboard.
  function mount(canvas, style, options) {
    const context = canvas.getContext('2d')
    let kind = options.kind ?? 'story'
    let scene = createScene(style, kind, options)
    let position = 0
    let playing = false
    let started = 0
    let audio = null

    function paint(time) {
      position = time
      drawFrame(scene, context, time)
      options.onTime?.(time, scene.duration)
    }

    function tick(now) {
      if (!playing) return
      const time = (now - started) / 1000
      if (time >= scene.duration && !options.loop) return pause()
      if (time >= scene.duration) {
        started = now
        paint(0)
        startAudio()
      } else paint(time)
      root.requestAnimationFrame(tick)
    }

    function startAudio() {
      if (!root.MotionSound || !audio) return
      audio.context?.close()
      audio.context = new root.AudioContext()
      root.MotionSound.play(audio.context, scene.part.score(scene), position)
    }

    function play() {
      playing = true
      started = root.performance.now() - position * 1000
      audio = audio ?? {}
      startAudio()
      root.requestAnimationFrame(tick)
    }

    function pause() {
      playing = false
      audio?.context?.close()
      if (audio) audio.context = null
    }

    function seek(time) {
      const wasPlaying = playing
      pause()
      paint(clamp(time, 0, scene.duration))
      if (wasPlaying) play()
    }

    function switchTo(next) {
      pause()
      kind = next
      scene = createScene(style, kind, options)
      paint(0)
    }

    root.addEventListener?.('keydown', (event) => {
      if (event.key === ' ') playing ? pause() : play()
      if (event.key === 'ArrowLeft') seek(position - 1 / 30)
      if (event.key === 'ArrowRight') seek(position + 1 / 30)
    })

    paint(0)
    return { play, pause, seek, switchTo, get scene() { return scene } }
  }

  root.Motion = {
    TAU,
    clamp,
    mix,
    remap,
    snap,
    ease,
    span,
    hit,
    stream,
    hashText,
    noise,
    fractal,
    blend,
    fade,
    timeline,
    surface,
    measure,
    along,
    trace,
    wobble,
    fitText,
    camera,
    grainTiles,
    styles,
    defineStyle,
    createScene,
    drawFrame,
    mount,
  }
})(globalThis)

```

## Reference Sound Kit (`MotionSound`)

```js
// Sound Kit, version 1.
// Sound is data: a style writes a score (voices plus timed events) and this kit plays it, live or
// offline, with the same result. Noise is seeded, so a render always sounds the same.
;(function (root) {
  'use strict'

  const START_GAP = 0.03
  const QUIET = 0.0001
  const OUTPUT_TRIM = 0.5
  const NOTE_NAMES = { C: 0, D: 2, E: 4, F: 5, G: 7, A: 9, B: 11 }
  const PITCHED = ['tone', 'fm', 'pluck', 'modal', 'thump', 'bed']
  const VOICE_KINDS = [...PITCHED, 'hiss']
  const MAX_EVENTS = 900

  function midiOf(note) {
    if (typeof note === 'number') return note
    const [, letter, accidental, octave] = /^([A-G])([#b]?)(-?\d)$/.exec(note)
    const shift = accidental === '#' ? 1 : accidental === 'b' ? -1 : 0
    return NOTE_NAMES[letter] + shift + (Number(octave) + 1) * 12
  }

  const frequency = (note) => 440 * 2 ** ((midiOf(note) - 69) / 12)

  // A scale is a function from degree to MIDI note, wrapping across octaves in both directions.
  function scale(rootNote, intervals) {
    return (degree) => {
      const octave = Math.floor(degree / intervals.length)
      const step = degree - octave * intervals.length
      return rootNote + octave * 12 + intervals[step]
    }
  }

  function seededSequence(seed) {
    let state = (seed * 2654435761) >>> 0
    return () => {
      state = (state + 0x9e3779b9) | 0
      let word = state ^ (state >>> 15)
      word = Math.imul(word, 0x2c1b3c6d)
      word ^= word >>> 12
      word = Math.imul(word, 0x297a2d39)
      return ((word ^ (word >>> 15)) >>> 0) / 4294967296
    }
  }

  function noiseBuffer(context, seconds, seed) {
    const length = Math.ceil(context.sampleRate * seconds)
    const buffer = context.createBuffer(1, length, context.sampleRate)
    const data = buffer.getChannelData(0)
    const next = seededSequence(seed)
    for (let index = 0; index < length; index += 1) data[index] = next() * 2 - 1
    return buffer
  }

  // Plucked string: a short noise burst circulates through a delay line and loses its highs.
  function pluckBuffer(context, hertz, seconds, voice, seed) {
    const length = Math.ceil(context.sampleRate * seconds)
    const buffer = context.createBuffer(1, length, context.sampleRate)
    const data = buffer.getChannelData(0)
    const period = Math.max(2, Math.round(context.sampleRate / hertz))
    const next = seededSequence(seed)
    const line = Float32Array.from({ length: period }, () => next() * 2 - 1)
    const keep = 0.5 + (voice.brightness ?? 0.5) * 0.5
    const loss = 1 - (voice.damping ?? 0.5) * 0.02
    let previous = 0
    for (let index = 0; index < length; index += 1) {
      const slot = index % period
      const current = line[slot]
      data[index] = current
      line[slot] = (current * keep + previous * (1 - keep)) * loss
      previous = current
    }
    return buffer
  }

  function roomBuffer(context, space, seed) {
    const length = Math.ceil(context.sampleRate * space.seconds)
    const buffer = context.createBuffer(2, length, context.sampleRate)
    const edge = space.seconds * 0.28
    for (let channel = 0; channel < 2; channel += 1) {
      const data = buffer.getChannelData(channel)
      const next = seededSequence(seed + channel + 1)
      for (let index = 0; index < length; index += 1) {
        data[index] = (next() * 2 - 1) * Math.exp(-(index / context.sampleRate) / edge)
      }
    }
    return buffer
  }

  function driveCurve(amount) {
    const size = 1024
    const curve = new Float32Array(size)
    const push = 1 + amount * 18
    for (let index = 0; index < size; index += 1) {
      const input = (index / (size - 1)) * 2 - 1
      curve[index] = Math.tanh(input * push) / Math.tanh(push)
    }
    return curve
  }

  function filterNode(context, type, hertz, resonance = 0.7) {
    const filter = context.createBiquadFilter()
    filter.type = type
    filter.frequency.value = hertz
    filter.Q.value = resonance
    return filter
  }

  function gainNode(context, value) {
    const gain = context.createGain()
    gain.gain.value = value
    return gain
  }

  function chain(...nodes) {
    for (let index = 0; index < nodes.length - 1; index += 1) nodes[index].connect(nodes[index + 1])
    return nodes[nodes.length - 1]
  }

  // Master bus: voices, then tone shaping, then the room, then a limiter.
  function buildMaster(context, master = {}, seed = 1) {
    const input = gainNode(context, master.gain ?? 0.8)
    const steps = [input]
    if (master.highpass) steps.push(filterNode(context, 'highpass', master.highpass))
    if (master.lowpass) steps.push(filterNode(context, 'lowpass', master.lowpass))
    if (master.drive) {
      const shaper = context.createWaveShaper()
      shaper.curve = driveCurve(master.drive)
      shaper.oversample = '2x'
      steps.push(shaper)
    }
    const tail = chain(...steps)
    const limiter = context.createDynamicsCompressor()
    limiter.threshold.value = -10
    limiter.ratio.value = 12
    limiter.attack.value = 0.004
    limiter.release.value = 0.18
    tail.connect(limiter)
    if (master.space) {
      const room = context.createConvolver()
      room.buffer = roomBuffer(context, master.space, seed)
      chain(tail, room, filterNode(context, 'lowpass', master.space.brightness ?? 4000), gainNode(context, master.space.mix ?? 0.2), limiter)
    }
    // The compressor adds its own make-up gain, so the bus is trimmed back to a safe level.
    chain(limiter, gainNode(context, OUTPUT_TRIM), context.destination)
    return input
  }

  function shapeEnvelope(param, at, peak, voice, length) {
    const attack = voice.attack ?? 0.005
    const decay = voice.decay ?? 0.3
    const sustain = voice.sustain ?? 0
    const release = voice.release ?? 0.05
    param.setValueAtTime(QUIET, at)
    param.linearRampToValueAtTime(peak, at + attack)
    param.exponentialRampToValueAtTime(Math.max(QUIET, peak * sustain), at + attack + decay)
    if (sustain <= 0) return at + attack + decay
    const end = Math.max(at + attack + decay, at + length)
    param.setValueAtTime(peak * sustain, end)
    param.exponentialRampToValueAtTime(QUIET, end + release)
    return end + release
  }

  function panned(context, output, pan) {
    if (!pan) return output
    const panner = context.createStereoPanner()
    panner.pan.value = pan
    panner.connect(output)
    return panner
  }

  function oscillator(context, wave, hertz, at, end, cents = 0) {
    const node = context.createOscillator()
    node.type = wave
    node.frequency.value = hertz
    node.detune.value = cents
    node.start(at)
    node.stop(end + 0.02)
    return node
  }

  function vibrato(context, target, voice, at, end) {
    if (!voice.vibrato) return
    const lfo = oscillator(context, 'sine', voice.vibrato.rate, at, end)
    chain(lfo, gainNode(context, voice.vibrato.cents)).connect(target.detune)
  }

  const VOICES = {
    tone(context, voice, event, at, output) {
      const amp = gainNode(context, 0)
      const end = shapeEnvelope(amp.gain, at, event.velocity, voice, event.length ?? 0.2)
      const source = oscillator(context, voice.wave ?? 'triangle', frequency(event.note), at, end, voice.detune)
      vibrato(context, source, voice, at, end)
      if (voice.glide) {
        source.frequency.setValueAtTime(frequency(event.note) * voice.glide, at)
        source.frequency.exponentialRampToValueAtTime(frequency(event.note), at + (event.length ?? 0.2))
      }
      chain(source, filterNode(context, 'lowpass', voice.cutoff ?? 4000, voice.resonance), amp, output)
    },
    fm(context, voice, event, at, output) {
      const hertz = frequency(event.note)
      const amp = gainNode(context, 0)
      const end = shapeEnvelope(amp.gain, at, event.velocity, voice, event.length ?? 0.2)
      const modulator = oscillator(context, 'sine', hertz * (voice.ratio ?? 2), at, end)
      const depth = gainNode(context, 0)
      depth.gain.setValueAtTime((voice.index ?? 100) * event.velocity, at)
      depth.gain.exponentialRampToValueAtTime(1, at + (voice.bite ?? voice.decay ?? 0.3))
      const carrier = oscillator(context, voice.wave ?? 'sine', hertz, at, end)
      chain(modulator, depth).connect(carrier.frequency)
      chain(carrier, amp, output)
    },
    pluck(context, voice, event, at, output, seed) {
      const seconds = voice.decay ?? 1
      const source = context.createBufferSource()
      source.buffer = pluckBuffer(context, frequency(event.note), seconds, voice, seed + Math.round(event.at * 1000))
      chain(source, gainNode(context, event.velocity), output)
      source.start(at)
    },
    modal(context, voice, event, at, output) {
      const hertz = frequency(event.note)
      voice.partials.forEach((ratio, index) => {
        const amp = gainNode(context, 0)
        const peak = event.velocity * (voice.gains?.[index] ?? 1 / (index + 1))
        const decay = voice.decays?.[index] ?? 1
        amp.gain.setValueAtTime(peak, at)
        amp.gain.exponentialRampToValueAtTime(QUIET, at + decay)
        chain(oscillator(context, 'sine', hertz * ratio, at, at + decay), amp, output)
      })
    },
    hiss(context, voice, event, at, output, seed) {
      const seconds = (voice.attack ?? 0.005) + (voice.decay ?? 0.2) + 0.05
      const source = context.createBufferSource()
      source.buffer = noiseBuffer(context, seconds, seed + Math.round(event.at * 1000))
      const amp = gainNode(context, 0)
      shapeEnvelope(amp.gain, at, event.velocity, voice, seconds)
      chain(source, filterNode(context, voice.filter ?? 'bandpass', voice.cutoff ?? 3000, voice.resonance ?? 1), amp, output)
      source.start(at)
    },
    thump(context, voice, event, at, output) {
      const hertz = frequency(event.note)
      const amp = gainNode(context, 0)
      const end = shapeEnvelope(amp.gain, at, event.velocity, { ...voice, attack: 0.002 }, 0)
      const source = oscillator(context, voice.wave ?? 'sine', hertz * (voice.drop ?? 3), at, end)
      source.frequency.setValueAtTime(hertz * (voice.drop ?? 3), at)
      source.frequency.exponentialRampToValueAtTime(hertz, at + (voice.bend ?? 0.05))
      chain(source, amp, output)
    },
    bed(context, voice, event, at, output) {
      const length = event.length ?? 2
      const amp = gainNode(context, 0)
      amp.gain.setValueAtTime(QUIET, at)
      amp.gain.linearRampToValueAtTime(event.velocity, at + length * 0.2)
      amp.gain.setValueAtTime(event.velocity, at + length * 0.75)
      amp.gain.exponentialRampToValueAtTime(QUIET, at + length)
      const filter = filterNode(context, 'lowpass', voice.cutoff ?? 800, voice.resonance ?? 0.7)
      const drift = oscillator(context, 'sine', voice.drift ?? 0.2, at, at + length)
      chain(drift, gainNode(context, (voice.cutoff ?? 800) * 0.35)).connect(filter.frequency)
      for (const cents of [-(voice.detune ?? 6), voice.detune ?? 6]) {
        oscillator(context, voice.wave ?? 'sawtooth', frequency(event.note), at, at + length, cents).connect(filter)
      }
      chain(filter, amp, output)
    },
  }

  function validateVoice(name, voice) {
    if (VOICE_KINDS.includes(voice.kind)) return []
    return [`voice ${name}: unknown kind ${voice.kind}`]
  }

  function validateEvent(event, index, voices) {
    const errors = []
    const voice = voices[event.voice]
    if (!voice) errors.push(`event ${index}: no voice named ${event.voice}`)
    if (!(event.at >= 0)) errors.push(`event ${index}: invalid time ${event.at}`)
    if (!(event.velocity > 0 && event.velocity <= 1)) errors.push(`event ${index}: velocity ${event.velocity} outside 0..1`)
    if (voice && PITCHED.includes(voice.kind) && event.note === undefined) errors.push(`event ${index}: missing note`)
    return errors
  }

  function validate(score) {
    const voices = score.voices ?? {}
    const events = score.events ?? []
    const errors = Object.entries(voices).flatMap(([name, voice]) => validateVoice(name, voice))
    if (events.length === 0) errors.push('score has no events')
    if (events.length > MAX_EVENTS) errors.push(`score has too many events: ${events.length}`)
    return errors.concat(events.flatMap((event, index) => validateEvent(event, index, voices)))
  }

  function play(context, score, from = 0) {
    const seed = score.seed ?? 1
    const bus = buildMaster(context, score.master, seed)
    const base = context.currentTime + START_GAP
    for (const event of score.events) {
      if (event.at < from) continue
      const voice = score.voices[event.voice]
      VOICES[voice.kind](context, voice, event, base + event.at - from, panned(context, bus, event.pan), seed)
    }
  }

  root.MotionSound = { frequency, scale, validate, play, noiseBuffer, pluckBuffer, midiOf }
})(globalThis)

```

## Reference Style & Material Implementation (`vintage-newsprint`)

```js
// Dungeon Cartographer: a map under fog. Light is knowledge, ink is permanence, the die marks turning points.
;(function () {
  const { TAU, clamp, mix, span, hit, ease, noise, surface, trace, along, wobble, fitText, stream, fade, snap } = Motion

  const W = 1280
  const H = 720
  const WORLD_W = 1920
  const WORLD_H = 1152
  const CENTER = { x: WORLD_W / 2, y: WORLD_H / 2 }
  const GRID = 32
  const PAPER = '#e9dfc6'
  const GRID_LINE = '#8fa9b8'
  const INK = '#2a2622'
  const PENCIL = '#a6322b'
  const FLAME = '#e8862a'
  const FOG = '#17161c'
  const TITLE_FONT = 'Almendra'
  const HAND_FONT = 'Kalam'
  const BPM = 72
  const BEAT = 60 / BPM

  const beatByKind = (scene, kind) => scene.story.beats.find((beat) => beat.kind === kind)
  const toGrid = (value) => Math.round(value / GRID) * GRID

  // Layout: a hub in the middle and one room per story item, on a ring snapped to the grid.
  function buildRooms(items, random) {
    return items.map((label, index) => {
      const angle = (index / items.length) * TAU - Math.PI / 2 + random.range(-0.1, 0.1)
      const width = toGrid(random.range(216, 288))
      const height = toGrid(random.range(150, 200))
      const x = toGrid(CENTER.x + Math.cos(angle) * 690 - width / 2)
      const y = toGrid(CENTER.y + Math.sin(angle) * 400 - height / 2)
      return { label, index, x, y, width, height, cx: x + width / 2, cy: y + height / 2 }
    })
  }

  function corridor(room) {
    const bendsSideways = Math.abs(room.cx - CENTER.x) > Math.abs(room.cy - CENTER.y)
    const corner = bendsSideways ? [room.cx, CENTER.y] : [CENTER.x, room.cy]
    return [[CENTER.x, CENTER.y], corner, [room.cx, room.cy]]
  }

  // Panic route: hub, room, hub, another room. Rooms are visited out of order on purpose.
  function panicRoute(rooms, random) {
    const order = rooms.map((room) => room.index).sort(() => random.float() - 0.5)
    const points = []
    for (const index of order) points.push(...corridor(rooms[index]), ...corridor(rooms[index]).reverse())
    return wobble(points, 7, 21, 0, 40)
  }

  function paintPaper(context, random) {
    context.fillStyle = PAPER
    context.fillRect(0, 0, WORLD_W, WORLD_H)
    context.strokeStyle = fade(GRID_LINE, 0.55)
    context.lineWidth = 1.2
    for (let x = 0; x <= WORLD_W; x += GRID) {
      context.beginPath()
      context.moveTo(x, 0)
      context.lineTo(x, WORLD_H)
      context.stroke()
    }
    for (let y = 0; y <= WORLD_H; y += GRID) {
      context.beginPath()
      context.moveTo(0, y)
      context.lineTo(WORLD_W, y)
      context.stroke()
    }
    for (let stain = 0; stain < 26; stain += 1) {
      const x = random.range(0, WORLD_W)
      const y = random.range(0, WORLD_H)
      const radius = random.range(50, 240)
      const mark = context.createRadialGradient(x, y, radius * 0.2, x, y, radius)
      mark.addColorStop(0, 'rgba(150,105,55,0.1)')
      mark.addColorStop(0.9, 'rgba(150,105,55,0.05)')
      mark.addColorStop(1, 'rgba(150,105,55,0)')
      context.fillStyle = mark
      context.fillRect(x - radius, y - radius, radius * 2, radius * 2)
    }
  }

  function roomPath(context, room, grow = 0) {
    context.rect(room.x - grow, room.y - grow, room.width + grow * 2, room.height + grow * 2)
  }

  function paintHatch(context, room, random) {
    context.save()
    context.beginPath()
    roomPath(context, room, 26)
    context.clip()
    context.strokeStyle = INK
    context.lineWidth = 1.5
    for (let line = 0; line < 130; line += 1) {
      const x = random.range(room.x - 44, room.x + room.width + 44)
      const y = random.range(room.y - 44, room.y + room.height + 44)
      const reach = random.range(14, 28)
      context.beginPath()
      context.moveTo(x, y)
      context.lineTo(x + reach, y - reach)
      context.stroke()
    }
    context.restore()
  }

  function paintRoomFloor(context, room, paper) {
    context.save()
    context.beginPath()
    roomPath(context, room)
    context.clip()
    context.drawImage(paper, 0, 0)
    context.restore()
    context.strokeStyle = INK
    context.lineWidth = 5
    context.strokeRect(room.x, room.y, room.width, room.height)
  }

  function paintRoomName(context, room) {
    context.fillStyle = INK
    context.textAlign = 'center'
    const size = fitText(context, room.label, room.width - 34, 34, TITLE_FONT, '700')
    context.font = `700 ${size}px ${TITLE_FONT}`
    context.fillText(room.label, room.cx, room.y + 42)
  }

  // Two layers, because corridors are inked between them: rock below, rooms on top.
  function paintGround(context, paper, rooms, hub, random) {
    context.drawImage(paper, 0, 0)
    for (const room of [...rooms, hub]) paintHatch(context, room, random)
  }

  function paintRooms(context, paper, rooms, hub) {
    for (const room of [...rooms, hub]) paintRoomFloor(context, room, paper)
    for (const room of rooms) paintRoomName(context, room)
  }

  function materials(scene) {
    const random = stream(`dungeon-${scene.seed}`)
    const rooms = buildRooms(scene.story.items, random.fork('rooms'))
    const hub = { x: CENTER.x - 96, y: CENTER.y - 80, width: 192, height: 160, cx: CENTER.x, cy: CENTER.y }
    const paper = surface(WORLD_W, WORLD_H, (context) => paintPaper(context, random.fork('paper')))
    const ground = surface(WORLD_W, WORLD_H, (context) => paintGround(context, paper, rooms, hub, random.fork('hatch')))
    const floors = surface(WORLD_W, WORLD_H, (context) => paintRooms(context, paper, rooms, hub))
    return { ground, floors, rooms, hub, panic: panicRoute(rooms, random.fork('panic')) }
  }

  function look(context, view, paint) {
    context.save()
    context.translate(W / 2, H / 2)
    context.scale(view.zoom, view.zoom)
    context.translate(-view.x, -view.y)
    paint()
    context.restore()
  }

  function flameShape(context, x, y, size, time, salt) {
    const lick = (noise(time * 5, salt, 8) - 0.5) * size * 0.8
    context.beginPath()
    context.moveTo(x - size * 0.5, y)
    context.quadraticCurveTo(x - size * 0.5, y - size * 0.8, x + lick, y - size * 1.7)
    context.quadraticCurveTo(x + size * 0.5, y - size * 0.8, x + size * 0.5, y)
    context.arc(x, y, size * 0.5, 0, Math.PI)
    context.fill()
  }

  function lantern(context, x, y, size, time, salt) {
    context.fillStyle = INK
    context.beginPath()
    context.arc(x, y + size * 0.5, size * 0.9, 0, TAU)
    context.fill()
    context.fillStyle = FLAME
    flameShape(context, x, y + size * 0.3, size, time, salt)
    context.fillStyle = PAPER
    flameShape(context, x, y + size * 0.3, size * 0.45, time, salt + 3)
  }

  function token(context, x, y, radius, fill) {
    context.fillStyle = 'rgba(23,22,28,0.35)'
    context.beginPath()
    context.ellipse(x + 5, y + 7, radius, radius, 0, 0, TAU)
    context.fill()
    context.fillStyle = fill
    context.strokeStyle = INK
    context.lineWidth = 4
    context.beginPath()
    context.arc(x, y, radius, 0, TAU)
    context.fill()
    context.stroke()
    context.fillStyle = INK
    context.beginPath()
    context.arc(x, y, radius * 0.34, 0, TAU)
    context.fill()
  }

  // Fog: a fresh sheet each frame, with soft holes burned out wherever there is fire.
  function fogSheet(view, lights, time) {
    return surface(W, H, (context) => {
      context.fillStyle = FOG
      context.fillRect(0, 0, W, H)
      context.globalCompositeOperation = 'destination-out'
      for (const light of lights) {
        const flicker = 1 + (noise(time * 6, light.salt, 2) - 0.5) * 0.09
        const radius = light.radius * flicker * view.zoom
        const x = (light.x - view.x) * view.zoom + W / 2
        const y = (light.y - view.y) * view.zoom + H / 2
        const hole = context.createRadialGradient(x, y, radius * 0.66, x, y, radius)
        hole.addColorStop(0, `rgba(0,0,0,${light.power ?? 1})`)
        hole.addColorStop(1, 'rgba(0,0,0,0)')
        context.fillStyle = hole
        context.fillRect(x - radius, y - radius, radius * 2, radius * 2)
      }
    })
  }

  function warmth(context, view, lights) {
    context.globalCompositeOperation = 'soft-light'
    for (const light of lights) {
      const radius = light.radius * view.zoom * 0.8
      const x = (light.x - view.x) * view.zoom + W / 2
      const y = (light.y - view.y) * view.zoom + H / 2
      const glow = context.createRadialGradient(x, y, 0, x, y, radius)
      glow.addColorStop(0, fade(FLAME, 0.55))
      glow.addColorStop(1, fade(FLAME, 0))
      context.fillStyle = glow
      context.fillRect(x - radius, y - radius, radius * 2, radius * 2)
    }
    context.globalCompositeOperation = 'source-over'
  }

  // The die: an icosahedron seen from above. It tumbles until `landsAt`, then shows `face`.
  function die(context, x, y, size, time, landsAt, face) {
    const rest = time >= landsAt
    const tumble = rest ? 0 : (landsAt - time) * 9
    const corners = Array.from({ length: 6 }, (_, index) => {
      const angle = (index / 6) * TAU + tumble + 0.52
      return [x + Math.cos(angle) * size, y + Math.sin(angle) * size]
    })
    context.fillStyle = 'rgba(23,22,28,0.4)'
    context.beginPath()
    context.ellipse(x + 8, y + 12, size, size * 0.9, 0, 0, TAU)
    context.fill()
    context.fillStyle = face === 1 ? PENCIL : PAPER
    context.strokeStyle = INK
    context.lineWidth = 4
    context.beginPath()
    corners.forEach(([cornerX, cornerY]) => context.lineTo(cornerX, cornerY))
    context.closePath()
    context.fill()
    context.stroke()
    context.lineWidth = 2
    context.beginPath()
    for (const index of [0, 2, 4]) {
      context.moveTo(corners[index][0], corners[index][1])
      context.lineTo(corners[(index + 2) % 6][0], corners[(index + 2) % 6][1])
    }
    context.stroke()
    if (!rest) return
    context.fillStyle = face === 1 ? PAPER : INK
    context.textAlign = 'center'
    context.font = `700 ${size * 0.72}px ${TITLE_FONT}`
    context.fillText(String(face), x, y + size * 0.25)
  }

  // The die crosses the table along a bouncing path and settles on the landing point.
  function rollingDie(context, time, start, duration, spot, face, leavesAt = Number.MAX_SAFE_INTEGER) {
    if (time < start) return
    const amount = span(time, start, start + duration, ease.outCubic)
    const gone = span(time, leavesAt, leavesAt + 0.5, ease.inCubic)
    const x = mix(spot.x - 760, spot.x, amount) + gone * 420
    const skip = Math.abs(Math.sin(amount * Math.PI * 3)) * (1 - amount) * 90
    die(context, x, spot.y - skip, 76, time, start + duration, face)
  }

  function scrap(context, text, y, font, size, write) {
    const fitted = fitText(context, text, W - 200, size, font)
    context.font = `${fitted}px ${font}`
    const width = context.measureText(text).width + 64
    const height = fitted * 1.64
    context.save()
    context.translate(W / 2, y)
    context.rotate(-0.008)
    context.fillStyle = PAPER
    context.strokeStyle = INK
    context.lineWidth = 2
    context.beginPath()
    context.moveTo(-width / 2, 0)
    for (let step = 0; step <= 12; step += 1) context.lineTo(-width / 2 + (width * step) / 12, (step % 2) * 3)
    context.lineTo(width / 2 + 4, height)
    for (let step = 12; step >= 0; step -= 1) context.lineTo(-width / 2 + (width * step) / 12, height + (step % 2) * 3)
    context.closePath()
    context.fill()
    context.stroke()
    context.beginPath()
    context.rect(-width / 2, -10, width * write, height + 20)
    context.clip()
    context.fillStyle = INK
    context.textAlign = 'center'
    context.fillText(text, 0, height * 0.71)
    context.restore()
  }

  function captionScrap(context, time, scene) {
    const { beat } = scene
    const appear = span(time, beat.start, beat.start + 0.5, ease.outCubic)
    const write = span(time, beat.start + 0.15, beat.start + 1.3, ease.inOutQuad)
    const leave = span(time, beat.end - 0.3, beat.end, ease.inQuad)
    if (appear <= 0 || leave >= 1) return
    scrap(context, beat.caption, mix(H + 20, 622, appear) + leave * 110, HAND_FONT, 38, write)
  }

  function inkCorridor(context, points, progress) {
    context.lineCap = 'square'
    context.lineJoin = 'miter'
    context.strokeStyle = INK
    context.lineWidth = 40
    trace(context, points, progress)
    context.strokeStyle = PAPER
    context.lineWidth = 28
    trace(context, points, progress)
  }

  function roomMarker(context, room, time, tension, index) {
    const at = tension.start + index * 0.12
    const pulse = hit(time, at, 0.1, 0.7)
    if (time < at) return
    context.strokeStyle = PENCIL
    context.lineWidth = 6 + pulse * 3
    context.lineCap = 'round'
    const size = 24 + pulse * 10
    context.beginPath()
    context.moveTo(room.cx - size, room.cy - size + 20)
    context.lineTo(room.cx + size, room.cy + size + 20)
    context.moveTo(room.cx + size, room.cy - size + 20)
    context.lineTo(room.cx - size, room.cy + size + 20)
    context.stroke()
  }

  function lightUpAt(room, change, count) {
    const gap = (change.end - change.start - 0.8) / count
    return change.start + 0.4 + (room.index + 1) * gap
  }

  function storyLights(scene, time, beats, runner) {
    const { rooms, hub } = scene.materials
    const shrink = span(time, beats.tension.start, beats.tension.end)
    const lights = [{ x: runner.x, y: runner.y, radius: mix(330, 240, shrink), salt: 1 }]
    lights.push({ x: hub.cx, y: hub.cy, radius: 200, salt: 2, power: 0.7 })
    const peek = span(time, beats.tension.start, beats.tension.start + 1.2, ease.outCubic)
    for (const room of rooms) {
      const litAt = lightUpAt(room, beats.change, rooms.length)
      const lit = span(time, litAt, litAt + 0.5, ease.outBack)
      if (lit > 0) lights.push({ x: room.cx, y: room.cy, radius: 340 * lit, salt: 10 + room.index })
      else if (peek > 0) lights.push({ x: room.cx, y: room.cy, radius: 250 * peek, salt: 10 + room.index, power: 0.62 })
    }
    return lights
  }

  function runnerPosition(scene, time, beats) {
    const { panic } = scene.materials
    if (time < beats.tension.start) return { x: CENTER.x, y: CENTER.y }
    if (time >= beats.change.start) {
      const home = span(time, beats.change.start, beats.change.start + 0.6, ease.inOutCubic)
      const last = along(panic, 1)
      return { x: mix(last.x, CENTER.x, home), y: mix(last.y, CENTER.y, home) }
    }
    const rush = span(time, beats.tension.start + 0.5, beats.change.start - 0.3, ease.inQuad)
    const point = along(panic, rush)
    return { x: point.x, y: point.y, rush }
  }

  function storyView(scene, time, beats, runner) {
    const pullOut = span(time, beats.tension.start, beats.tension.start + 1.4, ease.inOutCubic)
    const reveal = span(time, beats.result.start - 0.4, beats.result.start + 1.6, ease.inOutCubic)
    const zoom = mix(mix(1.7, 0.88, pullOut), 0.6, reveal)
    const shake = hit(time, beats.change.start - BEAT * 0.5, 0.02, 0.4) * 16
    return {
      zoom,
      x: mix(CENTER.x, mix(runner.x, CENTER.x, 0.72), pullOut) + noise(time * 22, 1, 4) * shake,
      y: mix(CENTER.y, mix(runner.y, CENTER.y, 0.72), pullOut) + reveal * 46 + noise(time * 22, 5, 4) * shake,
    }
  }

  function drawStoryWorld(context, scene, time, beats, runner) {
    const { ground, floors, rooms, panic } = scene.materials
    context.drawImage(ground, 0, 0)
    for (const room of rooms) {
      const inkAt = lightUpAt(room, beats.change, rooms.length) - 0.42
      const inked = span(time, inkAt, inkAt + 0.4, ease.inOutCubic)
      if (inked > 0) inkCorridor(context, corridor(room), inked)
    }
    context.drawImage(floors, 0, 0)
    const fadeOut = 1 - span(time, beats.change.start, beats.change.end - 1, ease.inQuad)
    if (runner.rush !== undefined || fadeOut < 1) {
      context.strokeStyle = fade(PENCIL, 0.85 * fadeOut)
      context.lineWidth = 3
      context.lineCap = 'round'
      trace(context, panic, runner.rush ?? 1)
    }
    drawRoomLife(context, scene, time, beats)
    token(context, runner.x, runner.y, 19, PAPER)
    lantern(context, runner.x, runner.y - 34, 11, time, 1)
  }

  function drawRoomLife(context, scene, time, beats) {
    for (const room of scene.materials.rooms) {
      const litAt = lightUpAt(room, beats.change, scene.materials.rooms.length)
      if (time < litAt) {
        roomMarker(context, room, time, beats.tension, room.index)
        continue
      }
      const orbit = time * 1.1 + room.index
      lantern(context, room.cx, room.cy - 8, 15, time, 20 + room.index)
      token(context, room.cx + Math.cos(orbit) * 58, room.cy + 30 + Math.sin(orbit) * 22, 13, GRID_LINE)
    }
  }

  function drawStoryFilm(context, time, scene) {
    const beats = {
      tension: beatByKind(scene, 'tension'),
      change: beatByKind(scene, 'change'),
      result: beatByKind(scene, 'result'),
    }
    const runner = runnerPosition(scene, time, beats)
    const view = storyView(scene, time, beats, runner)
    const lights = storyLights(scene, time, beats, runner)
    context.fillStyle = FOG
    context.fillRect(0, 0, W, H)
    look(context, view, () => drawStoryWorld(context, scene, time, beats, runner))
    warmth(context, view, lights)
    context.drawImage(fogSheet(view, lights, time), 0, 0)
    rollingDie(context, time, beats.change.start - BEAT * 2, BEAT * 1.5, { x: 1110, y: 150 }, 1, beats.change.start + BEAT)
    rollingDie(context, time, beats.result.start, BEAT * 1.5, { x: 1176, y: 112 }, 20)
    captionScrap(context, time, scene)
  }

  function drawStory(context, time, scene) {
    drawStoryFilm(context, time, scene)
    const closing = span(time, scene.duration - 0.5, scene.duration)
    if (closing > 0) {
      context.fillStyle = fade(FOG, closing)
      context.fillRect(0, 0, W, H)
    }
  }

  function drawShowcase(context, time, scene) {
    const { ground, floors, rooms } = scene.materials
    const spin = (time / scene.duration) * 3
    const route = corridor(rooms[Math.floor(spin) % rooms.length])
    const step = spin - Math.floor(spin)
    const point = along(route, step < 0.5 ? step * 2 : 2 - step * 2)
    const snapped = { x: snap(point.x, GRID) + GRID / 2, y: snap(point.y, GRID) + GRID / 2 }
    const view = { zoom: 1.05, x: mix(CENTER.x, snapped.x, 0.82), y: mix(CENTER.y, snapped.y, 0.82) }
    const lights = [
      { x: snapped.x, y: snapped.y, radius: 400, salt: 1 },
      { x: CENTER.x, y: CENTER.y, radius: 300, salt: 2, power: 0.8 },
      ...rooms.map((room) => ({ x: room.cx, y: room.cy, radius: 280, salt: 10 + room.index, power: 0.72 })),
    ]
    context.fillStyle = FOG
    context.fillRect(0, 0, W, H)
    look(context, view, () => {
      context.drawImage(ground, 0, 0)
      context.drawImage(floors, 0, 0)
      token(context, snapped.x, snapped.y, 19, PAPER)
      lantern(context, snapped.x, snapped.y - 34, 11, time, 1)
    })
    warmth(context, view, lights)
    context.drawImage(fogSheet(view, lights, time), 0, 0)
    scrap(context, 'Dungeon Cartographer', 586, `${TITLE_FONT}`, 70, 1)
    const edge = Math.min(span(time, 0, 0.5), 1 - span(time, scene.duration - 0.5, scene.duration))
    context.fillStyle = fade(FOG, 1 - edge)
    context.fillRect(0, 0, W, H)
    rollingDie(context, time, 1, BEAT * 1.5, { x: 1120, y: 150 }, 20)
  }

  // Sound: a stone room. The piece stays in D phrygian until the change, then lands on a D major chord.
  const VOICES = {
    dulcimer: { kind: 'pluck', damping: 0.25, brightness: 0.85, decay: 1.6 },
    drone: { kind: 'bed', wave: 'sawtooth', detune: 7, cutoff: 340, drift: 0.13 },
    footfall: { kind: 'thump', drop: 2.2, bend: 0.04, decay: 0.16 },
    clatter: { kind: 'modal', partials: [1, 2.32, 4.17, 6.9], gains: [1, 0.7, 0.4, 0.2], decays: [0.09, 0.07, 0.05, 0.03] },
    quill: { kind: 'hiss', filter: 'highpass', cutoff: 5200, attack: 0.03, decay: 0.34 },
    chime: { kind: 'fm', ratio: 3.01, index: 190, attack: 0.002, decay: 2.2, bite: 0.5 },
    choir: { kind: 'bed', wave: 'triangle', detune: 5, cutoff: 1500, drift: 0.2 },
  }

  const MASTER = { gain: 0.8, highpass: 40, lowpass: 7800, space: { seconds: 2.8, brightness: 2600, mix: 0.34 } }
  const PHRYGIAN = MotionSound.scale(50, [0, 1, 3, 5, 7, 8, 10])
  const WALK = [0, 2, 1, 4, 3, 1, 2, 0, 5, 4, 2, 1]

  function dieClatter(events, landsAt, random) {
    for (let bounce = 0; bounce < 8; bounce += 1) {
      const at = landsAt - 0.92 * (1 - bounce / 8) ** 1.7
      events.push({ at, voice: 'clatter', note: 74 + random.int(-3, 6), velocity: 0.34 + bounce * 0.05, pan: -0.5 + bounce * 0.1 })
    }
  }

  function dulcimerLine(events, from, to, step, intensity) {
    let count = 0
    for (let at = from; at < to; at += step) {
      events.push({ at, voice: 'dulcimer', note: PHRYGIAN(WALK[count % WALK.length] + 7), velocity: 0.4 * intensity, pan: (count % 2) * 0.5 - 0.25 })
      count += 1
    }
  }

  function storyScore(scene) {
    const tension = beatByKind(scene, 'tension')
    const change = beatByKind(scene, 'change')
    const result = beatByKind(scene, 'result')
    const rooms = scene.story.items
    const random = stream(scene.seed + 9)
    const events = [{ at: 0, voice: 'drone', note: 38, velocity: 0.5, length: result.start + 1 }]
    dulcimerLine(events, 0.4, tension.start, BEAT, 0.7)
    dulcimerLine(events, tension.start, change.start - BEAT, BEAT / 2, 1)
    for (let at = tension.start; at < change.start - BEAT; at += mix(0.5, 0.24, (at - tension.start) / (change.start - tension.start))) {
      events.push({ at, voice: 'footfall', note: 40, velocity: 0.55 })
    }
    dieClatter(events, change.start - BEAT * 0.5, random)
    events.push({ at: change.start - BEAT * 0.5, voice: 'footfall', note: 31, velocity: 0.9 })
    rooms.forEach((_, index) => {
      const litAt = lightUpAt({ index }, change, rooms.length)
      events.push({ at: litAt - 0.42, voice: 'quill', velocity: 0.28, pan: Math.sin(index * 1.8) * 0.6 })
      events.push({ at: litAt, voice: 'chime', note: PHRYGIAN(index + 7), velocity: 0.34, pan: Math.sin(index * 1.8) * 0.6 })
    })
    dieClatter(events, result.start + BEAT * 1.5, random)
    for (const [note, velocity] of [[38, 0.45], [50, 0.4], [54, 0.34], [57, 0.32], [62, 0.28]]) {
      events.push({ at: result.start + BEAT * 1.5, voice: 'choir', note, velocity, length: scene.duration - result.start - BEAT * 1.5 })
    }
    for (const note of [74, 78, 81, 86]) {
      events.push({ at: result.start + BEAT * 1.5 + (note - 74) * 0.03, voice: 'chime', note, velocity: 0.36 })
    }
    return { seed: scene.seed, master: MASTER, voices: VOICES, events }
  }

  function showcaseScore(scene) {
    const random = stream(scene.seed + 3)
    const events = [{ at: 0, voice: 'drone', note: 38, velocity: 0.5, length: scene.duration }]
    dulcimerLine(events, 0.2, scene.duration - 0.6, BEAT / 2, 0.8)
    dieClatter(events, 1 + BEAT * 1.5, random)
    events.push({ at: 1 + BEAT * 1.5, voice: 'chime', note: 74, velocity: 0.4 })
    return { seed: scene.seed, master: MASTER, voices: VOICES, events }
  }

  Motion.defineStyle({
    slug: 'atlas-substrate-cartography',
    materials,
    showcase: { duration: BEAT * 8, draw: drawShowcase, score: showcaseScore },
    story: { draw: drawStory, score: storyScore },
  })
})()


// Kintsugi Repair: one bowl. It cracks, opens, and the gold returns along the same paths.
;(function () {
  const { TAU, clamp, mix, span, hit, ease, noise, surface, along, fitText, stream, fade } = Motion

  const W = 1280
  const H = 720
  const BOWL_X = 500
  const BOWL_Y = 360
  const BOWL_R = 268
  const CAPTION_X = 936
  const LACQUER = '#14161f'
  const GLAZE = '#efe7d6'
  const IRON = '#6b3a22'
  const CLAY = '#c9b79c'
  const GOLD = '#d4a72c'
  const GOLD_LIGHT = '#fff0b8'
  const FONT = 'Shippori Mincho'
  const BPM = 54
  const BEAT = 60 / BPM

  const beatByKind = (scene, kind) => scene.story.beats.find((beat) => beat.kind === kind)

  // A crack runs from the rim to the center in jagged steps.
  function buildCrack(angle, random) {
    const points = []
    const steps = 11
    for (let step = 0; step <= steps; step += 1) {
      const amount = 1 - step / steps
      const swing = step === 0 || step === steps ? 0 : random.range(-0.13, 0.13) * (0.4 + amount)
      const radius = amount * BOWL_R
      points.push([BOWL_X + Math.cos(angle + swing) * radius, BOWL_Y + Math.sin(angle + swing) * radius])
    }
    return points
  }

  function buildBranch(crack, random) {
    const start = crack[random.int(3, 7)]
    const angle = random.range(0, TAU)
    const length = random.range(26, 70)
    return [start, [start[0] + Math.cos(angle) * length * 0.5, start[1] + Math.sin(angle) * length * 0.5], [start[0] + Math.cos(angle + 0.5) * length, start[1] + Math.sin(angle + 0.5) * length]]
  }

  function buildCracks(items, random) {
    return items.map((label, index) => {
      const angle = (index / items.length) * TAU - Math.PI / 2 + random.range(-0.08, 0.08)
      const path = buildCrack(angle, random)
      return { label, index, angle, path, branches: [buildBranch(path, random), buildBranch(path, random)] }
    })
  }

  function paintTable(context, random) {
    context.fillStyle = LACQUER
    context.fillRect(0, 0, W, H)
    const pool = context.createRadialGradient(BOWL_X - 80, BOWL_Y - 120, 40, BOWL_X, BOWL_Y, 760)
    pool.addColorStop(0, 'rgba(92,98,130,0.5)')
    pool.addColorStop(1, 'rgba(20,22,31,0)')
    context.fillStyle = pool
    context.fillRect(0, 0, W, H)
    context.strokeStyle = 'rgba(160,170,210,0.05)'
    context.lineWidth = 1
    for (let line = 0; line < 70; line += 1) {
      const y = random.range(0, H)
      context.beginPath()
      context.moveTo(0, y)
      context.bezierCurveTo(400, y + random.range(-20, 20), 800, y + random.range(-20, 20), W, y + random.range(-12, 12))
      context.stroke()
    }
  }

  function speckle(context, random) {
    for (let index = 0; index < 900; index += 1) {
      const angle = random.range(0, TAU)
      const radius = Math.sqrt(random.float()) * BOWL_R
      context.fillStyle = random.chance(0.8) ? 'rgba(107,58,34,0.2)' : 'rgba(40,30,28,0.3)'
      context.beginPath()
      context.arc(BOWL_X + Math.cos(angle) * radius, BOWL_Y + Math.sin(angle) * radius, random.range(0.4, 1.8), 0, TAU)
      context.fill()
    }
  }

  function paintBowl(context, random) {
    const body = context.createRadialGradient(BOWL_X + 40, BOWL_Y + 60, 30, BOWL_X, BOWL_Y, BOWL_R)
    body.addColorStop(0, '#d9cdb6')
    body.addColorStop(0.32, GLAZE)
    body.addColorStop(0.78, '#e4d8c3')
    body.addColorStop(0.93, '#b6946f')
    body.addColorStop(1, IRON)
    context.fillStyle = body
    context.beginPath()
    context.arc(BOWL_X, BOWL_Y, BOWL_R, 0, TAU)
    context.fill()
    speckle(context, random)
    context.strokeStyle = 'rgba(107,58,34,0.26)'
    context.lineWidth = 2.5
    context.beginPath()
    context.arc(BOWL_X, BOWL_Y, 92, 0, TAU)
    context.stroke()
    context.strokeStyle = IRON
    context.lineWidth = 7
    context.beginPath()
    context.arc(BOWL_X, BOWL_Y, BOWL_R - 3, 0, TAU)
    context.stroke()
  }

  function materials(scene) {
    const random = stream(`kintsugi-${scene.seed}`)
    return {
      table: surface(W, H, (context) => paintTable(context, random.fork('table'))),
      bowl: surface(W, H, (context) => paintBowl(context, random.fork('bowl'))),
      cracks: buildCracks(scene.story.items, random.fork('cracks')),
    }
  }

  function castShadow(context, offset) {
    const blur = context.createRadialGradient(BOWL_X + 22, BOWL_Y + 30, BOWL_R * 0.6, BOWL_X + 22, BOWL_Y + 30, BOWL_R * (1.28 + offset))
    blur.addColorStop(0, 'rgba(4,5,10,0.85)')
    blur.addColorStop(1, 'rgba(4,5,10,0)')
    context.fillStyle = blur
    context.fillRect(0, 0, W, H)
  }

  // One wedge of the bowl: from this crack, along the rim, back down the next crack.
  function wedgePath(context, crack, next) {
    context.beginPath()
    crack.path.forEach(([x, y]) => context.lineTo(x, y))
    context.closePath()
    context.beginPath()
    context.moveTo(crack.path[0][0], crack.path[0][1])
    const end = next.angle < crack.angle ? next.angle + TAU : next.angle
    context.arc(BOWL_X, BOWL_Y, BOWL_R + 1, crack.angle, end)
    for (const [x, y] of [...next.path]) context.lineTo(x, y)
    for (const [x, y] of [...crack.path].reverse()) context.lineTo(x, y)
    context.closePath()
  }

  function drawShard(context, scene, crack, next, open) {
    const middle = crack.angle + TAU / scene.materials.cracks.length / 2
    const push = open * (26 + (crack.index % 3) * 12)
    context.save()
    context.translate(Math.cos(middle) * push, Math.sin(middle) * push)
    context.translate(BOWL_X, BOWL_Y)
    context.rotate(open * ((crack.index % 2) * 2 - 1) * 0.035)
    context.translate(-BOWL_X, -BOWL_Y)
    wedgePath(context, crack, next)
    context.strokeStyle = CLAY
    context.lineWidth = open > 0 ? 7 : 0.1
    context.lineJoin = 'round'
    context.stroke()
    context.clip()
    context.drawImage(scene.materials.bowl, 0, 0)
    context.restore()
  }

  function drawBowl(context, scene, open) {
    const { cracks, bowl } = scene.materials
    if (open <= 0) {
      context.drawImage(bowl, 0, 0)
      return
    }
    cracks.forEach((crack, index) => drawShard(context, scene, crack, cracks[(index + 1) % cracks.length], open))
  }

  function drawHairline(context, path, progress) {
    context.strokeStyle = '#2e2420'
    context.lineWidth = 1.7
    context.lineJoin = 'miter'
    Motion.trace(context, path, progress)
  }

  // Gold is laid in short strokes whose width follows noise, the way a brush loads and lifts.
  function seamSegments(context, points, progress, widthScale, color) {
    const { total, lengths } = Motion.measure(points)
    const reach = total * clamp(progress)
    context.strokeStyle = color
    context.lineCap = 'round'
    for (let index = 1; index < points.length && lengths[index - 1] < reach; index += 1) {
      const [startX, startY] = points[index - 1]
      const tip = lengths[index] <= reach ? { x: points[index][0], y: points[index][1] } : along(points, progress)
      context.lineWidth = (3.6 + noise(index * 0.8, startY * 0.01, 4) * 6.4) * widthScale
      context.beginPath()
      context.moveTo(startX, startY)
      context.lineTo(tip.x, tip.y)
      context.stroke()
    }
  }

  function drawGold(context, points, progress, shine) {
    if (progress <= 0) return
    context.save()
    context.shadowColor = fade(GOLD, 0.8)
    context.shadowBlur = 10 + shine * 26
    seamSegments(context, points, progress, 1, GOLD)
    context.restore()
    seamSegments(context, points, progress, 0.36, GOLD_LIGHT)
    if (progress >= 1) return
    const head = along(points, progress)
    context.fillStyle = GOLD_LIGHT
    context.beginPath()
    context.arc(head.x, head.y, 6.5, 0, TAU)
    context.fill()
  }

  // The window highlight: a soft band that glides across the glaze.
  function highlight(context, position, power) {
    context.save()
    context.beginPath()
    context.arc(BOWL_X, BOWL_Y, BOWL_R - 8, 0, TAU)
    context.clip()
    context.globalCompositeOperation = 'screen'
    const x = BOWL_X - BOWL_R + position * BOWL_R * 2
    const band = context.createLinearGradient(x - 90, BOWL_Y - 240, x + 90, BOWL_Y + 240)
    band.addColorStop(0, 'rgba(255,250,235,0)')
    band.addColorStop(0.5, `rgba(255,250,235,${power})`)
    band.addColorStop(1, 'rgba(255,250,235,0)')
    context.fillStyle = band
    context.fillRect(0, 0, W, H)
    context.restore()
  }

  function labelSpot(crack) {
    const distance = BOWL_R + 26
    return { x: BOWL_X + Math.cos(crack.angle) * distance, y: BOWL_Y + Math.sin(crack.angle) * distance }
  }

  function drawLabel(context, crack, reveal, tone) {
    if (reveal <= 0) return
    const { x, y } = labelSpot(crack)
    const toRight = Math.cos(crack.angle) >= -0.1
    context.save()
    context.globalAlpha = reveal
    context.fillStyle = tone
    context.textAlign = toRight ? 'left' : 'right'
    const size = fitText(context, crack.label, 134, 22, FONT, '500')
    context.font = `500 ${size}px ${FONT}`
    const lift = Math.sin(crack.angle) < -0.6 ? -4 : 8
    context.fillText(crack.label, x, y + lift)
    context.restore()
  }

  function wrapLines(context, text, maxWidth) {
    const lines = []
    let line = ''
    for (const word of text.split(' ')) {
      const candidate = line ? `${line} ${word}` : word
      if (context.measureText(candidate).width > maxWidth && line) {
        lines.push(line)
        line = word
      } else line = candidate
    }
    lines.push(line)
    return lines
  }

  function caption(context, time, scene) {
    const { beat } = scene
    const appear = span(time, beat.start + 0.1, beat.start + 1, ease.inOutQuad)
    const leave = span(time, beat.end - 0.6, beat.end - 0.05, ease.inQuad)
    if (appear <= 0 || leave >= 1) return
    context.save()
    context.globalAlpha = appear * (1 - leave)
    context.fillStyle = GLAZE
    context.textAlign = 'left'
    context.font = `500 44px ${FONT}`
    const lines = wrapLines(context, beat.caption, 310)
    const top = BOWL_Y - ((lines.length - 1) * 60) / 2 + 10
    lines.forEach((line, index) => context.fillText(line, CAPTION_X, top + index * 60))
    context.restore()
  }

  function crackTiming(crack, tension, count) {
    const gap = (tension.end - tension.start - BEAT * 1.2) / count
    return tension.start + crack.index * gap
  }

  function goldTiming(crack, change, count) {
    const gap = (change.end - change.start - 1.6) / count
    return change.start + 0.5 + crack.index * gap
  }

  function drawCracks(context, scene, time, tension, change) {
    const { cracks } = scene.materials
    const remaining = 1 - span(time, change.start + 0.4, change.end, ease.linear)
    for (const crack of cracks) {
      const at = crackTiming(crack, tension, cracks.length)
      const grown = span(time, at, at + 0.34, ease.outQuad)
      if (grown <= 0 || remaining <= 0) continue
      context.globalAlpha = remaining
      drawHairline(context, crack.path, grown)
      for (const branch of crack.branches) drawHairline(context, branch, span(time, at + 0.2, at + 0.5))
      context.globalAlpha = 1
    }
  }

  function drawSeams(context, scene, time, change, shine) {
    const { cracks } = scene.materials
    for (const crack of cracks) {
      const at = goldTiming(crack, change, cracks.length)
      const route = [...crack.path].reverse()
      drawGold(context, route, span(time, at, at + 0.9, ease.inOutQuad), shine)
      for (const branch of crack.branches) drawGold(context, branch, span(time, at + 0.7, at + 1), shine)
    }
  }

  function drawLabels(context, scene, time, tension, change) {
    const { cracks } = scene.materials
    for (const crack of cracks) {
      const cracked = span(time, crackTiming(crack, tension, cracks.length), crackTiming(crack, tension, cracks.length) + 0.4)
      const gilded = span(time, goldTiming(crack, change, cracks.length) + 0.6, goldTiming(crack, change, cracks.length) + 1.1)
      drawLabel(context, crack, cracked, gilded > 0 ? GOLD : CLAY)
    }
  }

  function storyCamera(time, beats) {
    const lean = span(time, 0, beats.change.start, ease.inOutQuad) * 0.05
    const release = span(time, beats.change.start, beats.result.end, ease.inOutCubic) * 0.09
    const quake = hit(time, beats.change.start - 0.1, 0.03, 0.5)
    return {
      zoom: 1 + lean - release,
      x: noise(time * 30, 2, 7) * quake * 12 - quake * 6,
      y: noise(time * 30, 8, 7) * quake * 12 - quake * 6,
    }
  }

  function drawStory(context, time, scene) {
    const beats = {
      tension: beatByKind(scene, 'tension'),
      change: beatByKind(scene, 'change'),
      result: beatByKind(scene, 'result'),
    }
    const breakAt = beats.tension.end - 0.2
    const opened = span(time, breakAt, breakAt + 1, ease.outCubic)
    const closed = span(time, beats.change.start + 1, beats.change.end - 0.5, ease.inOutCubic)
    const open = opened * (1 - closed)
    const sweep = span(time, beats.result.start + 0.2, beats.result.end - 0.8, ease.inOutQuad)
    const shine = hit(time, mix(beats.result.start + 0.2, beats.result.end - 0.8, 0.45), 0.8, 1.2)
    const view = storyCamera(time, beats)
    context.drawImage(scene.materials.table, 0, 0)
    Motion.camera(context, { ...view, focusX: BOWL_X, focusY: BOWL_Y }, () => {
      castShadow(context, open * 0.12)
      drawBowl(context, scene, open)
      drawCracks(context, scene, time, beats.tension, beats.change)
      drawSeams(context, scene, time, beats.change, shine)
      highlight(context, mix(0.18, 0.28, span(time, 0, beats.result.start)) + sweep * 0.72, 0.22 + shine * 0.42)
      drawLabels(context, scene, time, beats.tension, beats.change)
    })
    caption(context, time, scene)
    const edge = Math.min(span(time, 0, 0.8), 1 - span(time, scene.duration - 0.7, scene.duration))
    context.fillStyle = fade(LACQUER, 1 - edge)
    context.fillRect(0, 0, W, H)
  }

  function drawShowcase(context, time, scene) {
    const { cracks } = scene.materials
    const pour = time / scene.duration
    context.drawImage(scene.materials.table, 0, 0)
    castShadow(context, 0)
    drawBowl(context, scene, 0)
    cracks.forEach((crack, index) => {
      const route = [...crack.path].reverse()
      const start = (index / cracks.length) * 0.55
      drawGold(context, route, span(pour, start, start + 0.4, ease.inOutQuad), hit(pour, 0.72, 0.08, 0.2))
    })
    highlight(context, 0.1 + pour * 0.85, 0.3)
    context.fillStyle = GLAZE
    context.textAlign = 'left'
    context.font = `500 56px ${FONT}`
    context.fillText('Kintsugi', CAPTION_X, 342)
    context.fillText('Repair', CAPTION_X, 412)
    const edge = Math.min(span(time, 0, 0.6), 1 - span(time, scene.duration - 0.6, scene.duration))
    context.fillStyle = fade(LACQUER, 1 - edge)
    context.fillRect(0, 0, W, H)
  }

  // Sound: bare ceramic against a long, quiet room. The gold is a singing bowl that keeps ringing.
  const VOICES = {
    ping: { kind: 'modal', partials: [1, 2.71, 5.19, 8.42], gains: [1, 0.55, 0.3, 0.16], decays: [0.5, 0.3, 0.16, 0.08] },
    crackle: { kind: 'hiss', filter: 'highpass', cutoff: 4200, attack: 0.001, decay: 0.03 },
    shatter: { kind: 'hiss', filter: 'bandpass', cutoff: 2100, resonance: 0.8, attack: 0.001, decay: 0.42 },
    knock: { kind: 'thump', drop: 1.8, bend: 0.03, decay: 0.28 },
    koto: { kind: 'pluck', damping: 0.32, brightness: 0.8, decay: 2 },
    singing: { kind: 'modal', partials: [1, 2.76, 5.4], gains: [0.8, 0.35, 0.14], decays: [6, 4, 2] },
    breath: { kind: 'tone', wave: 'sine', attack: 0.5, decay: 0.3, sustain: 0.7, release: 0.9, cutoff: 1400, glide: 0.94, vibrato: { rate: 4.4, cents: 12 } },
    pour: { kind: 'hiss', filter: 'lowpass', cutoff: 700, attack: 0.3, decay: 0.8 },
  }

  const MASTER = { gain: 1.7, highpass: 50, lowpass: 9000, space: { seconds: 3.6, brightness: 3200, mix: 0.42 } }
  const IN_SCALE = MotionSound.scale(62, [0, 1, 5, 7, 8])

  function shatterCluster(events, at, random) {
    events.push({ at, voice: 'shatter', velocity: 0.42 }, { at, voice: 'knock', note: 38, velocity: 0.5 })
    for (let piece = 0; piece < 16; piece += 1) {
      const offset = random.range(0, 0.7) ** 2
      events.push({ at: at + offset, voice: 'ping', note: 76 + random.int(-5, 14), velocity: random.range(0.1, 0.28) * (1 - offset), pan: random.range(-0.7, 0.7) })
    }
  }

  function storyScore(scene) {
    const tension = beatByKind(scene, 'tension')
    const change = beatByKind(scene, 'change')
    const result = beatByKind(scene, 'result')
    const { cracks } = scene.materials
    const random = stream(scene.seed + 31)
    const events = [
      { at: 0.5, voice: 'koto', note: IN_SCALE(5), velocity: 0.5 },
      { at: 1.6, voice: 'koto', note: IN_SCALE(7), velocity: 0.4, pan: 0.2 },
      { at: 1.4, voice: 'breath', note: IN_SCALE(3), velocity: 0.1, length: 1.3 },
    ]
    for (const crack of cracks) {
      const at = crackTiming(crack, tension, cracks.length)
      events.push({ at, voice: 'ping', note: 84 + crack.index * 2, velocity: 0.38, pan: Math.cos(crack.angle) * 0.6 })
      for (let tick = 0; tick < 6; tick += 1) {
        events.push({ at: at + random.range(0, 0.34), voice: 'crackle', velocity: random.range(0.08, 0.26), pan: Math.cos(crack.angle) * 0.6 })
      }
    }
    shatterCluster(events, tension.end - 0.2, random)
    cracks.forEach((crack) => {
      const at = goldTiming(crack, change, cracks.length)
      events.push({ at, voice: 'singing', note: IN_SCALE(crack.index), velocity: 0.4, pan: Math.cos(crack.angle) * 0.5 })
      events.push({ at, voice: 'pour', velocity: 0.1 })
    })
    const resolve = mix(result.start + 0.2, result.end - 0.8, 0.45)
    events.push({ at: result.start + 0.1, voice: 'koto', note: IN_SCALE(0), velocity: 0.42 })
    events.push({ at: result.start + 0.5, voice: 'koto', note: IN_SCALE(3), velocity: 0.42, pan: -0.2 })
    events.push({ at: resolve, voice: 'singing', note: 50, velocity: 0.42 }, { at: resolve, voice: 'singing', note: 62, velocity: 0.3 })
    events.push({ at: resolve + 0.3, voice: 'koto', note: IN_SCALE(5), velocity: 0.42, pan: 0.2 })
    return { seed: scene.seed, master: MASTER, voices: VOICES, events }
  }

  function showcaseScore(scene) {
    const { cracks } = scene.materials
    const events = cracks.map((crack, index) => ({
      at: (index / cracks.length) * 0.55 * scene.duration + 0.1,
      voice: 'singing',
      note: IN_SCALE(index),
      velocity: 0.42,
      pan: Math.cos(crack.angle) * 0.5,
    }))
    events.push({ at: scene.duration * 0.72, voice: 'koto', note: IN_SCALE(5), velocity: 0.5 })
    return { seed: scene.seed, master: MASTER, voices: VOICES, events }
  }

  Motion.defineStyle({
    slug: 'atlas-substrate-fracture',
    materials,
    showcase: { duration: BEAT * 6, draw: drawShowcase, score: showcaseScore },
    story: { draw: drawStory, score: storyScore },
  })
})()


// Vintage Newsprint 1950s Halftone & Broadsheet Engine
;(function () {
  const { TAU, clamp, mix, span, hit, ease, noise, surface, trace, along, wobble, fitText, stream, fade } = Motion

  const W = 1280
  const H = 720
  const DESK = '#231f1c'
  const PAPER = '#efe6d2'
  const PAPER_EDGE = '#dacbad'
  const INK = '#1e1c1a'
  const BLEED = '#6e7885'
  const WAX_RED = '#c83228'

  function paintNewsprintSheet(ctx, width, height, seed) {
    ctx.fillStyle = DESK
    ctx.fillRect(0, 0, width, height)
    const sx = 54
    const sy = 32
    const sw = width - 108
    const sh = height - 64

    const g = ctx.createRadialGradient(width * 0.5, height * 0.5, sh * 0.25, width * 0.5, height * 0.5, sw * 0.65)
    g.addColorStop(0, PAPER)
    g.addColorStop(1, PAPER_EDGE)
    ctx.fillStyle = g
    ctx.fillRect(sx, sy, sw, sh)

    // Reverse-page show-through simulation (7.5% alpha mirrored blocks)
    ctx.fillStyle = fade(BLEED, 0.075)
    for (let c = 0; c < 5; c += 1) {
      const cx = sx + 36 + c * 218
      ctx.fillRect(cx, sy + 90, 190, 28)
      for (let r = 0; r < 14; r += 1) {
        ctx.fillRect(cx, sy + 135 + r * 32, 184, 14)
      }
    }

    // Center fold crease
    ctx.strokeStyle = fade('#b5a485', 0.45)
    ctx.lineWidth = 2
    ctx.beginPath()
    ctx.moveTo(sx, height * 0.5)
    ctx.lineTo(sx + sw, height * 0.5)
    ctx.stroke()

    // Outer double editorial rule
    ctx.strokeStyle = INK
    ctx.lineWidth = 3
    ctx.strokeRect(sx + 18, sy + 18, sw - 36, sh - 36)
    ctx.lineWidth = 1
    ctx.strokeRect(sx + 24, sy + 24, sw - 47, sh - 47)
  }

  function paintHalftoneBox(ctx, x, y, w, h, darknessFn, cell = 6) {
    ctx.save()
    ctx.beginPath()
    ctx.rect(x, y, w, h)
    ctx.clip()
    ctx.fillStyle = INK
    const cos45 = Math.SQRT1_2
    const sin45 = Math.SQRT1_2
    const diag = Math.hypot(w, h)
    const cx = x + w * 0.5
    const cy = y + h * 0.5
    for (let u = -diag * 0.6; u <= diag * 0.6; u += cell) {
      for (let v = -diag * 0.6; v <= diag * 0.6; v += cell) {
        const px = cx + u * cos45 - v * sin45
        const py = cy + u * sin45 + v * cos45
        if (px < x || px > x + w || py < y || py > y + h) continue
        const dk = clamp(darknessFn((px - x) / w, (py - y) / h), 0, 0.95)
        const rad = cell * 0.56 * Math.sqrt(dk)
        if (rad > 0.35) {
          ctx.beginPath()
          ctx.arc(px, py, rad, 0, TAU)
          ctx.fill()
        }
      }
    }
    ctx.restore()
    ctx.strokeStyle = INK
    ctx.lineWidth = 2
    ctx.strokeRect(x, y, w, h)
  }

  function drawWaxRing(ctx, cx, cy, rx, ry, progress, seed) {
    if (progress <= 0) return
    const pts = []
    for (let i = 0; i <= 36; i += 1) {
      const a = (i / 36) * TAU * 1.08
      const jx = (noise(i * 0.4, seed, 1) - 0.5) * 6
      const jy = (noise(i * 0.4, seed, 2) - 0.5) * 5
      pts.push([cx + Math.cos(a) * rx + jx, cy + Math.sin(a) * ry + jy])
    }
    ctx.save()
    ctx.strokeStyle = WAX_RED
    ctx.lineWidth = 4.5
    ctx.lineCap = 'round'
    trace(ctx, pts, progress)
    ctx.restore()
  }

  function materials(scene) {
    const rng = stream('newsprint-' + scene.seed)
    const sheet = surface(W, H, (ctx) => paintNewsprintSheet(ctx, W, H, rng.int(1, 999)))
    const cols = scene.story.items.map((label, idx) => {
      const c = idx % 3
      const r = Math.floor(idx / 3)
      return { label, idx, x: 112 + c * 356, y: 176 + r * 224, w: 320, h: 184 }
    })
    const halftoneLayer = surface(W, H, (ctx) => {
      for (const col of cols) {
        paintHalftoneBox(ctx, col.x, col.y, col.w, 124, (u, v) => {
          const d = Math.hypot(u - 0.5, v - 0.5)
          return clamp(0.75 - d * 1.1 + 0.15 * Math.sin(u * 12 + col.idx), 0.08, 0.88)
        })
      }
    })
    return { sheet, cols, halftoneLayer }
  }

  function drawHalftonePage(ctx, time, scene) {
    const { sheet, cols, halftoneLayer } = scene.materials
    ctx.drawImage(sheet, 0, 0)
    ctx.drawImage(halftoneLayer, 0, 0)

    // Masthead
    ctx.fillStyle = INK
    ctx.font = '900 46px Playfair Display'
    ctx.textAlign = 'center'
    ctx.fillText(scene.story.title.toUpperCase(), W * 0.5, 118)

    for (const col of cols) {
      const p = span(time, col.idx * 0.3, col.idx * 0.3 + 0.9, ease.outCubic)
      // Paper halo cutout under label
      ctx.fillStyle = PAPER
      ctx.fillRect(col.x + 8, col.y + 132, col.w - 16, 40)
      ctx.fillStyle = INK
      ctx.textAlign = 'left'
      const sz = fitText(ctx, col.label, col.w - 28, 24, 'IBM Plex Serif', '700')
      ctx.font = '700 ' + sz + 'px IBM Plex Serif'
      ctx.fillText(col.label, col.x + 14, col.y + 160)
      if (col.idx === 0 || col.idx === cols.length - 1) {
        drawWaxRing(ctx, col.x + col.w * 0.5, col.y + 62, col.w * 0.42, 47, p, col.idx + 10)
      }
    }
  }

  function drawShowcase(ctx, time, scene) {
    drawHalftonePage(ctx, time, scene)
  }

  function drawStory(ctx, time, scene) {
    drawHalftonePage(ctx, time, scene)
    ctx.fillStyle = WAX_RED
    ctx.textAlign = 'left'
    ctx.font = '700 28px IBM Plex Mono'
    ctx.fillText(scene.beat.caption, 112, 654)
  }

  const VOICES = {
    rustle: { kind: 'hiss', filter: 'bandpass', cutoff: 1800, attack: 0.04, decay: 0.28 },
    knuckle: { kind: 'thump', drop: 1.9, bend: 0.04, decay: 0.12 },
    linotype: { kind: 'modal', partials: [1, 2.4, 4.3], gains: [0.8, 0.5, 0.25], decays: [0.05, 0.03, 0.02] },
    pressDrone: { kind: 'bed', wave: 'sawtooth', detune: 4, cutoff: 380, drift: 0.12 },
  }
  const SCALE = MotionSound.scale(53, [0, 2, 4, 7, 9])

  function showcaseScore(scene) {
    const events = [{ at: 0, voice: 'pressDrone', note: 41, velocity: 0.35, length: scene.duration }]
    for (let i = 0; i < 8; i += 1) {
      events.push({ at: 0.2 + i * 0.55, voice: 'linotype', note: SCALE(i), velocity: 0.38 })
      events.push({ at: 0.4 + i * 0.55, voice: 'rustle', velocity: 0.28 })
    }
    return { seed: scene.seed, voices: VOICES, events }
  }

  function storyScore(scene) {
    const events = [{ at: 0, voice: 'pressDrone', note: 41, velocity: 0.35, length: scene.duration }]
    scene.story.beats.forEach((beat, idx) => {
      events.push({ at: beat.start + 0.05, voice: 'rustle', velocity: 0.34, pan: -0.3 + idx * 0.2 })
      events.push({ at: beat.start + 0.22, voice: 'knuckle', note: 45 + idx * 2, velocity: 0.47 })
      events.push({ at: beat.start + 0.45, voice: 'linotype', note: SCALE(idx + 2), velocity: 0.42 })
    })
    return { seed: scene.seed, voices: VOICES, events }
  }

  Motion.defineStyle({
    slug: 'vintage-newsprint',
    materials,
    showcase: { duration: 6, draw: drawShowcase, score: showcaseScore },
    story: { draw: drawStory, score: storyScore },
  })
})()
```

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
