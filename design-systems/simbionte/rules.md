# Symbiote design system

Interfaces made of living black matter. Controls are soft, organic and alive: strands grow from them, grab, stretch, thin out, snap and retract. Use it for expressive creative interfaces, interactive video overlays or the signature moment of a brand, never for dense data screens.

## Colors

- Surface: light and quiet, #f5f7f6, so the black matter reads as an object on it.
- Matter: soft matte black, #080a0d. Deep surfaces may go to #090b0d.
- Text on matter: a silver gradient (#ffffff at the top, #d5d7dc, #a9afb7 in the middle, #e7ebee at the bottom) with a 1 px black drop shadow.
- Secondary text: #7b8288.
- Light: a cool silver sheen on top edges and a restrained blue-violet rim (#7e99cf family). A discreet blue and green rim is allowed on edges. No saturated accent colors.
- Light pieces (a toggle thumb, a ceramic track): pale radial gradients, #ffffff → #d6dbe1 → #aab1bb.

## Type

- System sans-serif, semibold (about 650), letter spacing -0.04em on labels.
- Labels are short verbs: "Create bond", "Enable bond".
- Captions 12 px, regular, no letter spacing.

## Shape and borders

- Pills and capsules, fully rounded. No hard corners, no visible borders on the matter.
- Depth comes from light and soft contact shadows on the surface, never from outlines.
- Focus ring: 2 px solid #7e99cf, offset 8 px from the shape.

## Material

- Matte body, never glossy plastic. Strands are the same material, thinner and slightly glossier.
- Thickness follows volume and length: whatever stretches gets thinner; free tips thicken as they retract.
- Matter is continuous: roots blend smoothly into the body; strands form webs and bridges between neighbors.

## Motion

- Simulated, not keyframed: strands have memory, inertia and tension (chains of nodes with fixed time steps). Never recompute curves from scratch every frame.
- Matter prepares before it moves: tips form, then reach, then grip, then pull.
- Each gesture has a distinct reverse: release is not the same animation played backwards.
- Snapping happens after the neck thins (about 105 ms); both fragments retract along their own path.
- Stillness strengthens a bond; shaking weakens it. Interruptions resume from the current pose.
- At rest, only small, local movement. Never pulse the whole control.
- Pause simulation out of view; motion must look the same at 30 Hz and 120 Hz.

## Accessibility

- Keep native semantics: a real button, a real switch with its state announced, keyboard included.
- Canvases are decorative (`aria-hidden`); labels stay real text.
- `prefers-reduced-motion: reduce`: static material, immediate state changes.
- Without WebGL, a plain functional fallback with the same colors and labels.

## Do

- Let the matter react to the person: proximity, stillness, interruption.
- Keep one living control per view; let the rest of the page stay calm.

## Don't

- Don't use gloss, chrome or wide white highlights: the matter becomes plastic.
- Don't fan every strand toward the cursor at once.
- Don't add saturated colors, glows or neon.
- Don't hide the control's function behind the effect.

Credit: the family was informed by the Venom Button by exteestudio (github.com/exteestudio/venom-button); its pieces were written from scratch.
