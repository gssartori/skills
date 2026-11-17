# Shine Button

Build a primary action button with this look and behavior. Adapt it to my project: plain HTML/CSS/JS, a React component, or a scene inside an animated video. Keep it dependency-free.

## Look

- Pill shape (fully rounded), generous padding (about 0.95em vertical, 1.6em horizontal), semibold system font, slight negative letter spacing.
- Background: a 135° gradient from the accent color to a second, cooler accent. White label and a small line icon on the left.
- Soft colored shadow under the button, in the accent color, plus a thin inner highlight on the top edge.
- A diagonal light streak (a translucent white gradient band, skewed about -18°) sits inside the button, clipped by its shape.

## Motion

- Idle: every few seconds the light streak crosses the button from left to right, then waits.
- Hover: the button rises 2px, its shadow grows, and the streak crosses faster.
- Press: it scales to 0.97.
- Click: a circular ripple grows from the click point and fades; the gradient turns green, the icon becomes a check that draws itself, and the label changes to the success text. After about 1.6 seconds it returns to the original state.
- Use ease curves that feel quick but soft (for example cubic-bezier(.2,.8,.2,1)).

## Accessibility

- A real `<button>` element, usable with Enter and Space, with a clear `:focus-visible` ring offset from the edge.
- Announce the success text politely (`aria-live="polite"`).
- With `prefers-reduced-motion: reduce`, remove the streak, the lift and the ripple; keep the color and label change.
- Readable in light and dark mode.

## Customize

Expose these as variables or props, with these defaults:

- accent: #0a84ff; second accent: #5e5ce6; success color: #30d158
- label: "Copy prompt"; success label: "Copied"
- streak interval: 3.2s; success duration: 1.6s
- radius: fully rounded
- the click action (copy text, submit, open a link)

A working reference implementation is linked from the install file as a single HTML file. Match its behavior, then apply my colors, text and action.
