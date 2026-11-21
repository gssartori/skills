# Win95 CRT Power Button

Build this component for my project. Ask where it will be used if that changes the implementation. Use the linked single-file reference for the interaction and adapt it to my layout. Provide dependency-free HTML, CSS and JavaScript or an equivalent component for my stack.

## Look

Build a small physical CRT with a thick cream bezel, inset glass, a green status light and subtle scan lines. Leave a faint standby label on the glass. Draw an original pixel desktop inside the glass with a tiny window and a taskbar.

## Motion

On hover or keyboard focus, expand a phosphor point into a horizontal line, then open it vertically and reveal the picture. On press, brighten the glass and reveal the miniature desktop. On leaving or losing focus, reverse the same progress value from the current frame so the beam never jumps.

## Accessibility

Use a real button. Keep a visible keyboard focus state and support Enter, Space and tap. With reduced motion, switch straight to the appropriate standby, welcome or desktop state.

## Customize

Expose the standby label, phosphor tint, startup and shutdown durations, desktop palette and action callback.
