---
name: no-slop-motion
description: >-
  Make a launch film, brand film, product announcement or promo video for a company that looks directed, not AI-generated. Use when someone asks for a launch video, brand video, sizzle, promo, product film or "a video for our brand/X/LinkedIn launch", or when an AI-made video "feels vibe coded", "looks like a slideshow", or keeps getting rejected. Covers the whole path: customer pain research, script, voiceover, world and style frames, optional mascot or hero object, animatic, HTML motion build (HyperFrames + GSAP), music, sound, QA and platform export.
---

# No-slop motion

A process for making a brand or launch film with an agent that people actually want to watch.

**The core idea: the agent's defaults are the slop.** When an agent picks something on its own (a track, a transition, a shadow, a font, a place to cut the voice), the result looks like every other AI video. What makes a film feel directed is that every choice comes from something real: the customer's own pain, the brand's own assets, the structure of the music, the narrator's breathing, or a named reference. So this skill is mostly about *where each decision comes from*, and the tooling is there to enforce it.

## What makes a film work

1. **Knowing the customer.** Who buys (the ICP), what hurts them in their own words, and the one thing only this product does (the USP). The film sells one before and after, not a feature list.
2. **One story thread.** Effect, then cause, then fix. For an invoicing tool: "why is the bank balance empty again?" → rewind → one invoice sat unsent for three weeks → the product arrives → it sends that invoice the moment work is done → what else you get → the balance fills up. A small mystery pulls people through a film. A feature tour doesn't.
3. **A world with its own rules.** A visual concept that comes from the story's feeling (for example a flickering 1970s office of paper forms and rubber stamps for the problem half, then clean brand colour when the product arrives). Every texture, colour and transition then has a reason.
4. **Brand motifs used freely.** Three to five things only this brand owns (a mascot, the logo mark, a signature button, a success animation, a sound). No mascot is fine: see [references/05-hero.md](references/05-hero.md).
5. **The voice sets the clock.** The narration is recorded first, in one continuous take per act. Picture is timed to the voice. Music comes last and is edited so it still sounds like one performance.
6. **Gates, not versions.** Each layer is locked before the next one is built, and each lock uses whatever the decision maker (the person who approves the film) can judge fastest: a page of text, five still frames, a rough animatic. Building story, style, voice and motion all at once is the slowest way to get there.

## Before you start

Check the tools in the first five minutes, not on day two:

