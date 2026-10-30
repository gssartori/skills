---
name: gs-video-ascii-demoscene
description: Makes an animated explainer video in the "ASCII Demoscene" visual style (Retro Digital) as a single HTML canvas animation with sound effects, built around the user's own content. Use when the user asks for a video, animation or explainer in the ASCII Demoscene style.
---

# ASCII Demoscene explainer video

- Look: A ray-marched 3D torus rasterised into a strict monospace character grid via a luminance ramp, colour-coded like a 90s demoscene intro: box-drawn title panel, plasma backdrop, copper bars and a sine scroller.
- Motion: Like a demo intro booting: plasma thickens in, the spinning torus is rastered into characters top-to-bottom behind a bright scan row, the block title and nfo panel print, copper bars open and a rainbow sine-scroller glides in from the right.
- How it explains: One long ASCII document that the terminal scrolls through row by row: figlet block-letter question, labelled ASCII cat/dog cards stepping along a box-drawing arrow into a MODEL box, a reverse-video GUESS/CHECK/ADJUST loop with a red error path, and block-character bar charts with figlet counters.

## Steps

1. Ask the user for their content: the topic, or the script to explain. Never invent it.
2. Ask how the audio works:
   - No voiceover: sound effects only (and music, if it suits the style). Ask whether they want a storyboard first (the default) or to go straight to the animation.
   - With voiceover: ask for the voiceover timing (an SRT file or the timed lines). The audio file itself is optional.
3. Read the prompt for that mode, `prompts/no-voice.md` or `prompts/with-voice.md`, and follow it as if the user had sent it, with their content in place of the bracketed placeholder and their timing under MY VOICEOVER TIMING. Skip the storyboard step if they asked to.
4. Where the prompt points to a file in `code/`, read `code/harness.js`, `code/sound.js` and `code/reference.js` and use them exactly as written.
