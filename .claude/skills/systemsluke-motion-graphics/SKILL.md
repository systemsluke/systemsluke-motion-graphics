---
name: systemsluke-motion-graphics
description: "Use when someone wants animated graphics and sound effects on their vertical talking-head videos (Instagram Reels first, also TikTok and Shorts) in their own style. The first run asks for their references, what they love and hate, their typography, colours and the animations they like and dislike, builds their own design system and saves it as their own editing skill. After that they upload a video: it transcribes it, logs every word and the graphic that lands on it, builds the edit with sound, and takes notes like an editor."
---

# systemsluke motion graphics: your own editing style

This skill turns a vertical talking-head video into a finished short with motion graphics timed to the words, real-world material cut in where it helps, quiet sound effects and upload-ready files. Everything about the look comes from the person using it. Nothing is a house style: their references and answers decide the colours, the type, the components, the illustrations, the layout, how things move, the transitions and the sound.

The flow, in the order the person meets it:

1. **References first.** It asks for things they love and things they can't stand.
2. **Their design system.** From those references and a short interview it works out their look all the way down to how things move, shows it to them on one board, and tests it on 10 seconds of their own footage.
3. **Their own editing skill.** The design system is saved as a skill of their own, so every later video starts from their style.
4. **Upload a video.** They send a video.
5. **Transcribe.** It transcribes the whole video with the time of every word.
6. **The edit log.** It logs every word and every graphic that lands on it, so one idea always gets the same visual and the whole video stays consistent.
7. **Build and deliver.** Graphics, sound effects and the files for upload and for their editor.
8. **Talk to it like an editor.** "This text is too small", "that sound is too loud": it fixes the video and keeps any note that should hold for every video in their editing skill.

Every frame is drawn by an HTML page as a pure function of time (`window.seek(t)`) and rendered with Chromium through Playwright. The full engine is in section 10: write those files out exactly, then change only `style.js` and `components.js` (once, from their design system) and the per-video files.

## Their style only

These rules hold in every step.

