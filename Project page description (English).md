## Audion Media Tools

**Audion Media Tools** is a portable, script-first workflow toolkit built around FFmpeg, yt-dlp, and a fast launcher UI (CMD + FZF/PowerShell).

This project does **not** aim to replace MeGUI, HandBrake, other FFmpeg front-ends, or Shutter Encoder. Those tools are excellent at being general-purpose GUIs.  
**Audion Media Tools is different:** it’s a curated set of ~85 production-oriented presets and launchers designed for repeatable, high-quality results in real-world video workflows.

### Why it exists
The goal is maximum control and consistency when preparing material for:
- video production and editing timelines (unifying mixed sources into a clean, predictable format),
- fast “dailies” / review exports for clients and family,
- normalizing client-provided footage into a single delivery spec,
- remuxing and utility operations without unnecessary re-encoding,
- and generally reducing friction in a professional-grade workflow.

### Audio: the proud part
A key highlight is the audio pipeline: **high-quality resampling and extraction** with FFmpeg using the **SOXR** resampler, preserving quality and avoiding “cheap” conversions.

For best results, it is strongly recommended to use a **FULL build of FFmpeg** (not “Essentials”), so all required filters and libraries are available (SOXR, LUT filters, zscale/tonemap, and more).

### Philosophy
- **Portable by design:** keep everything inside one folder, no installer required.
- **Repeatable presets:** predictable outputs, consistent naming, minimal surprises.
- **Fast UI:** pick a preset and keep working (looping FZF menus, no constant restarts).

If you want a clean, controlled “toolbox” that behaves the same every time — this is it.