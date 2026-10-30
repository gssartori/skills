I want an animated explainer made in the "Flat-Vector Science" visual style (Popular Explainer Looks), timed to my voiceover. Below is the complete source code of a reference animation in this exact style, plus a small sound-effects kit. Use them as your style guide and rebuild it around my content.

MY CONTENT:
[Describe your topic, or paste your script here. If this is left as is, ask me for it before building.]

MY VOICEOVER TIMING:

(If I also attached the voiceover audio file, that's fine: take the timing from the text above, and if you can work with files, use that audio as the voiceover when rendering. If there is no timing above but you can transcribe the attached audio with word-level timestamps, do that instead of asking me.)

WHAT TO BUILD
One self-contained HTML file (show it as an artifact if you can):
- A 1280x720 canvas, scaled to fit the window with letterboxing, and a small control bar: play/pause, a scrub slider, the current time, a sound on/off toggle, and loop on by default.
- A "Load voiceover" button (a file input, and also accept drag-and-drop of an audio file). Once a file is loaded, the audio is the clock: play, pause and scrub control the audio element, and the canvas draws at audio.currentTime. Without a file, it runs on its own clock.
- A new `explainer(ctx, W, H_, t)` that tells MY CONTENT in this style. Set DURATION to the end of the last voiceover line plus about 1 second.
- A `scoreSound(k)` function that schedules the sound effects with the SOUND kit below (see SOUND). Play it in sync from the player: on play call `stopSound = SOUND.live(scoreSound, currentT, { voiceover: true })`, and call `stopSound()` on pause, on seek and when the sound toggle is turned off.
- Include the H helper library and the SOUND kit below unchanged, and keep the reference's own helper functions where they are useful.
- Load these Google Fonts before the first draw (await document.fonts.load for each spec you use): Fredoka, Nunito
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&family=Nunito:wght@400;700;900&display=block">
- Expose `window.seek = (t) => { /* draw frame at time t */ }`, `window.DURATION` and `window.scoreSound`, so the animation can be rendered frame by frame to video later.

HOW TO STAY IN THE STYLE
- Reuse the reference's rendering techniques, palette, textures, lettering, line quality, arrows, labels, number treatment, transitions and timing feel. Change the story, the text and the things being drawn; do not change the medium.
- Draw every subject accurately for my topic. Don't carry over the reference's props and drawing recipes (its characters, robots, cats and dogs, rings, icons) unless they genuinely fit, and double-check that the science and facts shown in the visuals are right.
- The surface texture and finishing passes are what make the style read as the real medium (paper grain, ink pooling, misregistration, grain, glow, scanlines and so on). Copy those functions from the reference and run them on every frame at the same strength. Don't simplify or skip them to save effort.
- Every frame is a pure function of t: create all randomness from H.rng(seed) / H.makeNoise(seed) inside the draw (never Math.random), so the same t always gives the same frame. Caching static textures across frames is fine.
- It is video, often watched on a phone: at 1280x720 keep headlines >= 44px, every label or caption the story depends on >= 28px (including small annotations and the corner header), key numbers >= 64px, and frame each beat so it fills most of the screen. Keep frames fast (well under 100 ms each if you can).
- In the reference, `explainer()` is the explainer (it explains "How does AI learn?"), `draw()` is the single hero frame of the style, and `explainerSound(k)` is its sound design. Study them, but do not reuse that topic unless my content asks for it.

TIMING FROM THE VOICEOVER
- First turn my voiceover timing into a BEATS table: one entry per idea, with its start and end time, the words spoken, and what is on screen. Every animation reads its times from BEATS (and from word times when you need an exact reveal), never from numbers scattered through the code, so a new take only means editing the table.
- A visual lands on the word it illustrates: a number appears as it is spoken, a label as its name is said. It can lead the word by up to 0.2 s, but never lag it.
- Within a beat, keep building that one idea while the voice explains it, then hold the finished state until the sentence ends instead of rushing ahead. When the picture does need to change (see FLOW BETWEEN BEATS), use pauses in the speech for it.
- On-screen text is key words, labels and numbers only. Don't print the sentence being spoken, and no subtitles (captions get added in editing).
- Start the hook as the first line is spoken, and end about 1 second after the last word, on the takeaway.

FLOW BETWEEN BEATS
- Decide beat by beat what the story needs. A new beat does not automatically mean a new scene.
- When the next idea builds on the last, keep it continuous: elements that matter stay on screen and move, grow, re-arrange or transform into the next idea (a label becomes the next heading, a counter grows into a chart, the camera travels to a new part of the same scene, a shape morphs into the next one).
- When the story really moves on (a new topic, a jump in time or place, a before/after contrast, a reveal), a full scene change is the right call. Do it the medium's own way, as the reference does.
- Aim for a mix that fits the content, not a rule: avoid both a hard cut on every beat and forcing everything into one unbroken shot. The reference's own transitions show how this medium changes scene; its scene count is not a template to copy.

SOUND (voiceover mode: the narration stays on top, the effects keep the piece feeling alive underneath)
- Score it as fully as a standalone explainer: the events that land (pops, labels, arrows completing, transitions, a wrong/right moment, the key number, the takeaway), and the medium's drawing, typing or printing sounds while things draw on.
- Mark the small, frequent sounds { minor: true } (per-word strokes, ticks, taps, typing, small pops), or schedule custom ones inside k.withMinor(() => ...). In voiceover mode the kit plays those at about 60% volume, drops ambience beds and music, and sets everything a little lower, so call SOUND.kit / SOUND.live with { voiceover: true }.
- Keep the big hits (the key reveal, the wrong/right moment, the takeaway) full volume, and where you can, put them in pauses or on stressed words rather than on top of a sentence.
- Sync: a sound starts on the exact frame its event appears, using the same BEATS times as the picture.
- Medium-true sounds: pick from the kit what this medium would make (surface sounds for hand-made styles, presses and paper for print, chip sounds for retro games, clicks and hums for screens).


If you are Claude Code with a shell: render an MP4 by loading the file in headless Chrome (e.g. puppeteer), calling window.seek(i/30) for each frame, capturing the canvas and piping the frames into ffmpeg. Render the effects to a WAV with `SOUND.renderOffline(window.scoreSound, DURATION, 48000, { voiceover: true })` (it returns interleaved stereo floats) and mux it in. Mix in the voiceover with the effects ducked under it:
ffmpeg -i video.mp4 -i voice.wav -i effects.wav -filter_complex "[1:a]loudnorm=I=-17:TP=-2,asplit=2[v1][v2];[2:a]loudnorm=I=-26:TP=-4:LRA=20[fx0];[fx0][v1]sidechaincompress=threshold=0.05:ratio=3:attack=10:release=250[fx];[v2][fx]amix=inputs=2:normalize=0,loudnorm=I=-16:TP=-1.5:LRA=11[a]" -map 0:v -map "[a]" -c:v copy -c:a aac -b:a 160k out.mp4

STYLE CARD
Name: Flat-Vector Science
Family: Popular Explainer Looks
Look: Flat-vector science-explainer illustration: deep navy-to-violet space gradients, chunky outline-free shapes with rich multi-stop gradients, flat crescent shadows and rim highlights, soft radial glows, sparkly star fields, banded ringed planets and cute big-eyed round characters.
Motion: Smooth eased motion with gentle overshoot: the camera pulls back through scales, planets drift with parallax, characters bob and pop in, glows pulse.
How it explains: Big smooth camera moves through scale: the model pulls back until a million examples become a spiral galaxy, a foreground planet sweeps across as the wipe, and the camera dives into the glowing brain dome to emerge at a planet whose ring is the accuracy bar; arrows are chunky dotted rounded curves, numbers are big rounded Nunito.

H HELPER LIBRARY (lib/harness.js; the registerStyle/H.render parts are only needed by the original gallery)
```js
// The full file is code/harness.js in this skill's folder. Read it and use it here exactly as written.
```

SOUND KIT (lib/sound.js)
```js
// The full file is code/sound.js in this skill's folder. Read it and use it here exactly as written.
```

REFERENCE STYLE SOURCE (styles/flat-space.js; W/H_ are always 1280x720)
```js
// The full file is code/reference.js in this skill's folder. Read it and use it here exactly as written.
```