- **Start from their references, never from a house style.** The engine's starting tokens are neutral placeholders (white, one blue, a plain sans). Every token, component, illustration, motion setting and sound is replaced from their references and answers. If a setting is still at its starting value at the end of setup, it must be there because their answers chose it.
- **Learn from a reference, never copy it.** Take the principles that make a reference work (pace, contrast, type scale, colour ratio, how much moves, where graphics sit) and express them in the person's own colours, type and subject. Never recreate a creator's graphics, characters, layouts, signature effects or wording.
- **Make it theirs.** Their brand colours, their fonts, the objects of their world (a chef's knives, a coach's whiteboard, a developer's terminal) and their own footage and files beat anything generic.
- **Their dislikes are hard rules.** Anything they say they hate goes into a Never list and is checked before every delivery.
- **Ask, don't assume.** If something about their taste isn't covered by their references or answers, ask one short question rather than guessing.

## 0. Start here

1. Look for a saved style. In order: a skill whose name ends in `-editing-style` in the skills list (load it with the Skill tool), a `style-profile.md` in the conversation or their connected folder, or a design system in the project instructions. If one exists, load it and go to section 6.
2. No style yet: say in one line what happens next ("First I need your references and a few quick questions so I can build your editing style. Then send a video.") and start section 1.
3. If they send a video before any setup, keep it for the style test and still start with section 1. References are what make the result theirs. If they really want to skip, the minimum is two references they love, one they dislike, and their Never list; build from that and say what you assumed.

## 1. References (required)

Ask in plain text, so they can paste links and attach files:

- **Two to five things they love.** Reels or creators, brands, websites, apps, posters, films, magazine spreads: anything whose look they want to feel like. For each, one line on what they love about it.
- **One to three things they dislike**, or never want to look like, and why.
- **Their brand assets**, if they have them: logo, colours, fonts, website.

Study every reference before asking anything else:

- **A video file or screen recording.** Count cuts (`ffmpeg -i ref.mp4 -vf "select='gt(scene,0.3)',showinfo" -f null - 2>&1 | grep -c pts_time`; cuts per second sets the pace). Make a contact sheet (`fps=2,scale=270:-1,tile=8x4`) and look at it. Sample the palette (k-means on a few frames). Note where graphics sit relative to the speaker, how big text is relative to the frame, how things enter, what the transitions are, how much moves at once, and what you hear.
- **A link.** Try WebFetch, or the browser if one is available. Instagram and TikTok usually block reading, so ask for a screen recording or two or three screenshots instead.
- **An image.** Look at it: palette, type, shapes, texture, density, corners, shadows.

Write a reference read and keep it in their design system:

| Reference | What they love | What it does (measured) | Take (principle) | Leave |
|---|---|---|---|---|

"Take" is always a principle ("one accent colour on a lot of white", "text enters word by word", "a new visual about every 3 s"), never a graphic.

## 2. The interview

Use AskUserQuestion: up to four questions per call, two to four options each ("Other" is added automatically for free text), single or multi select, and short previews (hex swatches, type specimens in words, timings, tiny ASCII layouts) because people choose far better from something they can see. If the tool is missing, ask the same rounds in plain text, one round per message.

Shape every option from their references: the first option is the one their references point to, marked recommended. Never name a creator or brand in an option. Skip any question their references, brand assets or footage already answer, and never re-ask. "You decide" means: derive it from their references. Five rounds at most.

**Round 1: them and their videos**
- What they post about and who for (free text is fine).
- Three words for how their videos should feel (multi): calm, premium, playful, bold, technical, warm, raw, cinematic.
- Captions: they add captions later in their editor (then: where do the captions sit: below the head, mid-frame or low on the frame) / Instagram auto-captions / no captions. The graphics always leave that space empty.
- Platforms (multi): Instagram Reels (default), TikTok, YouTube Shorts. Sets the safe zones (section 9).

**Round 2: typography and colour**
- Type direction, with a specimen line for each, matched to their references: clean geometric sans / editorial serif headlines with a sans body / bold condensed headlines / rounded and friendly / a technical mono for labels / their brand fonts. Then offer two or three specific Google font pairings in that direction (any Google font installs with `npm i @fontsource/<slug>`; brand font files go in `fonts/`).
- Text treatment: sentence case / all caps for short labels / big bold keywords. Weight: light, regular, bold, black.
- Colour: their brand colours / three palettes sampled from their references (show swatches with hex) / a palette from their three words. Then how much accent: one accent used sparingly / two accents / mostly monochrome.
- Backgrounds for full-screen moments: flat colour / soft gradient / fine grain / a patterned texture. Light, dark or a mix.

**Round 3: what appears on screen**
- Graphics they like (multi): clean cards and app screens / real screenshots, pages and logos / simple flat icons and diagrams / 3D isometric objects / charts and numbers / photos and cutouts of real things / big kinetic words.
- Graphics they never want (multi): emoji explosions / speech bubbles / cartoon characters / glitch or neon glow / stock 3D renders / busy patterned backgrounds.
- Where graphics sit: floating above the head with their room left as it is (captions below) / in a panel above or below them / mostly full screen / small pops beside the head. And: can big graphics sit slightly behind their head (their head stays in front, no outline round them)?
- Full-screen moments, where the graphic covers the whole frame: none / one or two for the biggest beats / often.

**Round 4: animation they like and dislike**
- Entrances they like (multi): soft fade and rise / snappy pop with a small overshoot / slide in from the side / scale up from small / lines that draw on / stepped, frame-by-frame motion.
- Animation they dislike (multi): bouncy or elastic / spinning or rotating / swipe or slide screen changes / flashing or glitching / slow fades / lots of things moving at once.
- Text animation: word by word on the words they say / a real typing effect / a quick fade / none.
- Between scenes: a hard cut / a zoom punch (a cut that settles from 106%) / a quick crossfade / a slide (push) / a pixel dissolve. The first one picked is the default; the others are for chosen moments.
- Pace: a new graphic every 2 to 3 s / every 3 to 5 s / sparse, with room to breathe. And camera punch-ins on their emphatic lines (a digital zoom to 108 to 110%): yes / no.

**Round 5: sound, files and review**
- Sounds they like (multi): soft clicks when things land / a soft whoosh when something big flies in / typing on typed text / a real mouse click on clicked buttons / a small pop when a logo or badge appears / no sound effects. They add their own music.
- Sounds they dislike (multi): dings and chimes / risers / deep bass hits / cartoon boings / loud swooshes.
- Level: barely there / noticeable / punchy.
- Files (multi): 4K MP4 for upload, a 1080p copy under 30 MiB, a transparent ProRes 4444 overlay plus a sound-effects stem for their editor (ask which: Premiere, Final Cut, DaVinci, CapCut), a short post description.
- Review: just send the finished video / show the storyboard first / show stills first.

Then one plain-text question: anything they never want on screen or in sound (colours, fonts, emoji, phrases, punctuation, effects). Every answer goes into Never.

## 3. Their design system

From the references and answers, work out their look all the way down to how things move. Write it as their design system (it becomes the body of their editing skill):

```markdown
# <Name> editing style
## Feel
Three words: ... | What they post: ...
## References
| Reference | Take | Leave |   (principles only, never graphics)
## Colour
bg ... | tint ... | dark ... | ink ... | mute ... | accent ... | accent dark ... | accent light ... | how much accent: ...
Contrast: ink on bg >= 7:1, accent on bg >= 3:1 (checked)
## Type
Display: <font> <weight>, <size> | Title: ... | Body (inside cards, at least 28 px): ... | Label: <font> <size>, <case>
Text animation: ...
## Layout
float (speaker full frame, graphics above the head) or panel (seam at y ...) | caption band y ... to ... (kept empty)
Behind the head: yes/no | Full-screen moments: ... | Breathing moments: ...
## Components
Card or window: corners, border, shadow, header | Label | Highlight on screenshots | Cursor | Icons | Illustrations: style, stroke, fills, shading
(each one described so it can be drawn the same way every time; the code is in components.js)
## Texture
Full-screen backgrounds: flat / gradient / grain / dither, light and dark rotation
## Motion
Steps: smooth 30 fps or stepped 12 fps | Entrance: ease, duration, overshoot yes/no | Exits | Transitions: default <type, dur>; exceptions ...
Pace: a new graphic every ... s, never more than ... s with nothing landing | Punch-ins: yes/no, scale
## Sound
Allowed: ... | Level: ... | Never: ... | Music: they add it
## Files and review
Platforms: ... | Files: ... | Editor: ... | Review: ...
## Never
- ... (their words)
## Standing notes from feedback
- (dated, newest last)
## Tokens
The exact STYLE block (style.js), SFX_PROFILE block (sfx.py) and components.js
```

Map it to the engine (section 10):
- `STYLE.pal`: every colour, with `accentDark` about 10% darker than the accent and `accentLight` a pale tint of it. `STYLE.font` and `fontFiles` (every weight used must be listed).
- `STYLE.chrome`: `modern` (rounded cards, soft shadow, vector cursor) or `retro` (square 1-bit windows, pixel cursor), whichever is closer to their references; then restyle in `components.js` anything their references need beyond that.
- `STYLE.texture`, `STYLE.highlight` (`marker`, `box`, `underline` or `ants`), `STYLE.motionStep` (30 smooth, 12 stepped), `STYLE.overshoot`, `STYLE.transition` (`hard`, `zoom`, `fade`, `push`, `cut`, `tiles`, `wipe`, `iris`, `blocks`), `STYLE.layout` (`float` or `panel`), `STYLE.safe` from the platforms and the caption band.
- `SFX_PROFILE` in `sfx.py`: `allowed` sounds and `master` (barely there -4 dB, noticeable 0, punchy +4).
- `components.js`: their own drawing helpers (cards, labels, stickers, icon style, characters), built from the engine's primitives and only the tokens, so a colour or font change carries through.

**Show it on one board.** Fill `BOARD` in `board.js` (their name, three words, sounds, Never list; set `iso` only if isometric is in their vocabulary) and render it:

```bash
node render.js stills board.html board 1.2      # board/t_01.20.png: colour, type, motion, components, backgrounds, sound, never
```

Send the board and ask what to change. Apply notes to `style.js` and `components.js`, render again, and loop until they say it is them.

**The uniqueness check.** Before the style test, compare their tokens with the neutral starting values in section 10 and their components with the engine's stock ones. Anything still at its starting value or in its stock form needs a reason from their answers; otherwise restyle it from their references. Also check the board against every reference: if it reads as a copy of any one of them, push it towards their own colours, type and subject.

## 4. The style test

Seeing beats describing: people often change their mind about a palette or an entrance once it moves over their own face.

1. Take 10 seconds of their footage (the first 10 s, or a stretch where they name something). Without footage, make a stand-in clip with ffmpeg (a grey frame with a skin-tone block where the head would be) and say so.
2. Build two or three scenes that use the design system: one graphic landing on its word, one real capture with a word marked as it is spoken (if they use real material), one transition of their default type, and text animated their way.
3. Make two versions: A follows the design system literally; B changes the one thing they were least sure about (palette, entrance, transition, type or texture). Put B in `style_b.js` and `index_b.html` (a copy of `index.html` pointing at it).
4. `python3 tools/preview.py A 0 10` and `python3 tools/preview.py B 0 10 index_b.html`. Send both and ask which, and what to change.
5. Apply notes in `style.js` and `components.js` only. A direction they reject goes into Never in their words. Loop until they say it is right.

## 5. Save their editing skill

Their design system becomes a skill of their own, so every later video starts from it.

- On claude.ai: propose it with `propose_skills` (kind new). Name it `<their-name-or-brand>-editing-style` (kebab-case, without the words claude or anthropic). Description: "Use when <Name> sends a talking-head video to edit: their design system, components, motion, sound, Never list and files; run systemsluke-motion-graphics with these settings." The body is the design system from section 3, including the exact `STYLE`, `SFX_PROFILE` and `components.js`.
- In Claude Code: write the same file to `.claude/skills/<name>-editing-style/SKILL.md` (or `~/.claude/skills/...` to use it in every project).
- Otherwise: send `style-profile.md` and tell them to attach it, or keep it in the project, whenever they send a video.

When a note later becomes a standing rule, update their editing skill with the complete new file (read the current one first).

## 6. Every video

Set up a task list for the stages below; the last one is checking the work.

### 6.1 Upload: the project folder

They send the video (or it is in a folder you can reach).

```bash
mkdir -p proj/real proj/tools && cd proj
npm init -y >/dev/null && npm i @fontsource/inter @fontsource/jetbrains-mono simple-icons    # plus their fonts
node -e "require('playwright')" && echo playwright ok        # use the preinstalled Playwright; never run "playwright install" if it works
pip install --break-system-packages -q sherpa-onnx opencv-python-headless scipy rembg onnxruntime
cp /path/to/their/video.mp4 src.mp4
```

Write every file in section 10 into the folder exactly as given, then paste their `STYLE` into `style.js`, their `components.js`, and their `SFX_PROFILE` into `sfx.py`. Run `node tools/logos.js <brands named in the video>` (with no names it writes an empty `LOGO`; `index.html` always loads `logos.js`).

### 6.2 Inspect the video

```bash
ffprobe -v error -show_entries stream=width,height,r_frame_rate,nb_frames:format=duration -of default=nw=1 src.mp4
ffmpeg -v error -i src.mp4 -vf "fps=1,scale=180:320,tile=10x6" -frames:v 1 contact.png      # look at it
ffmpeg -i src.mp4 -af volumedetect -vn -f null - 2>&1 | grep mean_volume                       # voice level
```

Look at where the head sits across the video: the top of the head sets how low floating graphics can go, and the point between the eyes is the punch-in anchor (`camera.json` `face`). In the panel layout, find the seam (the first row of footage) and set `STYLE.canvas.panel` and `graphicsOnTop`. `T_END` = frames / fps. If the source is not 1080x1920 at 30 fps, convert it first (`ffmpeg -i in.mp4 -vf "scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920" -r 30 src.mp4`).

### 6.3 Transcribe the whole video

```bash
mkdir -p ~/models && cd ~/models
for m in sherpa-onnx-whisper-small.en sherpa-onnx-nemo-parakeet-tdt-0.6b-v2-int8; do
  curl -sSL -o m.tar.bz2 https://github.com/k2-fsa/sherpa-onnx/releases/download/asr-models/$m.tar.bz2 && tar -xjf m.tar.bz2 && rm m.tar.bz2; done
cd - && ffmpeg -v error -y -i src.mp4 -vn -ac 1 -ar 16000 audio16k.wav && python3 asr.py
```

Whisper gives the cleaner text, Parakeet the word times (`words.json`). Read both and fix mishearings by meaning (product names, a keyword they ask people to comment). For other languages, look for a multilingual model on the same release page. If a word matters (a call-to-action keyword) and the models disagree, ask them.

### 6.4 Research what they name

List every product, company, person, repo, news story and number they name. Find the primary source and check what they say against it. Never invent numbers or claims; on-screen wording stays close to what they say. For real material:
- **Logos**: `node tools/logos.js github notion` writes real Simple Icons paths. Never redraw a logo; ask for a file Simple Icons lacks.
- **Pages and posts**: captures must be sharp at 1080 wide. With a browser you can drive: set the window to 540x960 CSS px, decline cookie banners, hide scrollbars and sticky bars with injected CSS, then for each 270x480 tile set `document.documentElement.style.transformOrigin='0 0'; document.documentElement.style.transform='scale(2) translate(-Xpx,-Ypx)'`, take one throwaway screenshot, capture the viewport at full resolution, and join the tiles with `python3 tools/stitch.py`. Crop to the line that tells the story (text at least 20 px tall on the 1080 grid). Without a browser, ask them for screenshots. Never alter a capture.
- **Their own things** (a screen recording, their files, their analytics): ask for them; match a clip's loudness to the voice before cutting it in.
- **Bad examples they mock** ("this is what AI reels look like"): make generic mock-ups in their style, never someone's real content.

### 6.5 Storyboard and the edit log

Split the transcript into beats, one idea per scene, at the pace in their design system. For each scene: the time span and words, what is on screen, floating or full screen, the transition into it, and every element with the word it lands on.

Then write `edit_log.json`, the log of every word and the graphic that lands on it:

```json
{"concepts": {"the product": "app screen card", "growth": "towers rising", "AI": "robot"},
 "items": [{"scene": "A", "t": 1.60, "word": "agent", "what": "robot lands beside the card", "concept": "AI", "sound": "T"},
           {"scene": "D", "t": 12.40, "word": "", "what": "no graphics: breathing moment"}]}
```

`concepts` holds one visual per idea for the whole video: if a robot means "the AI", it means that every time. Log breathing moments too. Run `python3 tools/log.py <max gap in seconds>`: it checks every item lands on its word (within 0.12 s), every idea has its one visual, no stretch longer than the gap has nothing landing, and (once `sfx.py` has run) each item with a sound has its cue. It writes `edit_log.md`, a readable log to share when they ask what happens where. Show the storyboard first only if their review preference says so.

Rules for everyone:
- Every element lands on the word that names it, and every animation finishes at least 0.3 s before its scene's cut.
- Cut on the first word of the new idea (`TB` a frame or two before it).
- When they describe an action ("upload your video", "it transcribes everything"), show that action happening with their real things (their file uploading, their words appearing).
- Avoid gaps longer than their pace allows, and keep a few deliberate breathing moments with no graphics.
- The first frame is the thumbnail and must already look finished. The last scene holds to the end with no fade.
- A call to action ("comment X") gets the keyword big, in their style, with an illustration (a sign, a comment box typing it), held to the end.
- Never cover their face. Big graphics go behind the head (6.6), never over it.

### 6.6 Build `video.js`

Set `T_END`, `TB` (scene switch times), `MODE`, `XT`, `TRANS` (per-cut transition overrides from their design system), `REAL` (captures with pixel sizes). One `scene({ init, draw })` per entry. `draw(t)` returns `{ vb, vt, vx }`: SVG under the DOM layer, SVG over it (marks, cursor), and SVG over the footage (pops beside the head, drawn only while the scene is current). Real images are DOM: `realImg` in `init`, `placeImg` or `realWin` in `draw`. Draw with their `components.js` first, then the engine's primitives (`win`, `chip`, `mark`, `cursor`, `box`, `tower`, `plate`, `person`, `robot`, `dotPath`, `pixBM`).

**Float layout** (speaker full frame): `MODE` is `'full'` for every scene. A scene that calls no `background()` is transparent, so the graphics float over their real room. Keep floating graphics above the head (from `safe.top` down to just above the head) and out of the caption band. A full-screen moment is simply a scene that paints `background(kind, t, seed)`; rotate light, tint and dark, never the same twice in a row.

**Behind the head**: when a graphic is too big for the space above the head, let its lower part run behind the head. List those frames in `occlude.json` (`{"ranges": [[f0, f1], ...]}`, inclusive) and run `python3 tools/matte.py`; `comp.py`, `sheet.py` and `preview.py` then multiply the overlay's alpha by the inverse of the person's matte, so their head stays in front with no outline and the room unchanged. End a range before any cut into a full-screen scene.

**Punch-ins**: if they want them, write `camera.json` (`{"face": [x, y], "shots": [[t0, t1, 1.08], ...]}`, switched on line boundaries, never above 1.10 from a 1080p source) and run `python3 tools/camera.py` before the mattes. Everything after uses `src_cam.mp4`.

**Panel layout**: `MODE` per scene is `'half'` or `'full'`; graphics in half screen stay inside x 56 to 1024 and between `safe.top` and `safe.halfLow`.

Sizes on the 1080x1920 grid: labels 18 to 22 px, body text in cards at least 28 px, titles 56 to 72 px, captures scaled so their text is at least 20 px. Isometric painter's order: smaller x+y first, lower z first.

### 6.7 Stills and the safe-area check

```bash
python3 tools/sheet.py s1 0.5,2.1,3.0,4.2,5.5,7.9 --zones     # over the real footage; red = platform UI, yellow = caption band
python3 tools/bounds.py                                         # must print OK
```

Look at every scene at its entrance, middle and just before its cut; read the full-size composites in `st_<name>/`. For a marked phrase, measure the words with `python3 tools/wordbox.py real/page.png x0 y0 x1 y1` and mark `[first.x0, line.y0, last.x1, line.y1]` mapped with `rw.map()`; never eyeball a highlight. Check every scene against their Never list.

### 6.8 Render, sound, composite

Render only after the stills and bounds pass. Split the frames over two background processes and wait for both:

```bash
N=$(ffprobe -v error -select_streams v:0 -count_packets -show_entries stream=nb_read_packets -of csv=p=0 src.mp4); H=$((N/2))
(SCALE=2 node render.js frames index.html frames4k 0 $H > ra.log 2>&1 & SCALE=2 node render.js frames index.html frames4k $H $N > rb.log 2>&1 & wait)
```

It takes several minutes per minute of video; after a small fix, re-render only the affected frames. Then the sound: edit the CUES in `sfx.py` (`transitions()` places the sound for every cut; then one cue per thing that moves, on its beat: `T` lands, `K` small parts, `steps` builds, `winopen`, `keys` typing, `M` mouse clicks, `A` air, `Pp` pops, `W` whooshes, `label` text rolls). Sparse beats busy, and only sounds in their `allowed` set play. Levels follow the voice. You can't hear the result, so ask them to check sync and level by ear.

```bash
python3 sfx.py && python3 tools/log.py 4 && nohup python3 comp.py > comp.log 2>&1 &      # ENCODE_DONE at the end of comp.log
```

`comp.py` makes the 4K upload file, a 1080p file and the ProRes 4444 overlay (with the behind-the-head cut-outs in its alpha), then a chat copy under 30 MiB.

### 6.9 Check the work

- The frame count and duration of every output equal the source.
- A contact sheet of the finished 1080p (one frame every 1.5 s), read frame by frame: every scene present, nothing over the face, nothing clipped, the caption band empty, full-screen moments where planned.
- First and last frames look finished. Every highlight frames exactly its words.
- Every claim, number and name on screen matches its source.
- Nothing from their Never list appears, on screen or in sound.
- `sfx.py` printed a sensible event count and a peak with no clipping.

### 6.10 Deliver

Name the files from their design system, by default:
1. `<Name>_with_animations_4K.mp4` (the upload file)
2. `<Name>_with_animations.mp4` (the copy under 30 MiB; also send it in the conversation)
3. `<Name>_overlay_ProRes4444_alpha_IN-00-00-00-00.mov` (graphics only, transparent, starts at 0:00)
4. `<Name>_SFX_stem_IN-00-00-00-00.wav` (effects only, 48 kHz 24-bit, starts at 0:00)
5. `<Name>_framing.txt` (punch-in timecodes and scales, behind-the-head and full-screen ranges, for matching in their editor)

If their computer is linked and they named a folder, write the files there. Large files go over in pieces: `split -b 11M -d -a 3 big.mp4 big.part.`, then `gzip -n big.part.000` (a piece that starts with a media header can get altered in transit), reassemble on their computer, check `sha256sum` against the original, and remove the pieces (ask for delete permission once, saying it is only for the temporary pieces). On later rounds overwrite the same names. Without a linked computer, send the chat copy and say the large files can go to their computer once it is linked. If asked, add a short description in their voice, call to action first.

### 6.11 Talk to it like an editor

Lead with what is ready and where; then only what they need to check by ear or eye. Then take notes the way an editor would. Notes come back short; fix them, re-render only what changed, and replace the files under the same names.

| Note | Where it goes |
|---|---|
| "this text is too small" | the type scale in their design system (one size for every scene of that kind), or that element |
| "that sound is too loud" / "too quiet" | that cue's level, or `SFX_PROFILE.master` if it is all of them |
| "too much going on" | remove elements; slower pace in the design system |
| "too slow" / "too fast" | entrance duration, or the pace |
| "it covers my face" | move it above the head, or put it behind the head (6.6) |
| "I don't like that transition" | `TRANS` for that cut, or the default in `STYLE.transition` |
| "that doesn't look like me" | back to their references: restyle the component in `components.js` |
| "nothing happens there" | add a graphic on that word (and log it) |

Use `edit_log.md` to find the moment they mean ("the folder at 0:41" is the item at 41 s). A note that should hold for every video ("never cover my face", "no blue", "keep the captions room", "always a typing effect") is a standing rule: add it to their design system and update their editing skill. If they re-export their footage after you built the overlay, check alignment first: `python3 tools/align.py old.mp4 new.mp4`.

## 7. Lessons that hold for everyone

- Measure, never guess: the head position, the caption band, word boxes, the lowest painted row.
- Show a style change as a short A and B in context before rebuilding a whole video. A rejected direction goes into Never with the reason.
- Real material mixed with illustration reads as more credible than illustration alone; keep real material unedited and legible.
- Quick cuts suit runs of real material; calmer transitions suit explanations. The design system sets the default; the content sets the exceptions.
- One or two full-screen moments land harder than many.
- Every frame is a function of time: no unseeded randomness and no state between frames, so any frame renders alone and partial re-renders are safe.
- The ProRes overlay is far over 30 MiB, so it only ever goes to their computer.

## 8. Never in this skill

- No house style, no fixed palette, font or component look carried from one person to another.
- No copying of any reference's graphics, characters, layouts or signature effects.
- No graphics over the face, no outline round the person, no change to their room unless they ask.
- Nothing from their Never list, ever.

## 9. Platform safe zones (1080x1920)

| Platform | Top header | Sides | Bottom UI from | Buttons column |
|---|---|---|---|---|
| Instagram Reels | 230 | 56 | 1725 | x over 908, y over 1300 |
| TikTok | 250 | 60 | 1550 | x over 900, y over 1000 |
| YouTube Shorts | 230 | 56 | 1550 | x over 900, y over 1100 |

These are approximate and change with app versions; when posting to several platforms use the strictest value of each. They fill `STYLE.safe`, with the caption band from their answer.

## 10. The engine

Write these files exactly. Per person: `style.js` and `components.js` (from their design system), `board.js` (their board). Per video: `video.js`, `camera.json`, `occlude.json`, `edit_log.json` and the CUES in `sfx.py`. `video.js` below is a working example to copy from: two floating scenes over the speaker's room (one running behind the head) and one full-screen moment with a real capture.

### `index.html`
```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<style>
  *{box-sizing:border-box;margin:0;padding:0}
  html,body{width:1080px;height:1920px;background:transparent;overflow:hidden}
  body{-webkit-font-smoothing:antialiased;text-rendering:geometricPrecision}
  .slot,.inner,.slot canvas,.dom,.scn,.layer{position:absolute;left:0;top:0;width:1080px;height:1920px}
  .slot{overflow:hidden} .layer{overflow:visible}
  .rimg{position:absolute;overflow:hidden;background:#fff;transform-origin:50% 50%}
  .rimg img{position:absolute;left:0;top:0;display:block;max-width:none}
</style>
</head>
<body>
  <div class="slot" id="slot0"><div class="inner"><canvas></canvas><svg class="layer vb" viewBox="0 0 1080 1920"></svg><div class="dom"></div><svg class="layer vt" viewBox="0 0 1080 1920"></svg></div></div>
  <div class="slot" id="slot1"><div class="inner"><canvas></canvas><svg class="layer vb" viewBox="0 0 1080 1920"></svg><div class="dom"></div><svg class="layer vt" viewBox="0 0 1080 1920"></svg></div></div>
  <svg class="layer" id="ovl" viewBox="0 0 1080 1920"></svg>
  <script src="style.js"></script>
  <script src="core.js"></script>
  <script src="components.js"></script>
  <script src="timeline.js"></script>
  <script src="logos.js"></script>
  <script src="video.js"></script>
</body>
</html>
```

### `style.js` (their tokens; these starting values are neutral placeholders)
```js
// STYLE: their design system's tokens. Change the look here (and in components.js), never inside core.js or timeline.js.
const FS = 'node_modules/@fontsource/';
const STYLE = {
  canvas: { w: 1080, h: 1920, panel: 952 },             // panel layout only: the row where the speaker footage begins (measure it)
  graphicsOnTop: true,                                   // false when the speaker is on top and the graphics sit underneath
  font: { sans: 'Inter', mono: 'JetBrains Mono' },       // their fonts: any Google font via npm i @fontsource/<slug>
  fontFiles: [                                           // [family, file, weight]; every weight used must be listed
    ['Inter', FS + 'inter/files/inter-latin-400-normal.woff2', 400], ['Inter', FS + 'inter/files/inter-latin-500-normal.woff2', 500],
    ['Inter', FS + 'inter/files/inter-latin-600-normal.woff2', 600], ['Inter', FS + 'inter/files/inter-latin-700-normal.woff2', 700],
    ['JetBrains Mono', FS + 'jetbrains-mono/files/jetbrains-mono-latin-400-normal.woff2', 400], ['JetBrains Mono', FS + 'jetbrains-mono/files/jetbrains-mono-latin-500-normal.woff2', 500],
    ['JetBrains Mono', FS + 'jetbrains-mono/files/jetbrains-mono-latin-700-normal.woff2', 700],
  ],
  layout: 'float',                                       // 'float': speaker full frame, graphics float above the head, scenes transparent
                                                         //   except full-screen moments | 'panel': graphics in a panel above (or below) the speaker
  pal: {                                                 // neutral starting point; the person's design system replaces all of it
    bg: '#ffffff', bgAlt: '#e8eefc', dark: '#0e1116',    // the three backgrounds full-screen scenes rotate through
    ink: '#0e1116', mute: '#5f6672', faint: 'rgba(14,17,22,.16)',
    accent: '#2f6bff', accentDark: '#1f4fd1', accentLight: '#dbe5ff',
    ditherOnLight: '#dbe5ff', ditherOnDark: '#2f6bff', ditherOnAlt: '#ffffff',
  },
  texture: 'flat',                                       // full-screen backgrounds: 'flat' | 'gradient' | 'grain' | 'dither'
  chrome: 'modern',                                      // 'modern' (rounded cards, soft shadow) | 'retro' (1-bit windows, square corners)
  highlight: 'marker',                                   // how words are marked on captures: 'marker' | 'box' | 'underline' | 'ants'
  overshoot: true,                                       // entrances overshoot a little and settle (snappy)
  motionStep: 30,                                        // 30 = smooth; 12 = stepped, slightly laggy retro motion
  transition: { type: 'hard' },                          // default between scenes; see timeline.js for every type
  safe: { top: 230, side: 56, bottom: 1725, btnX: 908, btnY: 1300,       // platform UI: header, side crop, caption, buttons
          halfLow: 870, fullCapTop: 1590, fullCapBottom: 1720 },         // caption room. float layout: fullCap = where their captions sit
                                                                         // (kept empty always). panel layout: halfLow = the graphics' limit
                                                                         // beside the seam; fullCap = the band kept empty in full screen
};
```

### `components.js` (their own components)
```js
// ---------------------------------------------------------------------------
// components.js: the person's own components, drawn from their design system (built once at setup, saved in their editing skill).
// Restyle or replace anything here from their references: cards, labels, stickers, lower thirds, icons, characters.
// Use only tokens from style.js (P_, STYLE.font, RR) so a palette or font change carries through every video.
// ---------------------------------------------------------------------------
// example: a label pill in their accent, centred at cx (replace with their own label style)
function pill(cx, y, text, o = {}) {
  const fs = o.fs || 26, w = textW(text, fs, STYLE.font.sans, 700) + fs * 1.4, h = fs * 1.7;
  return rectR(cx - w / 2, y - h / 2, w, h, Math.min(h / 2, RR * 2 || 0), o.bg || P_.accent) + sans(cx, y + fs * .35, text, fs, { fw: 700, col: o.col || '#ffffff', anchor: 'middle', ls: '0' });
}
```

### `core.js` (drawing toolkit)
```js
// ---------------------------------------------------------------------------
// core.js: the drawing toolkit. Every frame is a pure function of time; nothing here keeps state between frames.
// Coordinates are on a 1080x1920 grid. Scenes return { vb, vt, vx }: svg under the DOM layer, svg over it, and svg
// drawn over the footage (unclipped, for logo pops beside the speaker).
// ---------------------------------------------------------------------------
const clamp = (x, a = 0, b = 1) => Math.min(b, Math.max(a, x));
const lerp = (a, b, u) => a + (b - a) * u;
const f2 = n => (Math.round(n * 100) / 100).toString();
const E = {
  lin: x => x, out3: x => 1 - (1 - x) ** 3, out4: x => 1 - (1 - x) ** 4,
  io2: x => x < .5 ? 2 * x * x : 1 - ((-2 * x + 2) ** 2) / 2,
  back: x => { const c1 = 1.55, c3 = c1 + 1; return 1 + c3 * (x - 1) ** 3 + c1 * (x - 1) ** 2; },
};
const qt = t => Math.floor(t * STYLE.motionStep + 1e-6) / STYLE.motionStep;            // time on the motion beat
const sq = (t, t0, d, e = E.out3) => e(clamp((qt(t) - t0) / d));                      // eased 0..1 from t0 over d
const ENTER = STYLE.overshoot ? E.back : E.out3;                                     // entrance ease: settle, or overshoot and settle
const rise = (t, t0, d = .5) => STYLE.motionStep >= 30 ? sq(t, t0, d, ENTER) : Math.ceil(sq(t, t0, d, ENTER) * 12) / 12;   // 0..1 (stepped in retro)
const dIn = (t, t0, d = .25) => STYLE.motionStep >= 30 ? clamp((t - t0) / d) : Math.ceil(clamp((qt(t) - t0) / d) * 8) / 8;   // fade in
const hsh = (i, s = 0) => { const x = Math.sin(i * 127.1 + s * 311.7 + 17.13) * 43758.5453; return x - Math.floor(x); };
const esc = s => String(s).replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;');
const P_ = STYLE.pal;
let CTX = null, PEND = [];                                                            // CTX: the active scene's canvas; PEND: images still decoding
const MCTX = document.createElement('canvas').getContext('2d');                       // for measuring text
const $ = (s, r = document) => r.querySelector(s);
function mk(tag, cls, html, parent) { const e = document.createElement(tag); if (cls) e.className = cls; if (html != null) e.innerHTML = html; if (parent) parent.appendChild(e); return e; }

// ---- svg primitives --------------------------------------------------------
const rect = (x, y, w, h, fill, extra = '') => `<rect x="${f2(x)}" y="${f2(y)}" width="${f2(Math.max(0, w))}" height="${f2(Math.max(0, h))}" fill="${fill}" ${extra}/>`;
const rectR = (x, y, w, h, r, fill, extra = '') => `<rect x="${f2(x)}" y="${f2(y)}" width="${f2(w)}" height="${f2(h)}" rx="${r}" fill="${fill}" ${extra}/>`;
const circ = (x, y, r, fill, extra = '') => `<circle cx="${f2(x)}" cy="${f2(y)}" r="${f2(r)}" fill="${fill}" ${extra}/>`;
const line = (a, b, col, sw = 1.6, extra = '') => `<line x1="${f2(a[0])}" y1="${f2(a[1])}" x2="${f2(b[0])}" y2="${f2(b[1])}" stroke="${col}" stroke-width="${sw}" stroke-linecap="round" ${extra}/>`;
const poly = (pts, fill, stroke = 'none', sw = 1.6) => `<polygon points="${pts.map(p => f2(p[0]) + ',' + f2(p[1])).join(' ')}" fill="${fill}" stroke="${stroke}" stroke-width="${sw}" stroke-linejoin="round"/>`;
const grp = (inner, op = 1, tr = '') => (op <= .003 || !inner) ? '' : `<g${op < 1 ? ` opacity="${f2(op)}"` : ''}${tr ? ` transform="${tr}"` : ''}>${inner}</g>`;
const scaleAbout = (cx, cy, s) => `translate(${f2(cx)},${f2(cy)}) scale(${f2(s)}) translate(${f2(-cx)},${f2(-cy)})`;
// text: sans for reading, mono for labels and UI
const sans = (x, y, s, fs, o = {}) => `<text x="${f2(x)}" y="${f2(y)}" font-family="${STYLE.font.sans}" font-size="${fs}" font-weight="${o.fw || 600}" fill="${o.col || P_.ink}" letter-spacing="${o.ls ?? '-.02em'}" text-anchor="${o.anchor || 'start'}">${esc(s)}</text>`;
const mono = (x, y, s, fs, o = {}) => `<text x="${f2(x)}" y="${f2(y)}" font-family="${STYLE.font.mono}" font-size="${fs}" font-weight="${o.fw || 500}" fill="${o.col || P_.ink}" letter-spacing="${o.ls ?? '.06em'}" text-anchor="${o.anchor || 'start'}">${esc(s)}</text>`;
function textW(s, fs, family = STYLE.font.sans, fw = 600) { MCTX.font = `${fw} ${fs}px "${family}"`; return MCTX.measureText(s).width; }
const monoW = (s, fs, ls = .06) => textW(s, fs, STYLE.font.mono, 500) + s.length * fs * ls;
const typed = (s, t, t0, cps = 36) => s.slice(0, Math.max(0, Math.floor((qt(t) - t0) * cps)));

// ---- isometric -------------------------------------------------------------
// o = { x, y, s }: screen origin and scale. x runs down-right, y down-left, z up.
const C30 = Math.cos(Math.PI / 6);
const P = (o, x, y, z = 0) => [o.x + (x - y) * C30 * o.s, o.y + (x + y) * .5 * o.s - z * o.s];
const ST = {
  white: { top: '#ffffff', left: '#ececf2', right: '#d6d6e0', stroke: 'rgba(11,11,14,.85)' },
  accent: { top: P_.accentLight, left: P_.accent, right: P_.accentDark, stroke: 'rgba(11,11,14,.85)' },
  dark: { top: '#2a2a32', left: '#1c1c22', right: '#141419', stroke: 'rgba(255,255,255,.6)' },
  plate: { top: '#ffffff', left: '#f4f4f7', right: '#e6e6ec', stroke: 'rgba(11,11,14,.8)' },
  plateDark: { top: '#15151b', left: '#101015', right: '#0b0b0f', stroke: 'rgba(255,255,255,.55)' },
  ghost: { top: 'rgba(255,255,255,.3)', left: 'rgba(255,255,255,.15)', right: 'rgba(255,255,255,.1)', stroke: 'rgba(11,11,14,.45)' },
};
function box(o, b, st, opt = {}) {
  const { x, y, z = 0, w, d, h } = b, z1 = z + h, sw = opt.sw || 1.6;
  let s = '';
  if (h > .01) {
    s += poly([P(o, x, y + d, z), P(o, x + w, y + d, z), P(o, x + w, y + d, z1), P(o, x, y + d, z1)], st.left, st.stroke, sw);
    s += poly([P(o, x + w, y + d, z), P(o, x + w, y, z), P(o, x + w, y, z1), P(o, x + w, y + d, z1)], st.right, st.stroke, sw);
  }
  if (opt.stripes) for (let zi = z + opt.stripes; zi < z1 - 1; zi += opt.stripes) s += `<polyline points="${[P(o, x, y + d, zi), P(o, x + w, y + d, zi), P(o, x + w, y, zi)].map(p => f2(p[0]) + ',' + f2(p[1])).join(' ')}" fill="none" stroke="${st.stroke}" stroke-opacity=".3" stroke-width="${sw * .8}"/>`;
  s += poly([P(o, x, y, z1), P(o, x + w, y, z1), P(o, x + w, y + d, z1), P(o, x, y + d, z1)], st.top, st.stroke, sw);
  if (opt.grid) for (let i = 1; i < opt.grid; i++) {
    s += line(P(o, x + w * i / opt.grid, y, z1), P(o, x + w * i / opt.grid, y + d, z1), opt.gs || 'rgba(11,11,14,.1)', sw * .8);
    s += line(P(o, x, y + d * i / opt.grid, z1), P(o, x + w, y + d * i / opt.grid, z1), opt.gs || 'rgba(11,11,14,.1)', sw * .8);
  }
  return s;
}
const plate = (o, cx, cy, size, st = ST.plate, opt = {}) => box(o, { x: cx - size / 2, y: cy - size / 2, z: -(opt.th ?? 12), w: size, d: size, h: opt.th ?? 12 }, st, { grid: opt.grid ?? 4, gs: opt.gs });
const tower = (o, x, y, w, h, st, opt = {}) => box(o, { x: x - w / 2, y: y - w / 2, z: opt.z || 0, w, d: w, h }, st, { stripes: opt.stripes ?? 22 });
// characters: a voxel person and a voxel robot (use the robot for AI/agents, consistently)
function person(o, x, y, z, k = 1, op = {}) {
  const body = op.body || ST.white, legs = op.legs || (op.dark ? ST.dark : { ...ST.dark, stroke: 'rgba(11,11,14,.9)' }), head = op.head || ST.white, la = op.arm || 0;
  const B = (bx, by, bz, w, d, h, st) => box(o, { x: x + bx * k, y: y + by * k, z: z + bz * k, w: w * k, d: d * k, h: h * k }, st);
  let s = B(-11, -5, 0, 9, 10, 30, legs) + B(2, -5, 0, 9, 10, 30, legs) + B(-19, -4, 34 + la, 6, 8, 26, body) + B(-13, -7, 30, 26, 14, 36, body) + B(13, -4, 34 - la, 6, 8, 26, body) + B(-10, -10, 68, 20, 20, 20, head) + B(-10.5, -10.5, 86, 21, 21, 6, legs);
  const e1 = P(o, x - 4 * k, y + 10 * k, z + 79 * k), e2 = P(o, x + 4 * k, y + 10 * k, z + 79 * k);
  return s + circ(e1[0], e1[1], 1.9 * k * o.s, '#18191b') + circ(e2[0], e2[1], 1.9 * k * o.s, '#18191b');
}
function robot(o, x, y, z, k = 1, op = {}) {
  const body = op.body || ST.accent, joint = op.joint || (op.dark ? ST.dark : { ...ST.dark, stroke: 'rgba(11,11,14,.9)' }), head = op.head || ST.white, la = op.arm || 0;
  const B = (bx, by, bz, w, d, h, st) => box(o, { x: x + bx * k, y: y + by * k, z: z + bz * k, w: w * k, d: d * k, h: h * k }, st);
  let s = B(-16, -12, 0, 32, 24, 10, joint) + B(-6, -6, 10, 12, 12, 14, joint) + B(-23, -4, 30 + la, 7, 8, 24, joint) + B(-16, -11, 24, 32, 22, 32, body) + B(16, -4, 30 - la, 7, 8, 24, joint) + B(-12, -10, 58, 24, 20, 20, head);
  s += poly([P(o, x - 9 * k, y + 10 * k, z + 64 * k), P(o, x + 9 * k, y + 10 * k, z + 64 * k), P(o, x + 9 * k, y + 10 * k, z + 72 * k), P(o, x - 9 * k, y + 10 * k, z + 72 * k)], '#18191b');
  const a = P(o, x, y, z + 78 * k), a2 = P(o, x, y, z + 88 * k);
  return s + line(a, a2, '#18191b', 2) + circ(a2[0], a2[1], 3 * k, P_.accent);
}

// ---- backgrounds (canvas) -------------------------------------------------
const BAYER = (() => { const m = [[0, 2], [3, 1]]; let b = m; for (let k = 0; k < 2; k++) { const n = b.length, o = []; for (let y = 0; y < n * 2; y++) { o.push([]); for (let x = 0; x < n * 2; x++) o[y].push(4 * b[y % n][x % n] + m[Math.floor(y / n)][Math.floor(x / n)]); } b = o; } return b; })();
const vn = (x, y, s) => { const xi = Math.floor(x), yi = Math.floor(y), xf = x - xi, yf = y - yi, u = xf * xf * (3 - 2 * xf), v = yf * yf * (3 - 2 * yf), h = (a, b) => hsh(a * 57 + b * 131, s);
  return lerp(lerp(h(xi, yi), h(xi + 1, yi), u), lerp(h(xi, yi + 1), h(xi + 1, yi + 1), u), v); };
const fbm = (x, y, s) => .55 * vn(x, y, s) + .3 * vn(x * 2.03 + 3.1, y * 2.03 - 1.7, s + 7) + .15 * vn(x * 4.1 - 5.3, y * 4.1 + 2.2, s + 13);
function ditherField(t, col, seed, o = {}) {
  const c = o.cell || 8, d = o.dot || 4, sp = o.speed ?? .06, lo = o.lo ?? .42, hi = o.hi ?? .86, H = o.h || STYLE.canvas.h;
  CTX.save(); CTX.fillStyle = col; CTX.globalAlpha = o.op ?? 1;
  for (let j = 0, y = 0; y < H; y += c, j++) for (let i = 0, x = 0; x < STYLE.canvas.w; x += c, i++) {
    const v = clamp((fbm(x * .0036 + t * sp, y * .0036 - t * sp * .6, seed) - lo) / (hi - lo));
    if (v > (BAYER[j & 7][i & 7] + .5) / 64) CTX.fillRect(x + (c - d) / 2, y + (c - d) / 2, d, d);
  }
  CTX.restore();
}
// kind: 'light' | 'alt' | 'dark'. STYLE.texture: 'flat' | 'gradient' (a soft tint towards one corner) | 'grain' (fine film grain,
// moving on the beat) | 'dither' (a drifting ordered-dither pattern). In the float layout only full-screen moments call background().
const GRAIN = document.createElement('canvas'); GRAIN.width = 540; GRAIN.height = 960;
function grain(t, seed, dark) {
  const g = GRAIN.getContext('2d'), im = g.createImageData(540, 960), d = im.data; let x = (Math.floor(t * 12) * 7919 + seed * 104729) >>> 0;
  for (let i = 0; i < d.length; i += 4) { x = (x * 1664525 + 1013904223) >>> 0; const v = x >>> 24; d[i] = d[i + 1] = d[i + 2] = dark ? 255 : 0; d[i + 3] = v > 200 ? (v - 200) * .5 : 0; }
  g.putImageData(im, 0, 0); CTX.save(); CTX.imageSmoothingEnabled = false; CTX.drawImage(GRAIN, 0, 0, STYLE.canvas.w, STYLE.canvas.h); CTX.restore();
}
function background(kind, t, seed) {
  if (window.NOBG) return;                                                            // the bounds check renders without backgrounds
  const bg = kind === 'dark' ? P_.dark : kind === 'alt' ? P_.bgAlt : P_.bg, tex = STYLE.texture || (STYLE.dither ? 'dither' : 'flat');
  CTX.fillStyle = bg; CTX.fillRect(0, 0, STYLE.canvas.w, STYLE.canvas.h);
  if (tex === 'dither') ditherField(t, kind === 'dark' ? P_.ditherOnDark : kind === 'alt' ? P_.ditherOnAlt : P_.ditherOnLight, seed, kind === 'alt' ? { op: .9 } : {});
  if (tex === 'gradient') { const g = CTX.createLinearGradient(0, 0, STYLE.canvas.w, STYLE.canvas.h); g.addColorStop(0, 'rgba(0,0,0,0)');
    g.addColorStop(1, kind === 'dark' ? P_.accentDark : kind === 'alt' ? P_.accentLight : P_.bgAlt); CTX.save(); CTX.globalAlpha = kind === 'dark' ? .45 : .8; CTX.fillStyle = g; CTX.fillRect(0, 0, STYLE.canvas.w, STYLE.canvas.h); CTX.restore(); }
  if (tex === 'grain') grain(t, seed, kind === 'dark');
}

// ---- windows, chips, highlights ------------------------------------------
// a window opens at t0 (retro: stepped zoom rectangles from src; modern: a quick rise). returns { s, open }
function win(x, y, w, h, title, t, t0, o = {}) {
  const dark = o.dark, ring = dark ? 'rgba(255,255,255,.4)' : 'rgba(11,11,14,.7)', bg = dark ? '#1b1b21' : '#ffffff', fg = dark ? '#ffffff' : P_.ink;
  const q = qt(t) - t0, dur = .25;
  let s = '';
  if (q < 0) return { s, open: false };
  if (STYLE.chrome === 'retro') {
    if (q < dur) { const src = o.src || [x + w / 2, y + h / 2, 0, 0];
      for (let k = 0; k < 3; k++) { const u = E.out3(clamp((q - k / 12) / (dur - 2 / 12))); if (q - k / 12 < 0) continue;
        s += rect(lerp(src[0], x, u), lerp(src[1], y, u), lerp(src[2], w, u), lerp(src[3], h, u), 'none', `stroke="${ring}" stroke-width="1.6" opacity="${f2(1 - k * .3)}"`); }
      return { s, open: false }; }
    s += rect(x + .8, y + .8, w - 1.6, h - 1.6, bg, `stroke="${ring}" stroke-width="1.6"`) + rect(x + 8.8, y + 46.8, w - 17.6, h - 55.6, dark ? '#121216' : '#ffffff', `stroke="${ring}" stroke-width="1.6"`);
    s += mono(x + 14, y + 30, title, o.fs || 20, { col: fg, fw: 400, ls: '0' }) + circ(x + w - 25, y + 23, 11, fg) + `<path d="M${f2(x + w - 29.2)} ${f2(y + 18.8)}l8.4 8.4M${f2(x + w - 20.8)} ${f2(y + 18.8)}l-8.4 8.4" stroke="${bg}" stroke-width="2.2" stroke-linecap="round"/>`;
    if (o.right) s += mono(x + w - 48, y + 30, o.right, o.fs || 20, { col: fg, fw: 400, ls: '0', anchor: 'end' });
    return { s, open: true };
  }
  const u = sq(t, t0, .35, E.out4), dy = (1 - u) * 18;
  s += `<g opacity="${f2(clamp(u * 2))}" transform="translate(0,${f2(dy)})"><rect x="${x}" y="${y + 10}" width="${w}" height="${h}" rx="22" fill="rgba(20,16,50,.10)"/>` + rectR(x, y, w, h, 22, bg, `stroke="${dark ? 'rgba(255,255,255,.12)' : 'rgba(11,11,14,.08)'}"`) +
    sans(x + 24, y + 38, title, 20, { fw: 500, col: dark ? '#c9c9d6' : P_.mute, ls: '0' }) + (o.right ? sans(x + w - 24, y + 38, o.right, 20, { fw: 500, col: P_.mute, ls: '0', anchor: 'end' }) : '') + '</g>';
  return { s, open: u > .5 };
}
const RR = STYLE.chrome === 'modern' ? 12 : 0;                                       // corner radius for chips and cards
// a mono label on a solid chip, centred at cx (readable on any pattern)
function chip(cx, y, label, o = {}) { const fs = o.fs || 18, w = monoW(label, fs, .1) + 24; return rect(cx - w / 2, y - fs * 1.1, w, fs * 1.75, o.bg || P_.ink, `rx="${RR}" stroke="${o.bg || P_.ink}" stroke-width="2"`) + mono(cx, y + fs * .02, label, fs, { col: o.col || '#ffffff', fw: 700, ls: '.1em', anchor: 'middle' }); }
// marching-ants outline (for marking words on screenshots): two dashed rects offset by one dash
function marquee(x, y, w, h, t, c1 = '#ffffff', c2 = P_.accent) {
  const off = -Math.floor(t * 12) * 3, r = `x="${f2(x)}" y="${f2(y)}" width="${f2(w)}" height="${f2(h)}" fill="none" stroke-width="2.4"`;
  return `<rect ${r} stroke="${c1}" stroke-dasharray="6 6" stroke-dashoffset="${off}"/><rect ${r} stroke="${c2}" stroke-dasharray="6 6" stroke-dashoffset="${off + 6}"/>`;
}
// mark words on a capture in the profile's highlight style: STYLE.highlight = 'ants' | 'box' | 'marker' | 'underline'
// (x, y, w, h) is the exact word box from tools/wordbox.py mapped with realWin(...).map(); t0 is the word's time
function mark(x, y, w, h, t, t0, style = STYLE.highlight || 'ants') {
  if (t < t0) return '';
  const u = sq(t, t0, .25, E.out3);
  if (style === 'ants') return marquee(x - 8, y - 6, w + 16, h + 12, t);
  if (style === 'box') return rect(x - 8, y - 6, (w + 16) * u, h + 12, 'none', `rx="${RR ? 8 : 0}" stroke="${P_.accent}" stroke-width="4"`);
  if (style === 'marker') return rect(x - 6, y - 2, (w + 12) * u, h + 4, P_.accent, `rx="${RR ? 6 : 0}" opacity=".28" style="mix-blend-mode:multiply"`);
  return rect(x, y + h + 4, w * u, 6, P_.accent, `rx="3"`);                          // underline
}
// stepped square pulses (a "ping" without sound)
function sqPulse(cx, cy, r0, t, t0, col, o = {}) { if (t < t0) return ''; const n = o.n || 6, p = Math.floor((t - t0) * 12) % (o.per || 99); if (p >= n) return ''; const rr = r0 + p * (o.grow || 10);
  return rect(cx - rr, cy - rr, rr * 2, rr * 2, 'none', `stroke="${col}" stroke-width="2.4" opacity="${f2(1 - p / n)}"`); }
// a dotted path drawn on to fraction u (pixel squares along a polyline)
function dotPath(pts, u, col, o = {}) {
  const step = o.step || 14, sz = o.sz || 5; let L = 0; const seg = [];
  for (let i = 1; i < pts.length; i++) { const d = Math.hypot(pts[i][0] - pts[i - 1][0], pts[i][1] - pts[i - 1][1]); seg.push(d); L += d; }
  const at = s => { let r = s; for (let i = 1; i < pts.length; i++) { if (r <= seg[i - 1]) { const k = r / Math.max(1e-6, seg[i - 1]); return [lerp(pts[i - 1][0], pts[i][0], k), lerp(pts[i - 1][1], pts[i][1], k)]; } r -= seg[i - 1]; } return pts[pts.length - 1]; };
  let d = ''; for (let s = 0; s <= L * u; s += step) { const p = at(s); d += `M${f2(p[0] - sz / 2)} ${f2(p[1] - sz / 2)}h${sz}v${sz}h${-sz}z`; }
  return d ? `<path d="${d}" fill="${col}"/>` : '';
}
// 1-bit bitmaps: rows of '.', 'B' (ink), 'W' (white), 'P' (accent); draw new icons the same way
function pixBM(rows, x, y, px, cmap = {}) {
  const cm = { B: P_.ink, W: '#ffffff', P: P_.accent, ...cmap }, paths = {};
  rows.forEach((r, j) => { for (let i = 0; i < r.length; i++) { const c = r[i]; if (c === '.') continue; (paths[c] = paths[c] || []).push(`M${f2(x + i * px)} ${f2(y + j * px)}h${px}v${px}h${-px}z`); } });
  return Object.entries(paths).map(([c, d]) => `<path d="${d.join('')}" fill="${cm[c]}"/>`).join('');
}
const BM = {
  check: ['.........PP', '........PP.', '.......PP..', 'PP....PP...', '.PP..PP....', '..PPPP.....', '...PP......'],
  warn: ['.....B.....', '....BWB....', '....BWB....', '...BWPWB...', '...BWPWB...', '..BWWPWWB..', '..BWWPWWB..', '.BWWWWWWWB.', '.BWWWPWWWB.', 'BWWWWWWWWWB', 'BBBBBBBBBBB'],
  cursor: ['B..........', 'BB.........', 'BWB........', 'BWWB.......', 'BWWWB......', 'BWWWWB.....', 'BWWWWWB....', 'BWWWWWWB...', 'BWWWWWWWB..', 'BWWWWWWWWB.', 'BWWWWWBBBBB', 'BWWBWWB....', 'BWB.BWWB...', 'BB..BWWB...', 'B....BWWB..', '.....BWWB..', '......BB...'],
};
// alert card: warning bitmap + mono label on white with an ink ring
function alertChip(cx, cy, label, o = {}) { const fs = o.fs || 18, w = monoW(label, fs, .1) + 60, h = 42;
  return rect(cx - w / 2, cy - h / 2, w, h, '#ffffff', `rx="${RR}" stroke="${P_.ink}" stroke-width="2"`) + pixBM(BM.warn, cx - w / 2 + 12, cy - 13, 2.4) + mono(cx - w / 2 + 46, cy + fs * .36, label, fs, { fw: 700, ls: '.1em' }); }
// the pointer: path keys [[x, y, t], ...] eased between keys; presses nudge it
function cursorAt(t, keys) { let x = keys[0][0], y = keys[0][1]; for (let i = 1; i < keys.length; i++) { const [x0, y0, t0] = keys[i - 1], [x1, y1, t1] = keys[i]; if (t >= t0) { const u = E.io2(clamp((t - t0) / Math.max(.001, t1 - t0))); x = lerp(x0, x1, u); y = lerp(y0, y1, u); } } return [x, y]; }
const cursor = (x, y, down = false) => STYLE.chrome === 'retro' ? `<g transform="translate(${down ? 1.5 : 0},${down ? 1.5 : 0})">${pixBM(BM.cursor, x, y, 3)}</g>`   // pixel arrow
  : `<g transform="translate(${f2(x)},${f2(y)}) scale(${down ? 1.3 : 1.4})"><path d="M0 0V30L8 23L13.5 34.5L18.5 32.5L13 21H23Z" fill="#ffffff" stroke="${P_.ink}" stroke-width="2" stroke-linejoin="round"/></g>`;   // vector arrow
const isDown = (t, clicks) => clicks.some(c => t >= c && t < c + .1);

// ---- real-world captures as DOM images -------------------------------------
// REAL = { key: [file, width, height] } is declared per video in video.js
function realImg(el, key) { const d = document.createElement('div'); d.className = 'rimg'; const im = document.createElement('img'); im.src = REAL[key][0]; d.appendChild(im); el.appendChild(d); d.style.display = 'none'; return { d, im, key }; }
// show crop [x0, y0, x1, y1] (image pixels) at screen x, y, width w; returns the shown height
function placeImg(r, on, x, y, w, crop, o = {}) {
  if (!on) { r.d.style.display = 'none'; return 0; }
  if (!r.im.complete) PEND.push(r.im.decode().catch(() => {}));
  const [x0, y0, x1, y1] = crop, k = w / (x1 - x0), h = (y1 - y0) * k, st = r.d.style;
  st.display = 'block'; st.left = f2(x) + 'px'; st.top = f2(y) + 'px'; st.width = f2(w) + 'px'; st.height = f2(h) + 'px'; st.transform = o.sc && o.sc !== 1 ? `scale(${o.sc.toFixed(4)})` : 'none';
  const is = r.im.style; is.width = f2(REAL[r.key][1] * k) + 'px'; is.left = f2(-x0 * k) + 'px'; is.top = f2(-y0 * k) + 'px';
  return h;
}
// a capture inside a window. returns { s (chrome svg for vb), open, h, map(pixel rect) -> screen rect }
function realWin(r, x, y, w, crop, title, t, t0, o = {}) {
  const cw = w - 16, ch = (crop[3] - crop[1]) * cw / (crop[2] - crop[0]), h = 46 + ch + 8;
  const ww = win(x, y, w, h, title, t, t0, o);
  const sc = o.cut ? 1 + .03 * (1 - clamp((qt(t) - t0) * 6)) : 1;              // a hard cut-in settles from 103% in two beats
  placeImg(r, ww.open, x + 8, y + 46, cw, crop, { sc });
  const k = cw / (crop[2] - crop[0]);
  return { s: ww.s, open: ww.open, h, map: ([a, b, c, d]) => [x + 8 + (a - crop[0]) * k, y + 46 + (b - crop[1]) * k, (c - a) * k, (d - b) * k] };
}
// a real logo (Simple Icons path in a 24 box)
const logo = (path, cx, cy, size, col) => `<path d="${path}" fill="${col}" transform="translate(${f2(cx - size / 2)},${f2(cy - size / 2)}) scale(${f2(size / 24)})"/>`;
```

### `timeline.js` (slots, transitions, float, half and full screen)
```js
// ---------------------------------------------------------------------------
// timeline.js: two render slots so the outgoing and incoming scenes both draw during a transition, a tile grid
// whose cells each show one scene or the other, half/full screen per scene, and the overlay layer.
// Per-video timing (T_END, TB, MODE, XT, TRANS) lives in video.js.
//
// Transition types (STYLE.transition, or per cut in TRANS[b] = { type, dur }):
//   tiles  ordered-dither tile dissolve (dur .5 reads as a soft, slightly laggy dissolve)
//   cut    the same with dur about .17: a quick two-beat tile cut
//   wipe   tiles flip left to right       iris   from the centre outwards      blocks  coarse 4x4 blocks at random
//   push   the new scene slides in from the right and pushes the old one out (dur about .35)
//   zoom   a hard cut where the new scene settles from 106% in a quarter second
//   fade   a crossfade (dur about .3)
//   hard   a straight cut
// ---------------------------------------------------------------------------
const GW = STYLE.canvas.w, GH = STYLE.canvas.h, PANEL = STYLE.canvas.panel, TOP = STYLE.graphicsOnTop !== false;
const CW = 40, HR = Math.max(1, Math.round((TOP ? PANEL : GH - PANEL) / 40)), CH = (TOP ? PANEL : GH - PANEL) / HR;
const Y0 = TOP ? 0 : PANEL - Math.ceil(PANEL / CH - 1e-6) * CH;
const NC = Math.ceil(GW / CW), NR = Math.ceil((GH - Y0) / CH - 1e-6);
const rowY = j => Y0 + j * CH;
const inHalf = j => TOP ? j < HR : rowY(j) >= PANEL - .5;
const SCENES = []; let SLOTS = [];
function scene(o) { SCENES.push(o); return o; }
const trAt = b => Object.assign({}, STYLE.transition, (typeof TRANS !== 'undefined' && TRANS[b]) || {});
const trDur = tr => (tr.type === 'hard' || tr.type === 'zoom') ? 0 : (tr.dur ?? .5);
const tq = t => STYLE.motionStep >= 30 ? t : qt(t);

function tileOrd(i, j, pat, seed) {
  const b = (BAYER[j & 7][i & 7] + .5) / 64, x = i / (NC - 1), y = j / (NR - 1);
  if (pat === 'wipe') return .8 * x + .2 * b;
  if (pat === 'rise') return .6 * (1 - y) + .4 * b;                       // bottom edge first (used to grow half -> full)
  if (pat === 'drop') return .6 * y + .4 * b;
  if (pat === 'iris') return .75 * Math.min(1, Math.hypot(x - .5, (y - .5) * GH / GW) / .9) + .25 * b;
  if (pat === 'blocks') return hsh(Math.floor(i / 4) * 7 + Math.floor(j / 4) * 13, seed);
  return b * .86 + .14 * (x + y) / 2;                                      // tiles, cut
}
const flipped = (i, j, t, t0, d, pat, seed) => d <= 0 ? t >= t0 : qt(t) >= t0 - d / 2 + tileOrd(i, j, pat, seed) * d;
function sceneAt(t) { let k = 0; while (k < TB.length && t >= TB[k]) k++; return k; }
function modeAt(s, t) { let m = MODE[s]; for (const x of XT) if (x.k === s && t >= x.t) m = x.mode; return m; }
function allowed(s, i, j, t) {                                            // may scene s draw on row j at time t?
  if (inHalf(j)) return true;
  let m = MODE[s];
  for (const x of XT) if (x.k === s && t >= x.t - (x.dur ?? .5) / 2 && flipped(i, j, t, x.t, x.dur ?? .5, TOP ? 'rise' : 'drop', 97)) m = x.mode;
  return m === 'full';
}
function activeCut(t) { for (let b = 0; b < TB.length; b++) { const d = trDur(trAt(b)); if (d > 0 && Math.abs(t - TB[b]) <= d / 2 + 1e-3) return b; } return -1; }
function pushU(b, t) { const d = trDur(trAt(b)); return E.io2(clamp((tq(t) - (TB[b] - d / 2)) / d)); }
function rowRuns(j, t) {
  const b = activeCut(t), runs = [];
  if (b >= 0 && trAt(b).type === 'fade') {                             // both scenes draw everywhere; seek() sets the opacity
    if (allowed(b, 0, j, t)) runs.push({ s: b, x0: 0, x1: GW });
    if (allowed(b + 1, 0, j, t)) runs.push({ s: b + 1, x0: 0, x1: GW });
    return runs;
  }
  if (b >= 0 && trAt(b).type === 'push') {
    const split = GW * (1 - pushU(b, t));
    if (allowed(b, 0, j, t) && split > 0) runs.push({ s: b, x0: 0, x1: split });
    if (allowed(b + 1, NC - 1, j, t) && split < GW) runs.push({ s: b + 1, x0: split, x1: GW });
    return runs;
  }
  const s0 = sceneAt(t); let run = null;
  for (let i = 0; i < NC; i++) {
    let s = s0;
    if (b >= 0) { const tr = trAt(b); s = flipped(i, j, t, TB[b], trDur(tr), tr.type, b * 3 + 11) ? b + 1 : b; }
    if (!allowed(s, i, j, t)) s = -1;
    const x0 = i * CW, x1 = Math.min(GW, (i + 1) * CW);
    if (run && run.s === s) run.x1 = x1; else { if (run && run.s >= 0) runs.push(run); run = { s, x0, x1 }; }
  }
  if (run && run.s >= 0) runs.push(run);
  return runs;
}
function slotPaths(t) {
  const P = [[], []], used = new Set();
  for (let j = 0; j < NR; j++) { const y0 = rowY(j), y1 = y0 + CH;
    for (const r of rowRuns(j, t)) { used.add(r.s); P[r.s % 2].push(`M${f2(r.x0 - .5)} ${f2(y0 - .5)}H${f2(r.x1 + .5)}V${f2(y1 + .5)}H${f2(r.x0 - .5)}Z`); } }
  return { P, used };
}
function innerTransform(s, t) {                                           // push and zoom move the whole scene
  const b = activeCut(t);
  if (b >= 0 && trAt(b).type === 'push') { const u = pushU(b, t); if (s === b) return [`translateX(${f2(-u * GW)}px)`, '']; if (s === b + 1) return [`translateX(${f2((1 - u) * GW)}px)`, '']; }
  if (s > 0 && trAt(s - 1).type === 'zoom' && t >= TB[s - 1] && t < TB[s - 1] + .3) {
    const u = sq(t, TB[s - 1], .25), half = modeAt(s, t) !== 'full', cy = half ? (TOP ? PANEL / 2 : (PANEL + GH) / 2) : GH / 2;
    return [`scale(${(1.06 - .06 * u).toFixed(4)})`, `${GW / 2}px ${f2(cy)}px`];
  }
  return ['none', ''];
}
window.INFO = t => ({ k: sceneAt(t), mode: modeAt(sceneAt(t), t), cut: activeCut(t) >= 0 || TB.some(b => Math.abs(t - b) < .2) });

async function init() {
  await Promise.all(STYLE.fontFiles.map(([fam, url, w]) => { const f = new FontFace(fam, `url(${url})`, { weight: String(w) }); document.fonts.add(f); return f.load(); }));
  const DPR = window.devicePixelRatio || 1;
  SLOTS = [0, 1].map(n => {
    const el = $('#slot' + n), inner = el.querySelector('.inner'), c = inner.querySelector('canvas');
    c.width = GW * DPR; c.height = GH * DPR; const ctx = c.getContext('2d'); ctx.setTransform(DPR, 0, 0, DPR, 0, 0);
    return { el, inner, ctx, vb: inner.querySelector('.vb'), vt: inner.querySelector('.vt'), dom: inner.querySelector('.dom') };
  });
  SCENES.forEach((s, k) => { s.k = k; s.slot = SLOTS[k % 2]; s.el = mk('div', 'scn', null, s.slot.dom); s.init && s.init(s.el); });
  if (SCENES.length !== TB.length + 1 || MODE.length !== SCENES.length) console.log(`CHECK: ${SCENES.length} scenes, ${TB.length} cuts, ${MODE.length} modes`);
}
async function seek(t) {
  t = Math.max(0, t); PEND = [];
  const { P, used } = slotPaths(t), out = [0, 1].map(() => ({ vb: '', vt: '', on: false, tr: ['none', ''] }));
  let ovl = '';                                                          // drawn over everything, unclipped: pops over the footage
  for (const s of SCENES) {
    const on = used.has(s.k); s.el.style.display = on ? 'block' : 'none'; if (!on) continue;
    CTX = s.slot.ctx; CTX.clearRect(0, 0, GW, GH);
    const r = s.draw(t) || {}, o = out[s.k % 2];
    o.vb += r.vb || ''; o.vt += r.vt || ''; o.on = true; o.tr = innerTransform(s.k, t);
    if (r.vx && sceneAt(t) === s.k) ovl += r.vx;
  }
  const fb = activeCut(t), fu = fb >= 0 && trAt(fb).type === 'fade' ? pushU(fb, t) : -1;      // crossfade: the upper slot (1) fades
  SLOTS.forEach((sl, n) => {
    sl.el.style.opacity = fu < 0 || n === 0 ? 1 : ((fb + 1) % 2 === 1 ? fu : 1 - fu).toFixed(3);
    sl.el.style.display = out[n].on && P[n].length ? 'block' : 'none';
    sl.el.style.clipPath = `path("${P[n].join('') || 'M0 0h0v0z'}")`;
    sl.inner.style.transform = out[n].tr[0]; sl.inner.style.transformOrigin = out[n].tr[1] || '50% 50%';
    sl.vb.innerHTML = out[n].vb; sl.vt.innerHTML = out[n].vt;
  });
  $('#ovl').innerHTML = ovl;
  if (PEND.length) await Promise.all(PEND);
  return true;
}
window.seek = seek;
window.addEventListener('load', async () => { await init(); window.CLIP = { T1: T_END }; await seek(Number(new URLSearchParams(location.search).get('t') || 0)); window.READY = true; });
```

### `video.js` (per video; the example)
```js
// ---------------------------------------------------------------------------
// video.js: everything that belongs to one video. Rebuilt for every video; the toolkit files never change.
// This example is the float layout (speaker full frame): A and C float above the head over the real room (no background),
// C's big plate runs behind the head (occlude.json), B is a full-screen moment with a real capture.
// ---------------------------------------------------------------------------
const T_END = 10;                                  // source duration: frames / fps
const TB = [3.4, 6.8];                             // scene switch times in seconds, each on a word from words.json
//              A       B       C
const MODE = ['full', 'full', 'full'];             // float layout: always 'full'; a scene is transparent unless it paints a background
const XT = [];                                     // in-scene switches (panel layout), e.g. { k: 2, t: 8.1, mode: 'full', dur: .5 }
const TRANS = { 0: { type: 'zoom' }, 1: { type: 'fade', dur: .3 } };   // per-cut overrides; others use STYLE.transition
const WB_DEMO = [63, 217, 647, 300];               // the phrase to mark, measured with tools/wordbox.py on the capture
const REAL = { page: ['real/sample.png', 1588, 1200] };          // captures: key -> [file, width px, height px]

// A (floating): a prompt card types what they say, an agent lands beside it; all above the head
scene({
  draw(t) {
    const w = win(110, 280, 560, 200, 'prompt.txt', t, .2, { src: [390, 380, 40, 40] });
    let vb = w.s;
    if (w.open) vb += sans(140, 400, typed('find every bug in this repo', t, .55, 30) + (Math.floor(t * 2) % 2 ? '|' : ''), 30, { fw: 500, ls: '0' });
    const o = { x: 850, y: 520, s: .8 };
    vb += grp(plate(o, 0, 0, 200), dIn(t, 1.2));
    const u = rise(t, 1.6, .42);
    if (t >= 1.6) vb += robot(o, 0, 0, (1 - u) * 140, 1.1);
    if (t >= 2.4) vb += chip(850, 640, 'AGENT READY', { bg: P_.accent });
    return { vb };
  },
});

// B (full screen): a real capture cuts in, the phrase is marked on its word, the cursor clicks, the logo pops
scene({
  init(el) { this.R = realImg(el, 'page'); },
  draw(t) {
    background('dark', t, 2);
    const rw = realWin(this.R, 110, 420, 860, [0, 0, 1588, 1200], 'github.com', t, 3.5, { dark: true, cut: true });
    let vb = rw.s, vt = '';
    if (rw.open) { const [x, y, w, h] = rw.map(WB_DEMO); vt += mark(x, y, w, h, t, 4.4); }
    const keys = [[860, 1250, 3.6], [600, 880, 4.9], [600, 880, 5.6]], [cx, cy] = cursorAt(t, keys);
    if (t >= 4.6) vt += cursor(cx, cy, isDown(t, [5.7]));
    if (t >= 6.0) vt += grp(rectR(465, 1190, 150, 150, RR, '#ffffff', `stroke="${P_.ink}" stroke-width="3"`) + logo(LOGO.github.path, 540, 1265, 96, '#181717'), 1, scaleAbout(540, 1265, lerp(.6, 1, rise(t, 6.0, .2))));
    return { vb, vt };
  },
});

// C (floating, behind the head): a big plate of towers rises above the head; its lower part sits behind the head
scene({
  draw(t) {
    const o = { x: 540, y: 560, s: 1.1 };
    let vb = plate(o, 0, 0, 380, ST.plate, { grid: 5 });
    [[-110, -60, 7.1], [90, -40, 7.3], [-20, 110, 7.5]].forEach(([x, y, t0]) => { const h = 150 * rise(t, t0, .4); if (t >= t0) vb += tower(o, x, y, 60, h, ST.accent); });
    const pts = [P(o, -110, -60, 150), P(o, 90, -40, 150), P(o, -20, 110, 150)];
    vb += dotPath(pts, sq(t, 8.0, .8, E.lin), P_.accent);
    if (t >= 8.9) vb += pixBM(BM.check, 506, 250, 6);
    return { vb };
  },
});
```

### `camera.json` (the example: one punch-in)
```json
{"face": [540, 870], "shots": [[1.8, 3.4, 1.08]]}
```

### `occlude.json` (the example: scene C behind the head)
```json
{"ranges": [[210, 299]]}
```

### `board.html`
```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<style>
  *{box-sizing:border-box;margin:0;padding:0}
  html,body{width:1080px;height:1920px;background:transparent;overflow:hidden}
  body{-webkit-font-smoothing:antialiased;text-rendering:geometricPrecision}
  .slot,.inner,.slot canvas,.dom,.scn,.layer{position:absolute;left:0;top:0;width:1080px;height:1920px}
  .slot{overflow:hidden} .layer{overflow:visible}
  .rimg{position:absolute;overflow:hidden;background:#fff;transform-origin:50% 50%}
  .rimg img{position:absolute;left:0;top:0;display:block;max-width:none}
</style>
</head>
<body>
  <div class="slot" id="slot0"><div class="inner"><canvas></canvas><svg class="layer vb" viewBox="0 0 1080 1920"></svg><div class="dom"></div><svg class="layer vt" viewBox="0 0 1080 1920"></svg></div></div>
  <div class="slot" id="slot1"><div class="inner"><canvas></canvas><svg class="layer vb" viewBox="0 0 1080 1920"></svg><div class="dom"></div><svg class="layer vt" viewBox="0 0 1080 1920"></svg></div></div>
  <svg class="layer" id="ovl" viewBox="0 0 1080 1920"></svg>
  <script src="style.js"></script>
  <script src="core.js"></script>
  <script src="components.js"></script>
  <script src="timeline.js"></script>
  <script src="logos.js"></script>
  <script src="board.js"></script>
</body>
</html>
```

### `board.js` (their design system on one page)
```js
// ---------------------------------------------------------------------------
// board.js: the person's design system on one page, drawn by the engine from style.js, so they see their look before any video.
// Fill BOARD from the interview, then: node render.js stills board.html board 1.2   -> board/t_01.20.png (send it to them)
// ---------------------------------------------------------------------------
const BOARD = {
  name: 'Your editing style',                                   // their name or handle
  feel: ['calm', 'premium', 'clear'],                           // their three words
  sounds: ['soft clicks', 'whoosh on big moments', 'typing'],  // from the sound round
  never: ['speech bubbles', 'emoji explosions', 'swipe transitions'],   // their dislikes, in their words
  iso: true,                                                    // show an isometric object (when isometric is in their vocabulary)
};
const T_END = 2, TB = [], MODE = ['full'], XT = [], TRANS = {}, REAL = {};
scene({
  draw(t) {
    background('light', t, 4);
    const L = (y, s) => mono(64, y, s, 18, { col: P_.mute, fw: 700, ls: '.14em' });
    let s = mono(64, 112, 'EDITING STYLE', 18, { col: P_.accent, fw: 700, ls: '.14em' }) + sans(64, 182, BOARD.name, 60, { fw: 700 });
    s += mono(1016, 182, BOARD.feel.join(' · ').toUpperCase(), 18, { col: P_.mute, fw: 700, ls: '.1em', anchor: 'end' });
    // colour
    s += L(258, 'COLOUR');
    [['bg', P_.bg], ['tint', P_.bgAlt], ['dark', P_.dark], ['ink', P_.ink], ['accent', P_.accent], ['accent dark', P_.accentDark], ['accent light', P_.accentLight]].forEach(([n, c], i) => {
      const x = 64 + i * 138; s += rectR(x, 278, 122, 122, RR, c, `stroke="${P_.faint}" stroke-width="2"`) + mono(x, 428, n.toUpperCase(), 14, { col: P_.ink, fw: 700, ls: '.06em' }) + mono(x, 450, c.toUpperCase(), 14, { col: P_.mute, ls: '0' }); });
    // type
    s += L(520, 'TYPE');
    s += sans(64, 680, 'Aa', 150, { fw: 700, ls: '-.04em' });
    s += sans(330, 590, `Display · ${STYLE.font.sans}`, 52, { fw: 700 }) + sans(330, 642, 'Title 36 · the line that lands', 36, { fw: 600 }) + sans(330, 684, 'Body 28 · text inside cards and windows', 28, { fw: 500, col: P_.mute });
    s += chip(330 + monoW(`LABEL · ${STYLE.font.mono}`, 18, .1) / 2 + 12, 734, `LABEL · ${STYLE.font.mono}`.toUpperCase());
    // motion: the entrance curve as it will move (stepped or smooth), and the transition
    s += L(812, 'MOTION');
    const bx = 64, by = 836, bw = 450, bh = 260; s += rectR(bx, by, bw, bh, RR, '#ffffff', `stroke="${P_.faint}" stroke-width="2"`);
    let pts = []; for (let i = 0; i <= 60; i++) { const u = i / 60, q = STYLE.motionStep >= 30 ? u : Math.floor(u * 12) / 12; pts.push([bx + 30 + u * (bw - 60), by + bh - 40 - ENTER(q) * (bh - 110)]); }
    s += `<polyline points="${pts.map(p => f2(p[0]) + ',' + f2(p[1])).join(' ')}" fill="none" stroke="${P_.accent}" stroke-width="5" stroke-linejoin="round"/>` + line([bx + 30, by + 70], [bx + bw - 30, by + 70], P_.faint, 2, 'stroke-dasharray="6 6"');
    s += mono(bx + 24, by + 40, (STYLE.motionStep >= 30 ? 'SMOOTH 30 FPS' : `STEPPED ${STYLE.motionStep} FPS`) + (STYLE.overshoot ? ' · OVERSHOOT' : ' · SETTLE'), 16, { fw: 700, col: P_.mute });
    const tr = STYLE.transition; s += sans(560, 900, 'Between scenes', 30, { fw: 700 }) + sans(560, 944, `${tr.type}${tr.dur ? ' · ' + tr.dur + ' s' : ''}`, 28, { fw: 500, col: P_.mute });
    s += sans(560, 1010, 'Words mark as', 30, { fw: 700 });
    const ww = textW('every word', 30, STYLE.font.sans, 600); s += mark(560, 1036, ww, 36, t, 0) + sans(560, 1064, 'every word', 30, { fw: 600 });
    // components
    s += L(1172, 'COMPONENTS');
    const w = win(64, 1196, 520, 250, 'window.app', t, .2); s += w.s;
    if (w.open) s += sans(96, 1302, 'A card or window', 32, { fw: 700 }) + sans(96, 1344, 'holds what you name', 28, { fw: 500, col: P_.mute }) + chip(200, 1404, 'SMALL LABEL', { bg: P_.accent });
    s += alertChip(800, 1240, 'HEADS UP') + cursor(930, 1290, false);
    if (BOARD.iso) { const o = { x: 800, y: 1390, s: .7 }; s += plate(o, 0, 0, 220) + tower(o, -40, -20, 60, 120, ST.accent) + tower(o, 50, 30, 50, 70, ST.white); }
    // texture, sound, never
    s += L(1520, 'BACKGROUNDS');
    return { vb: s, vt: textures(t) + list(1520, 'SOUND', BOARD.sounds, 590) + list(1700, 'NEVER', BOARD.never, 590, true) };
  },
});
function textures(t) {                                           // the three full-screen backgrounds, painted on the canvas
  [['light', 64], ['alt', 228], ['dark', 392]].forEach(([k, x], i) => { CTX.save(); CTX.beginPath(); CTX.rect(x, 1544, 148, 260); CTX.clip(); background(k, t, 7 + i); CTX.restore(); });
  return [64, 228, 392].map(x => rectR(x, 1544, 148, 260, RR, 'none', `stroke="${P_.faint}" stroke-width="2"`)).join('');
}
function list(y, title, items, x, cross) {
  let s = mono(x, y, title, 18, { col: P_.mute, fw: 700, ls: '.14em' });
  items.slice(0, 4).forEach((it, i) => { const yy = y + 44 + i * 40; s += (cross ? mono(x, yy, '✕', 22, { col: P_.accent, fw: 700 }) : rect(x + 2, yy - 14, 12, 12, P_.accent)) + sans(x + 34, yy, it, 26, { fw: 500 }); });
  return s;
}
```

### `render.js`
```js
// node render.js stills  <html> <outdir> t1,t2,...       stills on grey (transparency visible)
// node render.js astills <html> <outdir> t1,t2,...       stills with alpha (for compositing over the footage)
// node render.js bounds  <html> <outdir> [every=3]       alpha stills without backgrounds every N frames (+ the pop layer alone) + info.json
// SCALE=2 node render.js frames <html> <outdir> [f0] [f1]  numbered frames f_000000.png at 30 fps (2160x3840 with SCALE=2)
const { chromium } = require('playwright');
const path = require('path'), fs = require('fs');
(async () => {
  const [mode, html, out, a, b] = process.argv.slice(2), FPS = 30;
  const browser = await chromium.launch({ args: ['--font-render-hinting=none', '--disable-lcd-text', '--force-color-profile=srgb'] });
  const page = await browser.newPage({ viewport: { width: 1080, height: 1920 }, deviceScaleFactor: Number(process.env.SCALE || 1) });
  page.on('console', m => console.log('[page]', m.text()));
  page.on('pageerror', e => console.log('[pageerror]', e.message));
  if (mode === 'bounds') await page.addInitScript(() => { window.NOBG = true; });
  await page.goto('file://' + path.resolve(html));
  await page.waitForFunction(() => window.READY === true, null, { timeout: 60000 });
  await page.evaluate(() => Promise.all([...document.images].map(i => i.complete ? 1 : new Promise(r => { i.onload = i.onerror = r; }))));
  const clip = await page.evaluate(() => window.CLIP);
  fs.writeFileSync('timing.json', JSON.stringify(await page.evaluate(() => ({ T_END, TB, MODE, XT, TRANS: typeof TRANS !== 'undefined' ? TRANS : {}, transition: STYLE.transition, motionStep: STYLE.motionStep }))));
  fs.mkdirSync(out, { recursive: true });
  const shot = async (t, file, omit) => { await page.evaluate(t => window.seek(t), t); await page.screenshot({ path: path.join(out, file), omitBackground: omit }); };
  if (mode === 'stills' || mode === 'astills') {
    if (mode === 'stills') await page.evaluate(() => { document.documentElement.style.background = '#3a3a3a'; });
    for (const t of a.split(',').map(Number)) await shot(t, `t_${t.toFixed(2).padStart(5, '0')}.png`, mode === 'astills');
  } else if (mode === 'bounds') {
    await page.evaluate(() => { document.getElementById('ovl').style.display = 'none'; });
    const every = Number(a || 3), n = Math.round(clip.T1 * FPS), info = [];
    const vis = on => page.evaluate(on => { document.querySelectorAll('.slot').forEach(s => { s.style.visibility = on ? 'hidden' : ''; }); document.getElementById('ovl').style.display = on ? 'block' : 'none'; }, on);
    for (let f = 0; f < n; f += every) {
      const t = f / FPS; await shot(t, `b_${String(f).padStart(6, '0')}.png`, true);
      const ovl = await page.evaluate(() => document.getElementById('ovl').innerHTML.length > 0);    // pops over the footage: checked on their own
      if (ovl) { await vis(true); await page.screenshot({ path: path.join(out, `o_${String(f).padStart(6, '0')}.png`), omitBackground: true }); await vis(false); }
      info.push({ f, t, ovl, ...(await page.evaluate(t => window.INFO(t), t)) });
    }
    fs.writeFileSync(path.join(out, 'info.json'), JSON.stringify(info));
  } else {
    const n = Math.round(clip.T1 * FPS), f0 = a ? Number(a) : 0, f1 = b ? Math.min(n, Number(b)) : n, t0 = Date.now();
    for (let f = f0; f < f1; f++) await shot(f / FPS, `f_${String(f).padStart(6, '0')}.png`, true);
    console.log(`frames ${f0}-${f1 - 1} of ${n}: ${((Date.now() - t0) / 1000).toFixed(1)}s`);
  }
  await browser.close();
})();
```

### `asr.py`
```python
#!/usr/bin/env python3
"""Word-timed transcript. Whisper gives the best text, Parakeet gives token timestamps; print both and use Parakeet's
word times. Splits the audio into chunks under 28 s at the quietest points. Run from the project folder after:
  ffmpeg -i src.mp4 -vn -ac 1 -ar 16000 audio16k.wav
Models (GitHub releases work; Hugging Face is blocked), into $MODELS (default ~/models):
  for m in sherpa-onnx-whisper-small.en sherpa-onnx-nemo-parakeet-tdt-0.6b-v2-int8; do
    curl -sSL -o m.tar.bz2 https://github.com/k2-fsa/sherpa-onnx/releases/download/asr-models/$m.tar.bz2 && tar -xjf m.tar.bz2 && rm m.tar.bz2; done
Writes words.json: [[word, start_seconds], ...]."""
import wave, numpy as np, sherpa_onnx, json, os
M = os.environ.get('MODELS', os.path.expanduser('~/models'))
w = wave.open('audio16k.wav'); sr = w.getframerate()
a = np.frombuffer(w.readframes(w.getnframes()), dtype=np.int16).astype(np.float32) / 32768
D = len(a) / sr
# split points: the quietest 0.1 s inside each window so every chunk stays under 28 s
h = int(.02 * sr); n = len(a) // h; db = 20 * np.log10(np.sqrt((a[:n * h].reshape(n, h) ** 2).mean(1)) + 1e-9); sm = np.convolve(db, np.ones(5) / 5, 'same')
CH, s = [], 0.0
while D - s > 28:
    lo, hi = int((s + 14) / .02), int((s + 28) / .02); k = lo + int(np.argmin(sm[lo:hi])); e = round(k * .02, 2); CH.append((s, e)); s = e
CH.append((s, D))
d = f'{M}/sherpa-onnx-whisper-small.en/'
W = sherpa_onnx.OfflineRecognizer.from_whisper(encoder=d + 'small.en-encoder.int8.onnx', decoder=d + 'small.en-decoder.int8.onnx', tokens=d + 'small.en-tokens.txt', language='en', task='transcribe', num_threads=4)
d = f'{M}/sherpa-onnx-nemo-parakeet-tdt-0.6b-v2-int8/'
K = sherpa_onnx.OfflineRecognizer.from_transducer(encoder=d + 'encoder.int8.onnx', decoder=d + 'decoder.int8.onnx', joiner=d + 'joiner.int8.onnx', tokens=d + 'tokens.txt', num_threads=4, model_type='nemo_transducer')
words = []
for s, e in CH:
    st = W.create_stream(); st.accept_waveform(sr, a[int(s * sr):int(e * sr)]); W.decode_stream(st); print(f'[{s:.2f}-{e:.2f}] Whisper:', st.result.text)
    st = K.create_stream(); st.accept_waveform(sr, a[int(s * sr):int(e * sr)]); K.decode_stream(st); r = st.result; print('Parakeet:', r.text)
    cur = None
    for tok, ts in zip(r.tokens, r.timestamps):
        if tok.startswith(' ') or cur is None:
            if cur: words.append(cur)
            cur = [tok.strip(), round(s + ts, 2)]
        else: cur[0] += tok
    if cur: words.append(cur)
json.dump(words, open('words.json', 'w'))
print(' '.join(f'{w}@{t}' for w, t in words))
```

### `sfx.py`
```python
#!/usr/bin/env python3
"""Sound-effects stem: python3 sfx.py -> sfx.wav (48 kHz 24-bit stereo, the length of src.mp4) + sfx_cues.json. Needs timing.json (render.js writes it).
Set SFX_PROFILE once from the style profile; write the CUES section per video. All sounds are synthesised, dry, no reverb:
tok (something lands), tick (small parts), key (typing), mouse (button press and release), crackle (one per beat of a pixel
transition), air (high swell with nothing under 4 kHz: slides, pushes), pop (a logo or badge appears), whoosh (soft air past
the ear as something big flies in)."""
import numpy as np, wave, sys, json, math, subprocess, re
from scipy.signal import lfilter

# ---- SFX_PROFILE: set once from the style profile ---------------------------------------------------
SFX_PROFILE = {
    'allowed': {'tok', 'tick', 'key', 'mouse', 'pop', 'whoosh'},   # sounds the person likes; others are skipped silently
    'master': 0.0,                                          # dB on top of the levels below (their "louder / quieter" notes go here)
    'voice_ref': -24.6,                                     # mean voice level (dB) the levels below were balanced against
}
LV = {'tok': -28.0, 'tick': -34.5, 'key': -37.0, 'roll': -41.0, 'mouse': -21.0, 'crackle': -35.5, 'air': -36.0, 'pop': -30.0, 'whoosh': -31.0}

SR = 48000
DUR = float(subprocess.run(['ffprobe', '-v', 'error', '-show_entries', 'format=duration', '-of', 'csv=p=0', 'src.mp4'], capture_output=True, text=True).stdout)
N = int(round(DUR * SR)); mix = np.zeros((N, 2)); db = lambda x: 10 ** (x / 20); rng = np.random.default_rng(5)
TM = json.load(open('timing.json')); STEP = 1 / TM.get('motionStep', 12)
nrm = lambda x: x / (np.abs(x).max() + 1e-12)
def band(n, lo0, lo1, hi0, hi1, seed):                     # white noise: silent below lo0, full lo1..hi0, silent above hi1
    X = np.fft.rfft(np.random.default_rng(seed).standard_normal(n)); f = np.fft.rfftfreq(n, 1 / SR); g = np.zeros_like(f)
    up = (f >= lo0) & (f < lo1); g[up] = .5 - .5 * np.cos(np.pi * (f[up] - lo0) / (lo1 - lo0)); g[(f >= lo1) & (f <= hi0)] = 1
    dn = (f > hi0) & (f <= hi1); g[dn] = .5 + .5 * np.cos(np.pi * (f[dn] - hi0) / (hi1 - hi0)); return np.fft.irfft(X * g, n)
def tok(seed=0, pitch=1.0):
    n = int(.03 * SR); t = np.arange(n) / SR; r = np.random.default_rng(3000 + seed); f = 1050 * pitch * (1 + r.uniform(-.05, .05))
    body = np.sin(2 * np.pi * f * t + r.uniform(0, 6.28)) * np.exp(-t / .0042) * (1 - np.exp(-t / .0004)) + .35 * np.sin(2 * np.pi * f * 2.3 * t) * np.exp(-t / .0018)
    x = .9 * body + .55 * nrm(band(n, 900, 1500, 5000, 7500, 4000 + seed)) * np.exp(-t / .0012)
    return nrm(x * np.minimum(1, (n - np.arange(n)) / (.004 * SR)))
def tick(seed=0, pitch=1.0):
    n = int(.012 * SR); t = np.arange(n) / SR
    x = nrm(band(n, 2200 * pitch, 3200 * pitch, 7000, 10000, 5000 + seed)) * np.exp(-t / .0009) + .4 * np.sin(2 * np.pi * 2600 * pitch * t) * np.exp(-t / .0015)
    return nrm(x * np.minimum(1, (n - np.arange(n)) / (.002 * SR)))
def key(seed=0):
    n = int(.03 * SR); t = np.arange(n) / SR; r = np.random.default_rng(6000 + seed)
    a = nrm(band(n, 1200, 1800, 5200, 7500, 7000 + seed)) * np.exp(-t / .0011); d = int(r.uniform(.006, .010) * SR); b = np.zeros(n); b[d:] = a[:n - d] * .45
    return nrm((a + b + .3 * np.sin(2 * np.pi * 700 * t) * np.exp(-t / .002)) * np.minimum(1, (n - np.arange(n)) / (.003 * SR)))
def _env(t, a, d): return np.where(t < 0, 0, np.where(t < a, t / a, np.exp(-(t - a) / d)))
def _bn(n, lp, hp, seed):
    x = np.random.default_rng(seed).uniform(-1, 1, n); a = 1 - np.exp(-2 * np.pi * lp / SR); b = 1 - np.exp(-2 * np.pi * hp / SR)
    for _ in range(2): x = lfilter([a], [1, a - 1], x)
    for _ in range(2): x = x - lfilter([b], [1, b - 1], x)
    return nrm(x)
MOUSE = {'down': (.03, [(.52, .0004, .0019, .0018, 6200, 2600), (.42, .0031, .0005, .0036, 3600, 700)], (.0044, .0006, [(440, .13, .0040), (612, .1, .0052)])),
         'up': (.028, [(.46, .0008, .0005, .0016, 7400, 2200), (.36, .0021, .0010, .0042, 3400, 1100)], (.0022, .0007, [(486, .09, .0042), (598, .07, .0062)]))}
def mouse(kind, seed=0):
    dur, layers, (dl, a, parts) = MOUSE[kind]; n = int(dur * SR); t = np.arange(n) / SR; x = np.zeros(n)
    for k, (g, d0, at, dc, lp, hp) in enumerate(layers): x += g * _env(t - d0, at, dc) * _bn(n, lp, hp, 9000 + seed * 13 + k)
    for f, g, d in parts: x += g * _env(t - dl, a, d) * np.sin(2 * np.pi * f * (1 + np.random.default_rng(seed).uniform(-.03, .03)) * np.clip(t - dl, 0, None))
    fo = int(.002 * SR); x[-fo:] *= np.linspace(1, 0, fo); return nrm(x)
def crackle(seed=0, dur=.022, hold=8):
    n = int(dur * SR); x = np.repeat(np.random.default_rng(7000 + seed).uniform(-1, 1, n // hold + 1), hold)[:n]
    b = 1 - np.exp(-2 * np.pi * 1800 / SR); x = x - lfilter([b], [1, b - 1], x); return nrm(x * np.exp(-np.arange(n) / SR / .006))
def air(dur=.4, rising=True, seed=0):                      # nothing below 4 kHz, so it never muddies the voice
    n = int(dur * SR); u = np.arange(n) / n; env = np.sin(np.pi * u) ** 2.4; k = u if rising else 1 - u
    x = band(n, 4200, 5600, 8500, 11000, 100 + seed) * np.sqrt(1 - .75 * k) + band(n, 7000, 8800, 13500, 16500, 200 + seed) * np.sqrt(.25 + .75 * k)
    return nrm(x * env)
def pop(seed=0, pitch=1.0):
    n = int(.06 * SR); t = np.arange(n) / SR; f = 880 * pitch * (1 + .5 * np.exp(-t / .01))
    return nrm(np.sin(2 * np.pi * np.cumsum(f) / SR) * np.exp(-t / .016) * (1 - np.exp(-t / .0008)))
def whoosh(dur=.3, up=True, seed=0):                       # noise through a band that sweeps up (or down); no tone
    n = int(dur * SR); x = np.random.default_rng(1200 + seed).standard_normal(n); y = np.zeros(n); B = 256; zi = np.zeros(2)
    for s in range(0, n, B):
        u = (s + B / 2) / n; f0 = 700 * (5.0 ** (u if up else 1 - u)); w = 2 * np.pi * f0 / SR; al = np.sin(w) / 2.2
        y[s:s + B], zi = lfilter([al / (1 + al), 0, -al / (1 + al)], [1, -2 * np.cos(w) / (1 + al), (1 - al) / (1 + al)], x[s:s + B], zi=zi)
    u = np.arange(n) / n; pk = .62 if up else .38
    env = np.where(u < pk, np.sin(np.pi / 2 * np.minimum(u / pk, 1)) ** 2, np.clip(np.cos(np.pi / 2 * (u - pk) / (1 - pk)), 0, 1) ** 1.5)
    return nrm(y * env)

cues = []; _n = [0]
def place(kind, sig, t, g_db, pan=0.0, note=''):
    if kind not in SFX_PROFILE['allowed']: return
    i0 = int(round(t * SR)); n = min(len(sig), N - i0)
    if i0 < 0 or n <= 0: return
    l, r = np.sqrt(.5 * (1 - pan)), np.sqrt(.5 * (1 + pan))
    mix[i0:i0 + n, 0] += sig[:n] * db(g_db) * l * 1.414; mix[i0:i0 + n, 1] += sig[:n] * db(g_db) * r * 1.414; cues.append((round(t, 3), kind, note))
def nid(): _n[0] += 1; return _n[0]
def T(t, note='', d=0.0, pitch=1.0, pan=0.0): place('tok', tok(nid(), pitch), t, LV['tok'] + d, pan, note)
def K(t, note='', d=0.0, pitch=1.0, pan=0.0): place('tick', tick(nid(), pitch), t, LV['tick'] + d, pan, note)
def Y(t, note='typing', d=0.0): place('key', key(nid()), t, LV['key'] + d, rng.uniform(-.2, .2), note)
def M(t, note='click', held=.09, d=0.0): place('mouse', mouse('down', nid()), t, LV['mouse'] + d, 0, note); place('mouse', mouse('up', nid()), t + held, LV['mouse'] + d - 2.5, 0, note)
def A(t, dur=.4, rising=True, note='', d=0.0): place('air', air(dur, rising, nid()), t, LV['air'] + d, 0, note)
def Pp(t, note='', d=0.0, pitch=1.0): place('pop', pop(nid(), pitch), t, LV['pop'] + d, 0, note)
def W(t, note='', d=0.0, dur=.3, up=True): place('whoosh', whoosh(dur, up, nid()), t - dur * (.62 if up else .2), LV['whoosh'] + d, rng.uniform(-.25, .25), note)   # peaks at t
beat = lambda t: math.ceil(t / STEP - 1e-6) * STEP + .004                 # snap a cue onto the motion beat
def steps(t0, t1, note='', d=-2.0, p0=1.0, p1=1.3, every=1):            # one tick per beat while something builds
    k = math.ceil(t0 / STEP - 1e-6); n = max(1, int((t1 - t0) / STEP))
    for i in range(0, n, every): K((k + i) * STEP + .004, note, d, p0 + (p1 - p0) * i / max(1, n - 1), rng.uniform(-.3, .3))
def winopen(t0, note='window'): [K(beat(t0) + k * STEP, note, 1 - k, 1.05 + k * .12) for k in range(3)]
def keys(t0, n, cps, every=1): [Y(t0 + i / cps + .01) for i in range(0, n, every)]
def label(t0, n): [K(t0 + i * .045, 'label', LV['roll'] - LV['tick'] - 1 + rng.uniform(-2, 1), 1.3 * rng.uniform(.9, 1.1), rng.uniform(-.3, .3)) for i in range(n + 2)]
def transitions():                                                    # the right sound for every cut in timing.json
    tr0 = TM['transition']
    for b, tb in enumerate(TM['TB']):
        tr = {**tr0, **TM['TRANS'].get(str(b), {})}; ty, d = tr['type'], tr.get('dur', .5)
        if ty in ('tiles', 'cut', 'wipe', 'iris', 'blocks'):
            k0 = math.ceil((tb - d / 2) / (1 / 12) - 1e-6); nb = max(2, round(d * 12))
            for i in range(nb): place('crackle', crackle(nid(), hold=int(rng.integers(5, 12))), (k0 + i) / 12 + .004, LV['crackle'] - 2 * abs(i - (nb - 1) / 2) / max(1, (nb - 1) / 2), rng.uniform(-.35, .35), 'cut')
        elif ty == 'push': A(tb - d / 2, d + .1, True, 'push')
        elif ty == 'fade': pass                                    # a crossfade is silent
        elif ty in ('zoom', 'hard'): K(tb + .004, 'cut', -1, 1.2)

# ============================ CUES (per video) ============================
# The cues below belong to the example video.js; replace them for every video. Keep transitions().
transitions()
winopen(.2, 'prompt'); keys(.55, 27, 30, every=2); T(1.6 + .35, 'agent lands'); K(2.404, 'chip', -2, 1.3)
W(3.5, 'capture flies in', -2); K(4.4, 'mark', 0, 1.3); M(5.7, 'click'); Pp(6.0, 'logo pops', 0, 1.1)
for t0 in (7.1, 7.3, 7.5): steps(t0, t0 + .4, 'tower', -5, 1.0, 1.3, every=2)
steps(8.0, 8.8, 'trace', -4, 1.1, 1.4, every=2); T(8.9, 'check', 0, 1.2)

# ============================ LEVEL ============================
vm = float(re.search(r'mean_volume: (-?[\d.]+)', subprocess.run(['ffmpeg', '-i', 'src.mp4', '-af', 'volumedetect', '-vn', '-f', 'null', '-'], capture_output=True, text=True).stderr).group(1))
g = max(-6, min(6, vm - SFX_PROFILE['voice_ref'])) + SFX_PROFILE['master']; mix *= db(g)
peak = np.abs(mix).max()
print(f'voice mean {vm:.1f} dB -> effects {g:+.1f} dB | events {len(cues)} | peak {20 * np.log10(peak + 1e-12):.1f} dBFS')
i24 = (np.clip(mix, -1, 1) * (2 ** 23 - 1)).astype('<i4')
with wave.open(sys.argv[1] if len(sys.argv) > 1 else 'sfx.wav', 'wb') as w:
    w.setnchannels(2); w.setsampwidth(3); w.setframerate(SR); w.writeframes(np.frombuffer(i24.reshape(-1).tobytes(), dtype=np.uint8).reshape(-1, 4)[:, :3].tobytes())
json.dump(sorted(cues), open('sfx_cues.json', 'w'), indent=0)
```

### `comp.py`
```python
#!/usr/bin/env python3
"""One pass over the 4K frames gives out_4k.mp4 (upload file), out_1080.mp4 and out_overlay.mov (ProRes 4444 with alpha);
then out_chat.mp4, a re-encode of the 4K under 30 MiB for sending in chat. Run from the project folder, in the background:
    nohup python3 comp.py > comp.log 2>&1 &         (prints ENCODE_DONE at the end)
usage: python3 comp.py [frames_dir=frames4k] [src=src_cam.mp4 if it exists, else src.mp4] [sfx=sfx.wav]
Assumes 1080x1920 source at 30 fps and frames rendered with SCALE=2. For other sources change W, H, FPS."""
import cv2, numpy as np, subprocess, sys, glob, os
FR, SRC, SFX = (sys.argv[1:] + ['frames4k', 'src_cam.mp4' if os.path.exists('src_cam.mp4') else 'src.mp4', 'sfx.wav'][len(sys.argv) - 1:])[:3]   # src_cam.mp4: footage with punch-ins
W, H, FPS = 1080, 1920, 30
n_src = int(subprocess.run(['ffprobe', '-v', 'error', '-select_streams', 'v:0', '-count_packets', '-show_entries', 'stream=nb_read_packets', '-of', 'csv=p=0', SRC], capture_output=True, text=True).stdout.strip())
files = sorted(glob.glob(f'{FR}/f_*.png')); assert len(files) == n_src, f'{len(files)} frames rendered, source has {n_src}'
fc = (f"[1:v]split=2[ovA][ovB];[ovA]scale=out_color_matrix=bt709:out_range=tv,format=yuva444p[ov4];"
      f"[0:v]scale={2*W}:{2*H}:flags=lanczos+accurate_rnd:in_color_matrix=bt709:out_color_matrix=bt709,format=yuv444p[bg4];"
      f"[bg4][ov4]overlay=0:0:format=yuv444,split=2[c4a][c4b];[c4a]format=yuv420p[v4k];"
      f"[c4b]scale={W}:{H}:flags=lanczos+accurate_rnd,format=yuv420p[v1080];"
      f"[ovB]scale={W}:{H}:flags=area,scale=out_color_matrix=bt709:out_range=tv,format=yuva444p10le[vov];"
      f"[0:a][2:a]amix=inputs=2:duration=first:normalize=0,asplit=2[a1][a2]")
tags = ['-color_primaries', 'bt709', '-color_trc', 'bt709', '-colorspace', 'bt709', '-color_range', 'tv']
cmd = ['ffmpeg', '-hide_banner', '-loglevel', 'error', '-y', '-i', SRC, '-f', 'rawvideo', '-pix_fmt', 'bgra', '-s', f'{2*W}x{2*H}', '-r', str(FPS), '-i', '-', '-i', SFX, '-filter_complex', fc,
  '-map', '[v4k]', '-map', '[a1]', '-c:v', 'libx264', '-profile:v', 'high', '-preset', 'medium', '-crf', '15', '-r', str(FPS), *tags, '-c:a', 'aac', '-b:a', '320k', '-movflags', '+faststart', 'out_4k.mp4',
  '-map', '[v1080]', '-map', '[a2]', '-c:v', 'libx264', '-profile:v', 'high', '-level:v', '4.2', '-preset', 'slow', '-crf', '15', '-r', str(FPS), *tags, '-c:a', 'aac', '-b:a', '256k', '-movflags', '+faststart', 'out_1080.mp4',
  '-map', '[vov]', '-c:v', 'prores_ks', '-profile:v', '4444', '-pix_fmt', 'yuva444p10le', '-alpha_bits', '16', '-vendor', 'apl0', '-qscale:v', '9', *tags, '-r', str(FPS), 'out_overlay.mov']
ff = subprocess.Popen(cmd, stdin=subprocess.PIPE)
for i, f in enumerate(files):
    im = cv2.imread(f, cv2.IMREAD_UNCHANGED); assert im.shape[:2] == (2 * H, 2 * W), (f, im.shape)
    if im.shape[2] == 3: im = np.dstack([im, np.full(im.shape[:2], 255, np.uint8)])     # Chromium drops alpha on fully opaque frames
    mf = f'matte/m_{i:06d}.png'                                 # behind the head: the overlay's alpha times (1 - the speaker's matte)
    if os.path.exists(mf):
        m = cv2.resize(cv2.imread(mf, cv2.IMREAD_GRAYSCALE), (2 * W, 2 * H), interpolation=cv2.INTER_LINEAR).astype(np.float32) / 255
        im = im.copy(); im[:, :, 3] = (im[:, :, 3] * (1 - m)).astype(np.uint8)
    ff.stdin.write(im.tobytes())
    if i % 100 == 0: print('frame', i, flush=True)
ff.stdin.close(); print('ffmpeg exit', ff.wait(), flush=True)
for crf in (16.5, 18, 19.5, 21, 23):                       # the chat copy: from the 4K so it stays sharp, under 30 MiB
    subprocess.run(['ffmpeg', '-v', 'error', '-y', '-i', 'out_4k.mp4', '-vf', f'scale={W}:{H}:flags=lanczos', '-c:v', 'libx264', '-preset', 'slow', '-crf', str(crf), '-profile:v', 'high', '-pix_fmt', 'yuv420p',
                    *tags[:6], '-c:a', 'copy', '-movflags', '+faststart', 'out_chat.mp4'], check=True)
    if os.path.getsize('out_chat.mp4') < 30 * 2 ** 20: break
for f in ['out_4k.mp4', 'out_1080.mp4', 'out_chat.mp4', 'out_overlay.mov']: print(f, os.path.getsize(f))
print('ENCODE_DONE')
```

### `tools/camera.py`
```python
#!/usr/bin/env python3
"""Punch-ins for full-frame footage: python3 tools/camera.py -> src_cam.mp4 (comp.py, sheet.py, preview.py and matte.py use it
whenever it exists). camera.json: {"face": [x, y], "shots": [[t0, t1, scale], ...]}
Each shot scales the whole frame about the face point (between the eyes): 1.0 is the original framing, 1.08 to 1.10 a punch-in
(never above 1.10 from a 1080p source; up to 1.18 from 4K). Times outside every shot stay at 1.0. Switch on a line boundary."""
import json, subprocess, numpy as np, cv2
C = json.load(open('camera.json')); fx, fy = C['face']; SH = C['shots']
W, H, FPS = 1080, 1920, 30
dec = subprocess.Popen(['ffmpeg', '-v', 'error', '-i', 'src.mp4', '-vf', f'scale={W}:{H}', '-f', 'rawvideo', '-pix_fmt', 'bgr24', '-'], stdout=subprocess.PIPE)
enc = subprocess.Popen(['ffmpeg', '-v', 'error', '-y', '-f', 'rawvideo', '-pix_fmt', 'bgr24', '-s', f'{W}x{H}', '-r', str(FPS), '-i', '-', '-i', 'src.mp4',
                        '-map', '0:v', '-map', '1:a?', '-c:v', 'libx264', '-crf', '12', '-preset', 'fast', '-pix_fmt', 'yuv420p', '-c:a', 'copy', 'src_cam.mp4'], stdin=subprocess.PIPE)
n = 0
while True:
    buf = dec.stdout.read(W * H * 3)
    if len(buf) < W * H * 3: break
    im = np.frombuffer(buf, np.uint8).reshape(H, W, 3); t = n / FPS
    s = next((c[2] for c in SH if c[0] <= t < c[1]), 1.0)
    if abs(s - 1) > 1e-4: im = cv2.warpAffine(im, np.float32([[s, 0, fx - s * fx], [0, s, fy - s * fy]]), (W, H), flags=cv2.INTER_LANCZOS4, borderMode=cv2.BORDER_REPLICATE)
    enc.stdin.write(im.tobytes()); n += 1
enc.stdin.close(); enc.wait(); print('src_cam.mp4', n, 'frames')
```

### `tools/matte.py`
```python
#!/usr/bin/env python3
"""Behind-the-head mattes: graphics that are too big for the space above the head can sit behind it, with the room left as it is
and no outline round the person. occlude.json: {"ranges": [[f0, f1], ...]} in frames (inclusive), for the stretches where a graphic
reaches down behind the head. python3 tools/matte.py [occlude.json] -> matte/m_NNNNNN.png (1080x1920 grey, 1 = the person).
comp.py, tools/sheet.py and tools/preview.py multiply the overlay's alpha by (1 - matte) in those frames, so the ProRes overlay
stacks in the editor with no mask. About 0.7 s per frame on CPU. Needs: pip install --break-system-packages rembg onnxruntime
(the model downloads from GitHub on first use). End a range before any cut into a full-screen scene, or that scene's background
gets a head-shaped hole."""
import json, os, sys, subprocess, numpy as np, cv2
from rembg import new_session, remove
from PIL import Image
W, H, FPS = 1080, 1920, 30
R = json.load(open(sys.argv[1] if len(sys.argv) > 1 else 'occlude.json'))['ranges']; os.makedirs('matte', exist_ok=True)
SRC = 'src_cam.mp4' if os.path.exists('src_cam.mp4') else 'src.mp4'                  # the framing the viewer sees
sess = new_session('u2net_human_seg')
for f0, f1 in R:
    a0 = max(0, f0 - 1); n = f1 - a0 + 2
    raw = subprocess.run(['ffmpeg', '-v', 'error', '-ss', f'{a0 / FPS:.4f}', '-i', SRC, '-frames:v', str(n), '-vf', f'scale={W}:{H}', '-f', 'rawvideo', '-pix_fmt', 'rgb24', '-'], capture_output=True).stdout
    fr = np.frombuffer(raw, np.uint8).reshape(-1, H, W, 3)
    masks = [np.array(remove(Image.fromarray(im), session=sess, only_mask=True)).astype(np.float32) / 255 for im in fr]
    for k in range(f0, f1 + 1):                                                      # light temporal smoothing, a soft edge
        i = min(k - a0, len(masks) - 1); m = .5 * masks[i] + .25 * masks[max(0, i - 1)] + .25 * masks[min(len(masks) - 1, i + 1)]
        m = cv2.GaussianBlur(np.clip((m - .5) * 2.4 + .5, 0, 1), (0, 0), 1.0)
        Image.fromarray((m * 255).astype(np.uint8), 'L').save(f'matte/m_{k:06d}.png')
    print('range', f0, f1, flush=True)
print('MATTE_DONE')
```

### `tools/log.py`
```python
#!/usr/bin/env python3
"""The edit log: every graphic, the word it lands on, and the visual it uses, so the whole video stays consistent and the person
can talk about any moment ("the folder on 'skill' at 0:41"). Write edit_log.json while storyboarding, keep it in step with video.js:
  {"concepts": {"the skill": "folder card", "AI": "robot"},                       one visual per idea, for the whole video
   "items": [{"scene": "A", "t": 1.60, "word": "agent", "what": "robot lands on the plate", "concept": "AI", "sound": "T"}, ...]}
python3 tools/log.py [maxgap=4.0] -> checks each item against words.json (lands on that word, within 0.12 s of its start), each
concept against its one visual, gaps with nothing landing longer than maxgap seconds, the sound cues in sfx_cues.json if present,
and writes edit_log.md (a readable log to share)."""
import json, re, sys, os
maxgap = float(sys.argv[1]) if len(sys.argv) > 1 else 4.0
L = json.load(open('edit_log.json')); W = json.load(open('words.json')); items = sorted(L['items'], key=lambda x: x['t'])
norm = lambda s: re.sub(r"[^a-z0-9']", '', s.lower())
cues = json.load(open('sfx_cues.json')) if os.path.exists('sfx_cues.json') else None
T_END = json.load(open('timing.json'))['T_END'] if os.path.exists('timing.json') else None
bad = 0; md = ['| time | word | scene | what lands | idea : visual | sound |', '|---|---|---|---|---|---|']
for it in items:
    t, wd, msg = it['t'], it.get('word', ''), []
    near = min(W, key=lambda w: abs(w[1] - t)) if W else ['', 0]
    if wd:
        hits = [w for w in W if norm(w[0]) == norm(wd)]
        best = min(hits, key=lambda w: abs(w[1] - t)) if hits else None
        if not best: msg.append(f'"{wd}" is not in words.json')
        elif abs(best[1] - t) > .12: msg.append(f'"{wd}" starts at {best[1]:.2f}, not {t:.2f}')
    c = it.get('concept')
    if c and c not in L.get('concepts', {}): msg.append(f'concept "{c}" has no visual in "concepts"')
    if cues is not None and it.get('sound') and not any(abs(q[0] - t) <= .15 for q in cues): msg.append('no sound cue within 0.15 s')
    if msg: bad += 1; print(f"{t:6.2f} {it.get('scene', '')} {it.get('what', '')}: " + '; '.join(msg))
    vis = L.get('concepts', {}).get(c, '') if c else ''
    md.append(f"| {int(t // 60)}:{t % 60:05.2f} | {wd or near[0]} | {it.get('scene', '')} | {it.get('what', '')} | {(c + ' : ' + vis) if c else ''} | {it.get('sound', '')} |")
ts = [0.0] + [it['t'] for it in items] + ([T_END] if T_END else [])
for a, b in zip(ts, ts[1:]):
    if b - a > maxgap: bad += 1; print(f'{a:6.2f} to {b:.2f}: {b - a:.1f} s with nothing landing (pace limit {maxgap} s)')
open('edit_log.md', 'w').write('\n'.join(md) + '\n')
print(f'{len(items)} items, {len(L.get("concepts", {}))} ideas, edit_log.md written | ' + ('OK' if not bad else f'{bad} problems'))
```

### `tools/sheet.py`
```python
#!/usr/bin/env python3
"""Contact sheet of the animation over the real footage, for reviewing scenes.
usage (from the project folder): python3 tools/sheet.py NAME t1,t2,... [--zones]
Renders those times, composites each over the matching frame of src.mp4 and tiles them into sheet_NAME.png
(360x640 tiles, time stamped). --zones tints the platform UI zones red and the caption band yellow.
Full-size composites stay in st_NAME/ for close reading."""
import sys, subprocess, os, json
from PIL import Image, ImageDraw
import numpy as np
name, ts = sys.argv[1], [float(x) for x in sys.argv[2].split(',')]
zones = '--zones' in sys.argv
SRC = 'src_cam.mp4' if os.path.exists('src_cam.mp4') else 'src.mp4'
st = json.loads(subprocess.run(['node', '-e', "const fs=require('fs');eval(fs.readFileSync('style.js','utf8')+';console.log(JSON.stringify(STYLE))')"], capture_output=True, text=True).stdout)
S = st['safe']
subprocess.run(['node', 'render.js', 'astills', 'index.html', f'st_{name}', ','.join(map(str, ts))], check=True)
os.makedirs('.stillcache', exist_ok=True)
tiles = []
for t in ts:
    fr = f'.stillcache/{SRC[:-4]}_{t:.2f}.png'
    if not os.path.exists(fr):
        subprocess.run(['ffmpeg', '-v', 'error', '-y', '-ss', f'{t:.3f}', '-i', SRC, '-frames:v', '1', fr], check=True)
    bg = Image.open(fr).convert('RGBA').resize((1080, 1920))
    ov = Image.open(f'st_{name}/t_{t:05.2f}.png').convert('RGBA').resize((1080, 1920))
    mf = f'matte/m_{round(t * 30):06d}.png'                    # behind the head, as in comp.py
    if os.path.exists(mf):
        o = np.array(ov); o[:, :, 3] = (o[:, :, 3] * (1 - np.array(Image.open(mf).convert('L').resize((1080, 1920))) / 255)).astype(np.uint8); ov = Image.fromarray(o)
    bg.alpha_composite(ov)
    if zones:
        z = Image.new('RGBA', (1080, 1920)); d = ImageDraw.Draw(z); red, yel = (255, 0, 0, 60), (255, 220, 0, 70)
        for r in [(0, 0, 1080, S['top']), (0, 0, S['side'], 1920), (1080 - S['side'], 0, 1080, 1920), (S['btnX'], S['btnY'], 1080, 1920), (0, S['bottom'], 1080, 1920)]: d.rectangle(r, fill=red)
        d.rectangle((0, S['fullCapTop'], 1080, S['fullCapBottom']), fill=yel)
        if st.get('layout') == 'panel': d.line((0, S['halfLow'], 1080, S['halfLow']), fill=(255, 220, 0, 255), width=3)
        bg.alpha_composite(z)
    bg.convert('RGB').save(f'st_{name}/c_{t:05.2f}.jpg', quality=90)
    im = bg.convert('RGB').resize((360, 640))
    d = ImageDraw.Draw(im); d.rectangle([0, 0, 70, 22], fill=(0, 0, 0)); d.text((4, 4), f'{t:.2f}', fill=(255, 255, 0))
    tiles.append(im)
cols = min(len(tiles), 6); rows = (len(tiles) + cols - 1) // cols
sheet = Image.new('RGB', (cols * 366 - 6, rows * 646 - 6), (40, 40, 40))
for k, im in enumerate(tiles): sheet.paste(im, ((k % cols) * 366, (k // cols) * 646))
sheet.save(f'sheet_{name}.png'); print(f'sheet_{name}.png', sheet.size)
```

### `tools/bounds.py`
```python
#!/usr/bin/env python3
"""Caption and safe-area check. Renders the whole video without backgrounds every 3 frames,
then reports per scene where the graphics actually reach, against the STYLE.safe limits:
  half screen: nothing past safe.halfLow on the seam side (below it with graphics on top, above it with graphics underneath)
  full screen: nothing in the caption band safe.fullCapTop..fullCapBottom, nothing past the side margins or under the header
  pops over the footage (vx): clear of the platform UI and of the caption band (on the seam in half screen)
usage (from the project folder): python3 tools/bounds.py      -> prints OK or every breach with its time"""
import subprocess, json, glob, shutil
import numpy as np
from PIL import Image
st = json.loads(subprocess.run(['node', '-e', "const fs=require('fs');eval(fs.readFileSync('style.js','utf8')+';console.log(JSON.stringify(STYLE))')"], capture_output=True, text=True).stdout)
S, top, panel = st['safe'], st.get('graphicsOnTop', True), st['canvas']['panel']
shutil.rmtree('.bounds', ignore_errors=True)
subprocess.run(['node', 'render.js', 'bounds', 'index.html', '.bounds', '3'], check=True)
info = json.load(open('.bounds/info.json')); bad = 0; per = {}
for it in info:
    if it['cut']: continue                                     # transitions are mid-flight; check settled frames
    a = np.array(Image.open(f".bounds/b_{it['f']:06d}.png").convert('RGBA'))[:, :, 3] > 8
    rows, cols = np.where(a.any(1))[0], np.where(a.any(0))[0]
    if not len(rows): continue
    y0, y1, x0, x1 = rows.min(), rows.max(), cols.min(), cols.max()
    k = it['k']; p = per.setdefault(k, [it['mode'], 9999, 0, 9999, 0]); p[1] = min(p[1], y0); p[2] = max(p[2], y1); p[3] = min(p[3], x0); p[4] = max(p[4], x1)
    msg = []
    if it['mode'] == 'half':
        if top and y1 > S['halfLow']: msg.append(f'reaches y {y1} (half limit {S["halfLow"]})')
        if not top and y0 < S['halfLow']: msg.append(f'starts at y {y0}, too close to the seam (limit {S["halfLow"]})')
        if not top and y1 > S['bottom']: msg.append(f'reaches y {y1} (bottom UI from {S["bottom"]})')
    else:
        band = a[S['fullCapTop']:S['fullCapBottom'] + 1]
        if band.any(): msg.append(f'paints the caption band y {S["fullCapTop"]}-{S["fullCapBottom"]}')
        if y1 > S['bottom']: msg.append(f'reaches y {y1} (bottom UI from {S["bottom"]})')
        if a[S['btnY']:, S['btnX']:].any(): msg.append('touches the button column')
    if y0 < S['top'] and not (it['mode'] == 'half' and not top): msg.append(f'starts at y {y0} (header to {S["top"]})')
    if x0 < S['side'] or x1 > 1080 - S['side']: msg.append(f'x {x0}-{x1} (side margin {S["side"]})')
    if it.get('ovl'):                                          # pops over the footage: clear of the platform UI and the captions
        o = np.array(Image.open(f".bounds/o_{it['f']:06d}.png").convert('RGBA'))[:, :, 3] > 8
        lo, hi = (S['halfLow'], 2 * panel - S['halfLow']) if top else (2 * panel - S['halfLow'], S['halfLow'])
        cap = (lo, hi) if it['mode'] == 'half' else (S['fullCapTop'], S['fullCapBottom'])
        if o[cap[0]:cap[1] + 1].any(): msg.append(f'pop crosses the caption band y {cap[0]}-{cap[1]}')
        if o[S['btnY']:, S['btnX']:].any() or o[S['bottom']:].any() or o[:S['top']].any() or o[:, :S['side']].any() or o[:, 1080 - S['side']:].any(): msg.append('pop touches the platform UI zones')
    if msg: bad += 1; print(f"t {it['t']:.2f} scene {k} {it['mode']}: " + '; '.join(msg))
for k, (m, y0, y1, x0, x1) in sorted(per.items()): print(f'scene {k:2d} {m:4s}  y {y0}-{y1}  x {x0}-{x1}')
print('OK' if not bad else f'{bad} frames breach the limits')
```

### `tools/wordbox.py`
```python
#!/usr/bin/env python3
"""Find the exact pixel boxes of words in a screenshot, so an outline frames exactly the words meant.
usage: python3 tools/wordbox.py image.png x0 y0 x1 y1 [--light]     (region in image pixels; --light for light text on dark)
Prints each text line in the region and the box of every word on it: [x0, y0, x1, y1] in image pixels.
Pick the first and last word of the phrase, take [first.x0, line.y0, last.x1, line.y1], and pass it to realWin(...).map()."""
import sys
import numpy as np
from PIL import Image
f, X0, Y0, X1, Y1 = sys.argv[1], *map(int, sys.argv[2:6])
g = np.array(Image.open(f).convert('L')).astype(float)[Y0:Y1, X0:X1]
bgv = np.median(g)
ink = (g > bgv + 60) if '--light' in sys.argv else (g < bgv - 60)
rows = ink.any(1); lines = []; y = 0
while y < len(rows):
    if rows[y]:
        s = y
        while y < len(rows) and rows[y]: y += 1
        if y - s >= 6: lines.append((s, y))
    y += 1
for (a, b) in lines:
    colsum = ink[a:b].any(0); h = b - a; gap = max(6, int(h * .2)); words = []; x = 0
    while x < len(colsum):
        if colsum[x]:
            s = x; last = x
            while x < len(colsum) and (colsum[x] or x - last <= gap):
                if colsum[x]: last = x
                x += 1
            words.append((s, last + 1))
        x += 1
    print(f'line y {Y0 + a}-{Y0 + b}:', '  '.join(f'[{X0 + s}, {Y0 + a}, {X0 + e}, {Y0 + b}]' for s, e in words))
```

### `tools/preview.py`
```python
#!/usr/bin/env python3
"""Fast 1080p preview of a stretch of the video, with the footage, voice and effects: for the style test and for checking
one section without a full 4K render.
usage (from the project folder): python3 tools/preview.py NAME t0 t1 [html=index.html]   -> preview_NAME.mp4"""
import sys, subprocess, glob, os, shutil, numpy as np, cv2
name, t0, t1 = sys.argv[1], float(sys.argv[2]), float(sys.argv[3]); html = sys.argv[4] if len(sys.argv) > 4 else 'index.html'
d = f'.prev_{name}'; shutil.rmtree(d, ignore_errors=True)
SRC = 'src_cam.mp4' if os.path.exists('src_cam.mp4') else 'src.mp4'
f0, f1 = round(t0 * 30), round(t1 * 30)
mid = (f0 + f1) // 2
procs = [subprocess.Popen(['node', 'render.js', 'frames', html, d, str(a), str(b)], stdout=subprocess.DEVNULL) for a, b in ((f0, mid), (mid, f1))]
for p in procs: p.wait()
files = sorted(glob.glob(f'{d}/f_*.png'))
aud = ['-ss', f'{t0:.3f}', '-t', f'{t1 - t0:.3f}', '-i', 'sfx.wav'] if os.path.exists('sfx.wav') else ['-f', 'lavfi', '-t', f'{t1 - t0:.3f}', '-i', 'anullsrc=r=48000:cl=stereo']
fc = '[1:v]format=yuva444p[ov];[0:v][ov]overlay=0:0,format=yuv420p[v];[0:a][2:a]amix=inputs=2:duration=first:normalize=0[a]'
ff = subprocess.Popen(['ffmpeg', '-v', 'error', '-y', '-ss', f'{t0:.3f}', '-t', f'{t1 - t0:.3f}', '-i', SRC, '-f', 'rawvideo', '-pix_fmt', 'bgra', '-s', '1080x1920', '-r', '30', '-i', '-', *aud,
                       '-filter_complex', fc, '-map', '[v]', '-map', '[a]', '-c:v', 'libx264', '-crf', '20', '-preset', 'fast', '-c:a', 'aac', '-b:a', '192k', '-movflags', '+faststart', f'preview_{name}.mp4'], stdin=subprocess.PIPE)
for k, f in enumerate(files):
    im = cv2.imread(f, cv2.IMREAD_UNCHANGED)
    if im.shape[2] == 3: im = np.dstack([im, np.full(im.shape[:2], 255, np.uint8)])
    mf = f'matte/m_{f0 + k:06d}.png'                            # behind the head, as in comp.py
    if os.path.exists(mf): im[:, :, 3] = (im[:, :, 3] * (1 - cv2.imread(mf, cv2.IMREAD_GRAYSCALE).astype(np.float32) / 255)).astype(np.uint8)
    ff.stdin.write(im.tobytes())
ff.stdin.close(); ff.wait(); shutil.rmtree(d, ignore_errors=True)
print(f'preview_{name}.mp4', os.path.getsize(f'preview_{name}.mp4'))
```

### `tools/logos.js`
```js
// node tools/logos.js github cloudflare notion ...  -> logos.js with LOGO[slug] = { title, hex, path } (24x24 viewBox, from Simple Icons)
// Unknown names are listed with the closest slugs. Use the path unchanged: never redraw a logo.
const si = require('simple-icons'), fs = require('fs');
const all = Object.values(si).filter(x => x && x.slug), out = {};
for (const q of process.argv.slice(2)) {
  const hit = all.find(x => x.slug === q.toLowerCase()) || all.find(x => x.title.toLowerCase() === q.toLowerCase());
  if (hit) out[hit.slug] = { title: hit.title, hex: '#' + hit.hex, path: hit.path };
  else console.log('not found:', q, '| close:', all.filter(x => x.slug.includes(q.toLowerCase().slice(0, 4))).slice(0, 8).map(x => x.slug).join(' '));
}
fs.writeFileSync('logos.js', 'const LOGO = ' + JSON.stringify(out) + ';\n');
console.log('logos.js:', Object.keys(out).join(' '));
```

### `tools/stitch.py`
```python
#!/usr/bin/env python3
"""Stitch zoomed browser tiles into one sharp capture.
usage: python3 tools/stitch.py out.png COLS TILE_W_CSS TILE_H_CSS PAGE_W_CSS PAGE_H_CSS tile_r0c0.png tile_r0c1.png tile_r1c0.png ...
Tiles are row-major, each showing TILE_W_CSS x TILE_H_CSS CSS px of the page; the output covers PAGE_W_CSS x PAGE_H_CSS CSS px."""
import sys
from PIL import Image
out, cols, tw, th, pw, ph = sys.argv[1], int(sys.argv[2]), *map(float, sys.argv[3:7]); files = sys.argv[7:]
first = Image.open(files[0]); S = first.width / tw; TW, TH = first.width, round(th * S)
rows = (len(files) + cols - 1) // cols
im = Image.new('RGB', (cols * TW, rows * TH), 'white')
for i, f in enumerate(files): im.paste(Image.open(f).convert('RGB').resize((TW, TH)), ((i % cols) * TW, (i // cols) * TH))
im = im.crop((0, 0, round(pw * S), round(ph * S))); im.save(out); print(out, im.size, f'{S:.3f} px per CSS px')
```

### `tools/align.py`
```python
#!/usr/bin/env python3
"""Did a re-exported video move in time? Compares the voice tracks of two files.
usage: python3 tools/align.py old.mp4 new.mp4    -> the offset; 0 frames means the existing overlay, timing and cues still fit"""
import subprocess, sys, numpy as np
pcm = lambda f: np.frombuffer(subprocess.run(['ffmpeg', '-v', 'error', '-i', f, '-vn', '-ac', '1', '-ar', '8000', '-f', 's16le', '-'], capture_output=True).stdout, np.int16).astype(float)
a, b = pcm(sys.argv[1]), pcm(sys.argv[2]); n = min(len(a), len(b), 8000 * 90); a, b = a[:n], b[:n]
c = np.fft.irfft(np.fft.rfft(b, 2 * n) * np.conj(np.fft.rfft(a, 2 * n))); k = int(np.argmax(c)); k = k - 2 * n if k > n else k
print(f'new is {k / 8000:+.3f} s ({k / 8000 * 30:+.1f} frames) relative to old; lengths {len(pcm(sys.argv[1])) / 8000:.2f} s and {len(pcm(sys.argv[2])) / 8000:.2f} s')
print('aligned: reuse the overlay and cues' if abs(k) < 80 else 'shifted: add the offset to TB, XT, every cue time and the SFX cues, then re-render')
```
