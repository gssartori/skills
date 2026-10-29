---
name: gsart-video-flat-vector-science
description: Makes an animated explainer video in the "Flat-Vector Science" visual style (Popular Explainer Looks) as a single HTML canvas animation with sound effects, built around the user's own content. Use when the user asks for a video, animation or explainer in the Flat-Vector Science style.
---

# Flat-Vector Science explainer video

- Look: Flat-vector science-explainer illustration: deep navy-to-violet space gradients, chunky outline-free shapes with rich multi-stop gradients, flat crescent shadows and rim highlights, soft radial glows, sparkly star fields, banded ringed planets and cute big-eyed round characters.
- Motion: Smooth eased motion with gentle overshoot: the camera pulls back through scales, planets drift with parallax, characters bob and pop in, glows pulse.
- How it explains: Big smooth camera moves through scale: the model pulls back until a million examples become a spiral galaxy, a foreground planet sweeps across as the wipe, and the camera dives into the glowing brain dome to emerge at a planet whose ring is the accuracy bar; arrows are chunky dotted rounded curves, numbers are big rounded Nunito.

## Steps

1. Ask the user for their content: the topic, or the script to explain. Never invent it.
2. Ask how the audio works:
   - No voiceover: sound effects only (and music, if it suits the style). Ask whether they want a storyboard first (the default) or to go straight to the animation.
   - With voiceover: ask for the voiceover timing (an SRT file or the timed lines). The audio file itself is optional.
3. Read the prompt for that mode, `prompts/no-voice.md` or `prompts/with-voice.md`, and follow it as if the user had sent it, with their content in place of the bracketed placeholder and their timing under MY VOICEOVER TIMING. Skip the storyboard step if they asked to.
4. Where the prompt points to a file in `code/`, read `code/harness.js`, `code/sound.js` and `code/reference.js` and use them exactly as written.
