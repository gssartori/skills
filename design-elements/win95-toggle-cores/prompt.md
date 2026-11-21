# Win95 Color Switch

Build this component for my project. Ask where it will be used if that changes the implementation. Use the linked single-file reference for the interaction and adapt it to my layout. Provide dependency-free HTML, CSS and JavaScript or an equivalent component for my stack.

## Look

Make a square grey thumb inside a rectangular sunken track. Place a four-pane pixel mark on the thumb and a tiny signal in the track.

## Motion

Slide the thumb right as the mark turns once around its vertical axis. Bring back the original four colors and change the track to teal. Reverse the motion when switching off.

## Accessibility

Use a native button with switch semantics and aria-checked. Synchronize its visual state with the checked state. Allow tap, Enter and Space and remove the turn and slide under reduced motion.

## Customize

Expose the accessible label, track color, travel distance, timing and the state change callback.
