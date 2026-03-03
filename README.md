# Audion Media Tools v1.0

A portable **Windows** media toolkit: curated **FFmpeg** presets + launchers (CMD + **FZF UI** via PowerShell 7) for repeatable, high‑quality workflows.

✅ **Scripts-only** release (no third‑party binaries included).  
You download official builds (FFmpeg / fzf / yt-dlp / PowerShell / MediaDownloader / 7‑Zip) and place them into `Tools\...`.

---

## What this project is (and is not)

This project **does not** try to replace **Shutter Encoder**, **HandBrake**, **MeGUI**, or other FFmpeg front‑ends.  
Those are great general-purpose GUIs.

**Audion Media Tools** is a *workflow toolbox*: ~85 production‑oriented presets + many independent launchers to keep results consistent for:
- preparing footage for an editing timeline (unifying mixed sources),
- fast review exports (“dailies”) for clients / family,
- cleaning up and normalizing client-provided materials,
- remux utilities without unnecessary re‑encoding,
- audio extraction / resampling / loudness normalization.

### Special pride: audio
Audio presets focus on **quality-first** extraction and resampling using **SOXR** (via FFmpeg).  
For best results, use a **FULL** FFmpeg build (not “Essentials”), so all filters/libs are available.

---

## Project layout

Root folders:

```text
Docs\
Download\
LUTs\
Scripts\
Source\
Tools\
Transcoded\
```

Where:
- `Source\` — drop input media here
- `Transcoded\` — output files (audio usually under `Transcoded\Audio\`)
- `Download\` — YouTube output + helper files (URLs.txt, etc.)
- `LUTs\` — LUTs for grading presets
- `Scripts\` — preset `.cmd` scripts called by launchers
- `Tools\` — third‑party binaries (downloaded by you)

---

## Tools layout (important)

Expected `Tools\` structure:

```text
Tools\
  7zip\
  download\
  ffmpeg\
  fzf\
  Launchers\
  MediaDownloader\
  PowerShell\
  yt-dlp\
  env.cmd
  Run-PowerShell.cmd
```

FZF scripts:

```text
Tools\Launchers\fzf\
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

PowerShell portable must exist as:
- `Tools\PowerShell\pwsh.exe`

---

## Quick Start

1) Unpack the release into any folder (portable).

2) (Optional) Repair folder skeleton  
`run-init-dir.cmd` is a **repair tool**: it recreates the default folder layout if folders were deleted/damaged.  
Most users do **not** need it after unpacking the release.

3) **First-time tools bootstrap (no system PowerShell)**  
On some systems, using system PowerShell is restricted.  
Because FZF launchers require PowerShell 7, do the first download via CMD:

- Run: `launcher-tools-update.cmd`
- Download at minimum:
  - **PowerShell 7 portable ZIP**
  - **fzf ZIP**
  - **FFmpeg FULL** build (recommended)

Then unpack:
- PowerShell ZIP → `Tools\PowerShell\`  (so `Tools\PowerShell\pwsh.exe` exists)
- fzf ZIP → `Tools\fzf\bin\fzf.exe`
- FFmpeg → `Tools\ffmpeg\bin\ffmpeg.exe` + `ffprobe.exe`

4) Start:
- CMD UI: `launcher-main.cmd`
- FZF UI: `fzf-launcher-main.cmd`

---

## Official tool sources (upstream)

- PowerShell (portable ZIP): https://github.com/PowerShell/PowerShell/releases
- fzf: https://github.com/junegunn/fzf/releases
- yt-dlp: https://github.com/yt-dlp/yt-dlp/releases
- MediaDownloader: https://github.com/mhogomchungu/media-downloader/releases

FFmpeg builds:
- Gyan.dev (Windows builds): https://www.gyan.dev/ffmpeg/builds/
- BtbN builds: https://github.com/BtbN/FFmpeg-Builds/releases

7‑Zip:
- https://www.7-zip.org/

---

## Updating tools (recommended workflow)

### First run (bootstrap)
- Use **CMD**: `launcher-tools-update.cmd` (download-only into `Tools\download\`)

### After PowerShell is installed
- Use **FZF** tools updater:
  - `Tools\Launchers\fzf\launcher-tools-update.fzf.ps1`

### yt-dlp updates (frequent)
yt-dlp updates often. Update from the YouTube launcher:
- `yt-dlp -U`

---

## Launchers

### Main
- `launcher-main.cmd` — CMD main menu
- `fzf-launcher-main.cmd` — FZF main menu

### CMD category launchers
- `launcher-youtube.cmd`
- `launcher-resample.cmd`
- `launcher-remux.cmd`
- `launcher-lut-grading.cmd`
- `launcher-prores-dnxhr.cmd`
- `launcher-x264-hevc.cmd`
- `launcher-fps.cmd`
- `launcher-select-fps-speed.cmd`

Utilities:
- `run-ff-selftest.cmd`
- `run-mediadownloader.cmd`
- `Unblock All Files DIR No Pause.cmd`

---

## Which preset should I choose?

### YouTube / Web
- Best quality: **Extract audio COPY (no re‑encode)** (keeps OPUS/M4A as-is)
- For editing: **WAV 48k PCM 24‑bit** (or **32‑bit float**) (+ sync if available)
- For compatibility: **M4A AAC 256k / 384k**
- For publish loudness: **-14 LUFS** (typical web)

### Editing / timeline (NLE)
- Prefer **WAV 48k PCM 24‑bit / 32‑bit float**
- Use **ProRes / DNxHR** intermediates for smooth editing

### Archive
- **FLAC** presets (lossless, smaller than WAV)
- Or keep originals using **COPY** where possible

### Container fixes (no re‑encode)
- **Remux** presets (MP4 ↔ MKV, MOV ↔ MXF)

---

## Optional: clear screen before each FZF menu

By default, logs stay visible (recommended).  
To clear the screen before each FZF menu:

```bat
set AUDION_FZF_CLEAR=1
fzf-launcher-main.cmd
```

Disable:

```bat
set AUDION_FZF_CLEAR=
```

---

## Troubleshooting

### FZF does not start
Check:
- `Tools\fzf\bin\fzf.exe`
- `Tools\PowerShell\pwsh.exe`

### ffmpeg / ffprobe not found
Check:
- `Tools\ffmpeg\bin\ffmpeg.exe`
- `Tools\ffmpeg\bin\ffprobe.exe`

### yt-dlp not found
Check:
- `Tools\yt-dlp\bin\yt-dlp.exe`

### Weird characters / broken emoji
Use Windows Terminal + PowerShell 7 (portable recommended).

---

## License

**MIT** for this project (scripts, launchers, docs).  
Third‑party tools are **not included** and are governed by their own licenses.
