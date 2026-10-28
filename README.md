# systemsluke motion graphics

A Claude skill that turns a vertical talking-head video (Instagram Reels first, also TikTok and YouTube Shorts) into a finished short: motion graphics timed to the spoken words, real-world material cut in where it helps, quiet sound effects, and upload-ready files.

There is no house style. On the first run the skill gathers the person's references and taste, builds their own design system from them, and saves it as their own editing skill. Every later video starts from that style.

## How it works

1. **References.** The person shares two to five things they love, one to three they dislike, and any brand assets.
2. **Interview.** Up to five short rounds cover feel, typography and colour, what appears on screen, animation likes and dislikes, sound, and delivery files.
3. **Design system.** Their answers become colour, type, layout, components, texture, motion and sound tokens, plus a Never list. It is shown on one board and tested on 10 seconds of their own footage, as an A/B comparison.
4. **Their editing skill.** The design system is saved as `<name>-editing-style`, so later videos skip setup.
5. **Every video.** Transcribe with word timings → research what they name → storyboard and edit log (every word and the graphic that lands on it) → build → check stills and safe areas → render, add sound, composite → deliver.
6. **Editor notes.** Short notes ("this text is too small", "that sound is too loud") are fixed in place. Notes that should apply to every video become standing rules in their editing skill.

## Under the hood

Every frame is drawn by an HTML page as a pure function of time (`window.seek(t)`) and rendered in headless Chromium through Playwright. Python tools handle transcription (sherpa-onnx with Whisper and Parakeet), person mattes for graphics that sit behind the head, camera punch-ins, sound effects and final encoding with ffmpeg.

The whole engine (`index.html`, `core.js`, `timeline.js`, `render.js`, `sfx.py`, `comp.py`, `tools/*`, and the rest) is embedded in section 10 of the skill and written out into a project folder for each video. Per person, only `style.js`, `components.js` and `board.js` change. Per video, `video.js`, `camera.json`, `occlude.json`, `edit_log.json` and the sound cues change.

## Deliverables

- `<Name>_with_animations_4K.mp4`: the upload file
- `<Name>_with_animations.mp4`: a 1080p copy under 30 MiB
- `<Name>_overlay_ProRes4444_alpha_IN-00-00-00-00.mov`: graphics only, transparent
- `<Name>_SFX_stem_IN-00-00-00-00.wav`: sound effects only
- `<Name>_framing.txt`: punch-in, behind-the-head and full-screen ranges for matching in an editor

## Requirements

- Node.js with Playwright and Chromium
- Python 3 with `sherpa-onnx`, `opencv-python-headless`, `scipy`, `rembg` and `onnxruntime`
- ffmpeg and ffprobe

The skill installs the npm and pip packages and downloads the speech models when it sets up each project folder.

## Repository layout

```
.claude/skills/systemsluke-motion-graphics/SKILL.md   the skill
README.md                                             this overview
```

## Using it

**Claude Code:** the skill lives in this repo's `.claude/skills/`, so it is available in any session started here. To use it in every project, copy the folder to `~/.claude/skills/`.

**claude.ai:** zip the `systemsluke-motion-graphics` folder and upload it as a custom skill.

Then send a talking-head video, or ask for a new editing style.
