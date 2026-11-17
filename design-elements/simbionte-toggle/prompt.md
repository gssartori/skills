# Symbiote Toggle

Build an on/off switch where a droplet of living black matter grabs the thumb and pulls it across. Adapt it to my project: plain HTML/CSS/JS, a web component, a React component, or a scene inside an interactive video. No dependencies: WebGL2 for the material and a CSS fallback when there is no GPU.

## Look

- A light ceramic capsule track with a pale sphere as the thumb (radial gradient from white to cool grey, #fff → #d6dbe1 → #aab1bb).
- Off: the sphere rests on the left, a small droplet of soft matte black matter (#080a0d) sits on the right. No inner webs yet.
- On: the black mass covers the track from right to left with an irregular edge and small outer extensions; filaments of different lengths and curvatures run inside it, two of them crossing.
- The same lighting as the Symbiote Button: matte body, cool silver sheen, a discreet blue and green rim on the edges.

## Motion

Use one reversible transition with separate intervals for each part, so the sequence reads as a gesture, not a slide:

1. The droplet forms tips and prepares before anything moves.
2. It reaches out six fingers of different lengths and wraps the sphere.
3. Only then does it pull the sphere across the track; the mass spreads behind it.
4. Filaments grow from around the sphere toward the left, at different times.
5. It settles: small, local movement only. The whole capsule never pulses.

Switching off is a distinct gesture, not the same film backwards: the ceramic reappears from the left, the sphere is pushed back, the fingers let go at different times and retreat into the droplet. An interruption resumes from the current pose.

## Accessibility

- A real switch: `<button role="switch" aria-checked>` or a native checkbox, with Space and Enter, a visible focus ring and the state announced.
- The canvas is decorative (`aria-hidden`).
- With `prefers-reduced-motion: reduce`, the state changes immediately with the static material.
- Without WebGL, fall back to a plain capsule whose sphere slides with a 0.45 s ease; it stays fully functional.

## Customize

Expose these as variables or props, with these defaults:

- label: "Enable bond"; initial state: off
- matter color: #080a0d; sphere gradient: #fff → #d6dbe1 → #aab1bb
- transition length (about 3.5 s on, a little shorter off)
- what the switch controls

Credit: inspired by the Venom Button by exteestudio (github.com/exteestudio/venom-button). This piece was written from scratch.

A working reference implementation is linked from the install file as a single HTML file. Match its behavior, then apply my colors, text and action.
