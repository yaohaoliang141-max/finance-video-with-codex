---
name: subtitle-synced-finance-video
description: Create or revise Chinese financial explainer videos from user-supplied footage, scripts, subtitles, or narration using HyperFrames. Use when the user invokes this skill or asks for the established dark financial-documentary video style with subtitle-triggered MG animation, full-screen translucent charts, frequent kinetic text, varied layouts, a bottom chapter progress bar, and 2–3 second chapter title cards. Enforce exact subtitle timing and semantic relevance: MG must never appear before the subtitle phrase it explains.
---

# Subtitle-Synced Finance Video

Build the complete video through the installed `hyperframes:hyperframes` and `hyperframes:hyperframes-cli` skills. Read both skills before authoring or rendering. Use GSAP guidance when writing animation. Preserve supplied footage, narration, and burned-in subtitles unless the user explicitly requests changes.

Read [references/production-rules.md](references/production-rules.md) before planning the timeline. When chapter styling is needed, inspect the bundled reference images in `assets/`.

## Required workflow

1. Inspect the source video with `ffprobe`; confirm duration, resolution, frame rate, audio, and subtitle situation.
2. Obtain precise subtitle start and end times before scheduling MG:
   - Prefer supplied SRT/VTT/transcript timestamps.
   - Otherwise transcribe the actual source audio with Chinese-capable Whisper.
   - When subtitles are burned in and transcription is unavailable, detect or OCR their change points from the subtitle region.
   - Never substitute uniform intervals, broad topic estimates, or guessed timings.
3. Read the complete transcript and divide it into meaningful chapters. Choose concise chapter names derived from the actual narration.
4. Create or update `DESIGN.md` before editing composition HTML. Preserve the approved dark financial-documentary identity while varying layout and palette emphasis.
5. Build the unchanged source video on track 0 and its audio on a separate track. Add MG, chapter cards, and navigation on higher visual tracks.
6. Map every MG clip to an exact subtitle phrase in a timing table before authoring. Record: subtitle text, subtitle start/end, MG concept, MG start/end, and layout type.
7. Author subtitle-specific MG, a persistent chapter navigation bar, and 2–3 second chapter openers.
8. Run the full HyperFrames check, inspect dense timestamps, render, then extract review frames at every chapter opener and representative MG moments.
9. Verify output duration, video dimensions, frame rate, audio track, subtitle visibility, timing, and semantic matches before delivery.

## Hard timing gate

- Set `MG start >= matching subtitle start`. Never allow an MG to foreshadow its subtitle.
- Prefer `MG start = subtitle start` or 0.05–0.20 seconds later.
- An MG may remain slightly after the matching subtitle ends for readability, but must not conflict with the next subtitle.
- If the subtitle displays a concrete value such as `10000元`, trigger the matching value animation only after `10000元` is visible.
- When subtitle meaning changes, change or clear the MG promptly.
- Reject any MG that is merely related to the overall topic but not to the exact simultaneous subtitle.

## Motion behavior

- Make exits visually reverse their entrances: slide back toward origin, scale back down, retract lines, and collapse bars to their baseline.
- Do not use abrupt full-screen wipes, flashes, hard cuts, or unrelated transition covers to remove MG.
- Keep entrances energetic and exits shorter, smooth, and readable.
- This mirrored-exit requirement overrides a generic HyperFrames transition rule when the two conflict.

## Visual system

- Use dark graphite/black-gray financial-documentary styling with warm white text and controlled orange accents.
- Keep charts translucent so source footage remains visible.
- Vary placement, color emphasis, scale, and composition. Rotate among left, right, centered, split-screen, edge-anchored, full-screen, and asymmetric layouts.
- Avoid repeated recolors of one template. Select the visual form from the exact subtitle meaning.
- Preserve the burned-in subtitle safe area.

## Chapter system

- Keep a bottom chapter progress/navigation bar visible through the main content, without covering subtitles.
- Show all chapter labels, clearly mark the active chapter, and animate progress deterministically.
- Before each chapter, insert a 2–3 second editorial documentary title card with chapter number and prominent Chinese chapter name. An optional short English subtitle is allowed.
- Use textured archival financial imagery, restrained monochrome treatment, and strong editorial typography inspired by the bundled chapter reference.
- Enter and leave chapter cards with mirrored motion, not abrupt transition covers.

## Delivery

Render final MP4 files into the workspace `outputs/` directory with a descriptive Chinese filename. Link the final file and briefly report chapter count, MG count, duration, resolution, frame rate, and verification status.
