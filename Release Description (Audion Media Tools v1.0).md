# Audion Media Tools v1.0

Portable Windows media toolkit: **FFmpeg presets + YouTube (yt-dlp) + Remux + Audio (SOXR/LUFS) + FZF UI (PowerShell 7)**.

This release is a **scripts-only bundle** (no third-party binaries included).  
Use the README to download and place: **FFmpeg / fzf / 7-Zip / yt-dlp / PowerShell / MediaDownloader** into `Tools\...`.

## Start
- Create folders: `run-init-dir.cmd`
- CMD UI: `launcher-main.cmd`
- FZF UI: `fzf-launcher-main.cmd`

## FZF system (PowerShell)
FZF launchers live here:
`Tools\Launchers\fzf\`

Main entry:
- `Tools\Launchers\fzf\fzf-main.ps1`

Runner:
- `Tools\Run-PowerShell.cmd` (prefers `Tools\PowerShell\pwsh.exe`)

## Notes
- Third-party tools are **not included** and have their own licenses.
- Project scripts/docs are MIT-licensed.