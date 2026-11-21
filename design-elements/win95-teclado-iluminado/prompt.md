# Win95 Backlit Scene Keypad

Build this component for my project. Ask where it will be used if that changes the implementation. Use the linked single-file reference for the interaction and adapt it to my layout. Provide dependency-free HTML, CSS and JavaScript or an equivalent component for my stack.

## Look

Draw a tiny pixel-art studio next to a hardware keypad with three backlit, bevelled keys. Use sun, moon and power pictograms and a small light on the selected key.

## Motion

Press a key to ease from the room palette currently on screen into day, evening or standby. Keep the pixel geometry stable. A new press mid-transition should start from the colors currently shown.

## Accessibility

Use a named radio group with real radio inputs, one checked option and visible keyboard focus. Support arrow keys, Home and End. Jump to the selected palette when reduced motion is requested.

## Customize

Expose the three palettes, option labels, transition duration, scene art and change callback.
