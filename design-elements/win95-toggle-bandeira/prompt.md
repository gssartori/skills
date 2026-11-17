# Win95 Flag Toggle

Build an on/off toggle in the look of a mid-1990s desktop operating system. Adapt it to my project: plain HTML/CSS/JS, a React component, or a scene inside an animated video. Keep it dependency-free.

## Look

- A small window: `#C0C0C0` face with a 2 px bevel (outer top-left `#DFDFDF`, bottom-right `#000000`; inner top-left `#FFFFFF`, bottom-right `#808080`), a solid `#000080` title bar with white bold text and bevelled close and minimize buttons, on a teal `#008080` desktop.
- Inside, a group box with an etched border and an inset title, holding the toggle: a bevelled button with a 16 px square light (`#404040` off, `#00A000` on) and a bold label.
- Next to it, a sunken white field with a pixel-art flagpole: black pole, amber `#E8D050` finial, grey ground. The flag has four panes: red `#FF0000`, green `#00A000`, navy `#000080`, amber `#E8D050`, with a 1 px black outline.
- Draw the flag on a tiny canvas (about 48 × 48 logical pixels) scaled up with `image-rendering: pixelated`. Integer pixels only, no smoothing.
- A two-pane sunken status bar under the window. Optional taskbar with a Start button and a clock.
- Bitmap-looking system font (Tahoma or similar, no font smoothing). Never rounded pills, gradients in title bars or soft shadows.

## Motion

- On: the button sinks (swap to the pressed bevel: outer top-left `#000000`, bottom-right `#FFFFFF`; inner top-left `#808080`, bottom-right `#DFDFDF`), the light turns green, and the flag climbs the pole in discrete 2 px steps every 60 ms (about 0.6 s).
- At the top the flag waves: each column rises or falls by up to 2 pixels along a sine that moves one step at a time, more at the free edge than at the pole; the troughs get a 1-pixel checker dither in black.
- Off: the button pops back up, the flag steps down the pole and hangs still at the bottom.
- Stepped, not smooth: this is an old computer redrawing.

## Accessibility

- A real switch: `<button role="switch" aria-checked>`, toggled by click, Space and Enter. Keyboard focus shows as a dotted focus rectangle around the label.
- The status bar announces "Flag raised" / "Flag lowered" with `aria-live="polite"`. The canvas is decorative (`aria-hidden`).
- With `prefers-reduced-motion: reduce`, the flag jumps straight to its place and does not wave.

## Customize

Expose these as variables or props, with these defaults:

- label: "Raise flag"; window title: "Flag"; status texts: "Flag raised" / "Flag lowered"
- pane colors: #FF0000, #00A000, #000080, #E8D050
- step: 2 px every 60 ms; wave amplitude: 2 px
- what the switch controls

A working reference implementation is linked from the install file as a single HTML file. Match its behavior, then apply my colors, text and action.
