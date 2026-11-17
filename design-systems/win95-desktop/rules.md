# Win95 Desktop design system

A mid-1990s beige-box desktop operating system on a crisp pixel grid: bevelled grey chrome windows, navy title bars, aliased bitmap text, dotted pixel arrows and a classic taskbar with a waving four-pane flag. It works for landing pages, components, slides and videos. Every element lives inside the desktop.

## Identity

Teal desktop wallpaper (`#008080`) with a 24 px bottom taskbar, 2-pixel bevelled `#C0C0C0` window chrome (`#FFFFFF` / `#DFDFDF` top-left highlights, `#808080` / `#000000` bottom-right shadows), solid `#000080` active title bars (`#808080` when inactive), and aliased 1-bit pixel/bitmap typography.

**Three signatures every desktop scene shows** (a single component carries at least the bevelled chrome and the crisp pixels):

1. Authentic 2-pixel bevelled grey chrome (`#C0C0C0`) with solid `#000080` title bars, close/minimize/maximize bevel buttons, and a bottom taskbar with a `Start` button and a system clock.
2. A crisp pixel aesthetic: integer scaling with nearest-neighbor pixels, aliased bitmap text, 2x2 Bayer ordered dithering on any shaded panel, and dotted pixel arrows.
3. Active desktop interaction: an aliased pixel arrow (or hourglass) cursor clicking tabs, dragging windows, or triggering dialogs that open with 3-step outline-zoom rectangles.

**Three exclusions:** never smooth antialiased drop shadows or blurred glass; never linear gradients inside title bars; never unmotivated fade transitions or static dead frames.

## Pixels

Design on a low-resolution logical grid and scale it up by whole numbers (2x, 3x) with nearest-neighbor sampling (`image-rendering: pixelated` on the web, `imageSmoothingEnabled = false` on a canvas). Snap every coordinate to an integer pixel (`Math.round`). Never blur or smooth the pixels.

## Materials

- **Desktop & Chrome.** Teal `#008080` wallpaper. Chrome face `#C0C0C0`, highlight `#FFFFFF`, light `#DFDFDF`, shadow `#808080`, black `#000000`.
- **Bevels (2 px logical).**
  - `window`: outer TL `#DFDFDF`, BR `#000000`; inner TL `#FFFFFF`, BR `#808080`.
  - `button`: outer TL `#FFFFFF`, BR `#000000`; inner TL `#DFDFDF`, BR `#808080`.
  - `pressed`: outer TL `#000000`, BR `#FFFFFF`; inner TL `#808080`, BR `#DFDFDF`.
  - `field` (sunken): outer TL `#808080`, BR `#FFFFFF`; inner TL `#000000`, BR `#DFDFDF`.
- **Dithered Shading.** Use a 2x2 Bayer matrix (`[[0, 0.5], [0.75, 0.25]]`) to dither between palette bands on left wizard banners or active taskbar buttons (white/grey checker).
- **Palette.** Teal `#008080`, chrome `#C0C0C0`, navy `#000080`, white `#FFFFFF`, black `#000000`, shadow `#808080`, tooltip cream `#FFFFE1`, error red `#FF0000`, success green `#008000` (`#00A000` for the success icon), accent amber `#E8D050`, highlight cyan `#40A0D0`.
- **Lettering.** Crisp aliased bitmap system font for all UI chrome, tabs, status bars and badges, plus hard-thresholded `Inter` (700/800, alpha threshold > 120 snapped to 255/0) for large display headlines and key numbers. Minimum logical sizes: titles 22 px, essential labels 14 px, key numbers 32 px. Always place black text on `#FFFFFF`, `#C0C0C0` or `#FFFFE1` tooltip plates, or white text on `#000080` navy selection bars.
- **Finish.** Crisp 1 px logical outlines (`#000000`); an optional CRT bezel/scanline hint at most 3% alpha, never blurring the pixels.

## Time

Smooth cursor travel and window motion, paired with authentic stepped OS interactions: progress bars tick in discrete 7x10 px navy blocks, focus rectangles blink at 6–8 Hz, and a dragged error dialog redraws in laggy steps.

- **Something is always alive.** The cursor glides along eased paths, the clock, hourglass and LEDs pulse, progress blocks fill, data icons fly along dotted paths.
- **Three-beat action.** Dialogs and elements enter with 3-frame outline-zoom rectangles or a crisp pop-in with a 1-frame settle; active controls keep subtle idle feedback (blinking caret, spinning hourglass, pulsing status bar); elements leave by minimize/close or an outline-zoom collapse over `0.25–0.45 s`.
- **Reduced motion.** With `prefers-reduced-motion: reduce`, keep the stepped state changes and drop travel, zooms and blinking.

## Piece vocabulary

Turn any noun into a Win95 desktop piece:

- **Central Object / System.** An application window or tabbed Property Sheet with menu bar, group boxes (`etched` border + inset title), trackbar sliders, navy-block progress bars, and a 2-pane status bar whose gauges and controls change state.
- **Figure (Character).** Crisp pixel-art characters (16x16 to 48x48 logical sprites scaled cleanly 2x–4x) with distinct silhouettes, solid palette fills, 1 px black pixel outlines, blinking eyes (~0.14 s every ~3 s), and expressive reactions (sweat drop, raised arms, wide eyes).
- **List Item.** Desktop icons (`32x32` logical pixel art + centered label), file-explorer items, or sunken-bevel `#FFFFFF` mini-window cards inside a group box, each with a distinct pixel-art illustration of its task drawn inside the card.
- **Arrow / Connection.** Dotted pixel lines (`2x2` px dots spaced every `4 px`) that draw on progressively and end in a crisp pixel arrowhead, with data cards or signals stepping along the path.
- **Label.** Crisp aliased text on `#FFFFE1` tooltip boxes (`1 px` `#000000` border), `#000080` navy selection bars, or `#C0C0C0` bevelled buttons, always on top.
- **Counter.** A number inside a sunken `#FFFFFF` field or status bar, ticking upward along an ease-out curve and locking in a `#000080` navy highlight box.
- **Progress Graph.** Sunken `#FFFFFF` chart with dotted grey gridlines, a pixel-stepped green/navy line, square data markers, and a `#FFFFE1` tooltip on the final point.
- **Error Mark.** Classic `#FF0000` circle-X icon + `SYSTEM` error dialog (`bevel` frame) or a blinking `#FF0000` focus box + backward dotted red arrow; a dragged error box may smear a stair-step trail of 4–6 copies. **Fix / Success Mark:** `#00A000` green circle-check + navy highlight + classic info message box.
- **Emphasis.** A blinking `#FF0000` dotted focus rectangle or a zoom (`1.5x–2.0x`) framing the active group box.
- **Header.** A dialog title that outline-zooms into the main application's navy title bar.
- **Toggle.** A bevelled button that sinks (`pressed` bevel) when on, with a pixel indicator; never a rounded pill switch.

## Accessibility

- Real controls underneath the pixels: buttons, switches with `aria-checked`, keyboard focus shown as the dotted focus rectangle.
- Text stays real text where the medium allows; contrast follows the plate rules above.
