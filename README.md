```md
# Audion Media Tools v1.0

Portable Windows media toolkit: preset scripts + launchers for **FFmpeg**, **yt-dlp**, and a fast **FZF UI** (PowerShell 7).  
Designed for repeatable, high-quality results in real-world video workflows.

✅ This release is **scripts-only** (no third-party binaries are bundled).  
You install tools by downloading official builds and placing them into `Tools\...`.

---

## Audion Media Tools (Project Overview)

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

---

## Project layout

Root folders:

```

Docs
Download
LUTs
Scripts
Source
Tools
Transcoded\

```

Where:
- `Source\` — drop input media here
- `Transcoded\` — output files
- `Download\` — YouTube output + helper files (URLs.txt, etc.)
- `LUTs\` — LUTs for grading presets
- `Scripts\` — preset `.cmd` scripts called by launchers
- `Tools\` — third-party binaries (downloaded by you)

---

## Tools layout (important)

Your `Tools\` folder contains:

```

Tools
7zip
download
ffmpeg
fzf
Launchers
MediaDownloader
PowerShell
yt-dlp
env.cmd
Run-PowerShell.cmd

```

FZF scripts:

```

Tools\Launchers\fzf
fzf-main.ps1
launcher-youtube.fzf.ps1
launcher-resample.fzf.ps1
launcher-remux.fzf.ps1
launcher-lut-grading.fzf.ps1
launcher-prores-dnxhr.fzf.ps1
launcher-x264-hevc.fzf.ps1
launcher-fps.fzf.ps1
launcher-tools-update.fzf.ps1

```

PowerShell portable is unpacked directly into:
- `Tools\PowerShell\` (NOT `bin\`)

So the important file is:
- `Tools\PowerShell\pwsh.exe`

---

## Quick Start

1) Unpack the release into any folder (portable).
2) Run:

```

run-init-dir.cmd

```

3) Download tools (below) and place them into their folders.
4) Start:
- CMD UI: `launcher-main.cmd`
- FZF UI: `fzf-launcher-main.cmd`

---

## Install tools (manual)

You can use any archiver already installed (7-Zip / WinRAR / PeaZip).

### 1) FFmpeg
Put into:
- `Tools\ffmpeg\bin\`

Required:
- `ffmpeg.exe`
- `ffprobe.exe`

**Recommendation:** use a **FULL build** of FFmpeg (not “Essentials”).

### 2) fzf
Put into:
- `Tools\fzf\bin\fzf.exe`

### 3) yt-dlp
Put into:
- `Tools\yt-dlp\bin\yt-dlp.exe`

### 4) PowerShell 7 (portable, recommended)
Unpack the PowerShell zip into:
- `Tools\PowerShell\`

So you have:
- `Tools\PowerShell\pwsh.exe`

`Tools\Run-PowerShell.cmd` will automatically prefer this portable PowerShell.

### 5) MediaDownloader (optional)
Put into:
- `Tools\MediaDownloader\bin\media-downloader.exe`

### 6) 7-Zip (optional)
Not required for normal operation.
If you want it:
- `Tools\7zip\bin\7za.exe` or `7zr.exe`

---

## Built-in tool download helpers (download-only)

- `launcher-tools-update.cmd` — downloads tool archives/exes into `Tools\download\` (download-only)
- `launcher-media-downloader-update.cmd` — downloads MediaDownloader Qt6 zip (download-only)

Then you manually unpack/move binaries into `Tools\...\bin\` (and PowerShell into `Tools\PowerShell\`).

---

## Launchers

### CMD UI
Start:
- `launcher-main.cmd`

Direct category launchers:
- `launcher-youtube.cmd`
- `launcher-resample.cmd`
- `launcher-remux.cmd`
- `launcher-lut-grading.cmd`
- `launcher-prores-dnxhr.cmd`
- `launcher-x264-hevc.cmd`
- `launcher-fps.cmd`
- `launcher-select-fps-speed.cmd`

### FZF UI
Start:
- `fzf-launcher-main.cmd`

Internals:
- `Tools\Run-PowerShell.cmd` runs `Tools\Launchers\fzf\fzf-main.ps1`
- each submenu is `launcher-*.fzf.ps1`

---

## Optional: clear screen before each FZF menu

By default, logs stay visible (recommended).

If you want clean screen before each menu:

```

set AUDION_FZF_CLEAR=1
fzf-launcher-main.cmd

```

Disable:

```

set AUDION_FZF_CLEAR=

```

---

## Typical workflow

1) Drop files into:
- `Source\`

2) Run CMD or FZF UI
3) Choose a preset
4) Outputs appear in:
- `Transcoded\` (and subfolders like `Transcoded\Audio\`)

---

## Which preset should I choose?

### YouTube / Web downloads
- **Best quality, no loss:** use **Extract audio COPY (no re-encode)**  
  (keeps OPUS/M4A exactly as delivered)
- **Need editing-friendly audio:** extract/resample to **WAV 48k PCM 24-bit** (or **32-bit float**)
- **Need compatibility / small file:** export to **M4A AAC 256k / 384k**
- **Need loudness for publish:** normalize to **-14 LUFS** (typical web loudness)

### Editing / timeline (NLE)
- Prefer **WAV 48k PCM 24-bit** (or **32-bit float**) + sync variant if available.
- For video intermediates:
  - **ProRes / DNxHR** presets for smooth playback / editing.

### Archive / storage
- **FLAC** presets (lossless, smaller than WAV).
- Keep original streams using **COPY** when possible.

### Quick container fixes (no re-encode)
- Use **Remux** presets (MP4 ↔ MKV, MOV ↔ MXF) when you only need a container swap.

### FPS conversion (23.976 workflows)
- **VARISPEED**: changes speed & pitch (film-style)
- **CONFORM**: keeps pitch using audio time-stretch (when available)

---

## Troubleshooting

### FZF does not start
Check:
- `Tools\fzf\bin\fzf.exe`
- `Tools\PowerShell\pwsh.exe`

Run:
- `fzf-launcher-main.cmd`

### ffmpeg / ffprobe not found
Check:
- `Tools\ffmpeg\bin\ffmpeg.exe`
- `Tools\ffmpeg\bin\ffprobe.exe`

### yt-dlp not found
Check:
- `Tools\yt-dlp\bin\yt-dlp.exe`

### Script opens and immediately closes
Run the script from a terminal (CMD/PowerShell) to see the error text.

### Weird characters / broken emoji
Use Windows Terminal + PowerShell 7 (portable recommended):
- `Tools\PowerShell\pwsh.exe`

### Files with spaces / parentheses fail
Most scripts are robust, but if a specific preset breaks on special filenames:
- rename the file temporarily, or
- report the preset name and the filename pattern that failed.

### Want clean screen before every FZF menu
Enable:
```

set AUDION_FZF_CLEAR=1

```
Disable:
```

set AUDION_FZF_CLEAR=

```

---

## License

**MIT** for this project (scripts, launchers, docs).

Third-party tools are **NOT included** and are governed by their own licenses:
FFmpeg, yt-dlp, fzf, PowerShell, MediaDownloader, 7-Zip, etc.
```
