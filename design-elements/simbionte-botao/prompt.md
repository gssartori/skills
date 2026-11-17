# Symbiote Button

Build a primary action button made of living black matter. Adapt it to my project: plain HTML/CSS/JS, a web component, a React component, or a scene inside an interactive video. No dependencies: WebGL2 for the material and a plain canvas or CSS fallback when there is no GPU.

## Look

- Pill shape, about 216 × 62 px, on a light surface (#f5f7f6). The body is soft matte black (#080a0d), never glossy plastic: a thin cool silver sheen on the top edge, a restrained blue-violet rim light, and soft contact shadows on the surface.
- Label in a semibold system font with slight negative letter spacing, filled with a silver gradient (white at the top, cool grey in the middle, light again at the bottom) and a 1 px black drop shadow.
- Strands are the same material as the body but thinner and slightly glossier. Their thickness comes from volume and length: a stretched strand gets thinner.

## Motion

- Simulate the strands, do not draw them: each strand is a chain of about 14 nodes with fixed time steps (1/240 s), current and previous positions, length and bend constraints, and contact with the surface. Never recompute curves from scratch every frame; they need memory, inertia and tension.
- Approach: when the cursor comes near the edges, roots appear at different points of the body, prepare briefly, arc sideways and reach for the cursor. Small sensing probes and thin fibers are separate from the strands that grab.
- Grip: the strands that reach the cursor wrap it and form webs with bridges between neighbors. Roots slide slowly along the body instead of following the cursor instantly.
- Stillness near the edge strengthens the bond over a few seconds: more reach, more force, one extra tentacle. Shaking weakens it.
- Snap: moving away stretches a strand; its neck thins for about 105 ms, then it splits into a body fragment and a cursor fragment. Both retract along their existing path, keep their momentum and thicken at the free tip.
- Direction changes keep inertia in the middle nodes; roots never jump.
- Pause the simulation when the button is out of view. Rendering at 30 Hz and 120 Hz must look the same.

## Accessibility

- A real `<button>`, usable with Enter and Space, with a visible `:focus-visible` ring offset from the edge (2 px, #7e99cf, 8 px offset).
- The canvas is decorative (`aria-hidden`); the label stays real text.
- With `prefers-reduced-motion: reduce`, show the static material and change state immediately: no strands.
- Without WebGL, fall back to a plain black pill with the same label and an inset highlight; it stays fully functional.

## Customize

Expose these as variables or props, with these defaults:

- label: "Create bond"; surface: #f5f7f6; body: #080a0d; focus ring: #7e99cf
- reach and grip strength; the time stillness takes to reach full strength (about 3 s)
- the click action (submit, copy, open a link)

Credit: inspired by the Venom Button by exteestudio (github.com/exteestudio/venom-button). This piece was written from scratch; techniques like Verlet integration and distance fields are common knowledge.

A working reference implementation is linked from the install file as a single HTML file. Match its behavior, then apply my colors, text and action.