| Need | Default | Notes |
| --- | --- | --- |
| Motion and render | [HyperFrames](https://hyperframes.heygen.com) (HTML + GSAP to MP4) | `npx hyperframes skills` installs its agent skills. Read `/hyperframes-core` before writing composition HTML. |
| Voice | [Cartesia](https://cartesia.ai) Sonic (`scripts/audio/tts-cartesia.ts`) | ElevenLabs works too. The key goes in an env var. Record a scratch voice in the first pass. |
| Music | [Suno](https://suno.com) or a licensed track | Once a track is liked, ask for continuations of it, not a fresh batch. |
| Transcription | faster-whisper or `npx hyperframes transcribe` | Word timestamps feed captions and voice splitting. |
| Audio and video tools | ffmpeg, Python 3 with numpy, librosa, soundfile | `pip install -r scripts/audio/requirements.txt` |
| Real UI | Access to the live product, marketing site and brand files | UI gets rebuilt as HTML from the product's real CSS and copy. |

Start the project from [starter/](starter/): a HyperFrames project with a film engine (one timeline, a timing table, actors, cameras, captions, sound cues). Copy it, then read `starter/README.md`.

## The gates

Work through them in order. A gate opens only when the decision maker has signed off the lock before it. Details and checklists are in the reference for each gate.

| Gate | What you make | Lock | Reference |
| --- | --- | --- | --- |
| 0. Inputs | Input pack: brand truth from production, product surfaces, claims list, platform and length, 2 to 4 references with what to take from each | Pack exists, `LOVES-HATES.md` started | [01-inputs.md](references/01-inputs.md) |
| 1. Pain and positioning | Pain bank from real customer words, one villain, 2 or 3 felt numbers, one-page brief | Brief approved | [02-story.md](references/02-story.md) |
| 2. Script | The film as spoken paragraphs per act | Words approved when read aloud | [02-story.md](references/02-story.md) |
| 3. Voice | Cast, record one take per act in 2 or 3 readings, score, split in silences | VO timeline. From here the voice sets the clock | [03-voice.md](references/03-voice.md) |
| 4. World and style frames | 2 or 3 world concepts, then 5 still frames for the chosen one, plus `DESIGN.md` with a banned list | Approved contact sheet | [04-world.md](references/04-world.md) |
| 5. Hero (parallel lane) | Mascot rig or hero object, with an expression or state sheet | Rig and sheet approved | [05-hero.md](references/05-hero.md) |
| 6. Animatic | Every shot blocked on the VO timeline with temp music, a named transition for every cut | Story and timing frozen | [06-motion.md](references/06-motion.md), [07-build.md](references/07-build.md) |
| 7. Build | Scenes split into files, built by parallel agents, linted and reviewed | Picture lock | [07-build.md](references/07-build.md) |
| 8. Sound | Cue sheet, music edited on downbeats, few SFX tuned to the key, mix | One full listen with no audible splice | [08-sound.md](references/08-sound.md) |
| 9. Final gauntlet | Independent review of every frame, sound on and muted, exports | Ship | [09-qa-render.md](references/09-qa-render.md) |

Fill the templates in [templates/](templates/) as you go: `BRIEF.md`, `PAIN-BANK.md`, `SCRIPT.md`, `DESIGN.md`, `SHOTLIST.md`, `CUE-SHEET.md`, `LOVES-HATES.md`.

**Do not skip ahead to motion.** The common failure is a beautiful animatic of the wrong story. Story and visual style are the two layers that take the most rounds, and they take far more when they are attempted at the same time as everything else.

## Standing rules

These apply at every gate.

- **Keep a loves and hates file.** After every message from the decision maker, add what they loved and what they hated to `LOVES-HATES.md`, in their words, with the fix. Re-read it before every render. Without it, the same complaints come back round after round.
- **Ground every choice.** Before building anything, ask where it came from. Customer words, the live brand, the music's structure, the narrator's take, or a named reference are all fine. "It looked good to me" is not. When something looks invented, replace it with something real.
- **Claims come from the whitelist.** A launch film is a public claim. Every spoken or written line must match the marketing site or an approved claims list. Watch for lines that promise more autonomy or speed than the product has.
- **When the feedback is "too much", cut the number of elements, not the life.** Corrections tend to overshoot: "too busy" easily turns into "too minimal and dry" in one round. Keep the texture, colour and motion. Remove things.
- **Batch follow-ups.** Notes arrive mid-render. Fold them all into one pass, and say which layer each one touches.
- **Don't touch a locked layer without saying so.** If a picture change needs a new voice line, or a music edit needs a picture retime, say it before doing it.
- **Review before handover.** Before showing any cut, have an independent subagent review it adversarially against `LOVES-HATES.md` and the banned list, and run the QA scripts. The decision maker should never be the first to find a pop, a mistimed caption or a cursor that misses.
- **Use subagents in parallel for the build**, one owner per scene file (see [07-build.md](references/07-build.md)).

## Banned by default

These are the fingerprints of AI motion slop. They go in `DESIGN.md`, and `scripts/qa/lint-slop.ts` checks for them. Remove one only if the decision maker asks for it.

- Hard offset shadows and drop shadows on containers. Depth belongs only to buttons.
- Radial gradients, glows, vignettes, coloured world backgrounds, checkerboard floors, corner labels.
- Card grids and icon lists standing in for an explanation.
- Static UI screens with no camera move, build or morph (a slide).
- Text parked at the top of the frame while something else happens below.
- Hard pops: anything that appears, vanishes or flashes in one or two frames. Black dips between shots.
- Shader transitions that drop colour on capture, glitch transitions picked for "energy".
- Linear moves. Overshoot (`back.out`, `elastic`) on UI; keep squash and stretch for a character.
- CSS filters (`grayscale`, `sepia`, `saturate`) to fake a colour world. Author the colours.
- Customer quotes as tweet or Slack cards. Research feeds the film; it doesn't go on screen.
- More than one brand-coloured call to action in a frame.
- A sound on every landing.
- Stitched one-line TTS clips. Voice cut in the middle of a word or a sentence.

## Scripts

All scripts print their usage with `--help`.

| Script | What it does |
| --- | --- |
| `scripts/audio/tts-cartesia.ts` | Record each act as several continuous takes with different emotion settings |
| `scripts/audio/score_takes.py` | Rank takes by word accuracy, emotional range, pitch range and pace, as a shortlist to listen to |
| `scripts/audio/split_takes.py` | Split the winning take into line pieces only in real silences, then re-transcribe each piece |
| `scripts/music/join_on_downbeats.py` | Join or shorten music takes on matching downbeats with one-beat crossfades, without stretching |
| `scripts/music/cue_sheet.py` | Check every must-hit against the music's beats and flag misses over 0.1 s |
| `scripts/qa/lint-slop.ts` | Grep the project for banned patterns (configurable from your loves and hates) |
| `scripts/qa/pop-scan.py` | Find pops, flashes and black dips in a render that aren't on a planned cut |
| `scripts/qa/contact_sheet.py` | Tile frames every N seconds, or densely around cuts, for review |
| `scripts/render/render.ts` | Render picture, mix voice, music and SFX, normalise loudness, and remix audio onto a locked picture |
| `scripts/export/social.ts` | Platform exports (X under 512 MB, 4:5, 9:16) at -14 LUFS |

## Handing over a cut

Hand over a review page or a Studio link, not only a file: the video, a frame grid, and a short list of what changed against the last notes. Keep the message short:

1. What changed, one line per note, in the decision maker's words.
2. What you want them to judge this round (for example "only the style frames, not the timing").
3. Anything you could not do, and why.

Time a full render in the first pass and plan review loops around it. Long renders near a deadline are the most common way to run out of time (see [09-qa-render.md](references/09-qa-render.md) for how to make renders fast).
