# ⚡ AceBlade Downloader

A clean, modern desktop YouTube downloader for **Linux / Ubuntu**.

Paste a link → pick Video or Audio → download. No clutter, no Python module headaches.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Ubuntu-orange)
![License](https://img.shields.io/badge/License-MIT-green)

---

## Features

- 🎬 **Video** — MP4, best quality (auto-merged with FFmpeg)
- 🎵 **Audio** — MP3 at 128 / 192 / 256 / 320 kbps
- 📋 Paste any YouTube URL (`watch`, `youtu.be`, Shorts)
- 🔍 Preview title, channel, and duration before downloading
- 📊 Live progress: percentage, speed, size, ETA
- ⏹ Cancel an active download safely
- 📁 Choose download folder · open it when done
- 🕘 Local download history
- ⚙ Settings (quality, paths, filename length)
- 🌙 Dark modern UI
- 🛠 First-launch dependency check & installer

---

## Why this exists

Many Ubuntu systems ship the **yt-dlp binary** but block `pip install yt-dlp` (PEP 668 / externally-managed-environment). Apps that do `import yt_dlp` then crash with:

```text
ModuleNotFoundError: No module named 'yt_dlp'
```

**AceBlade never imports the Python package.**  
It always calls the system `yt-dlp` executable through `subprocess`:

```python
subprocess.Popen(["yt-dlp", "--no-playlist", ...])
```

Works whether yt-dlp was installed via `apt`, `pipx`, or any other PATH method.

---

## Requirements

| Component | Notes |
|-----------|--------|
| **Python 3.8+** | Tested on 3.10 / 3.12 |
| **Tkinter** | `python3-tk` on Debian/Ubuntu |
| **yt-dlp** | System executable (`which yt-dlp`) |
| **FFmpeg** | Needed for merge & MP3 conversion |

---

## Install & Run

### 1. System packages

```bash
sudo apt update
sudo apt install -y python3 python3-tk yt-dlp ffmpeg
```

### 2. Get the app

```bash
git clone https://github.com/YOUR_USERNAME/aceblade-downloader.git
cd aceblade-downloader
```

### 3. Launch

```bash
python3 aceblade_downloader.py
```

On first launch the app checks dependencies.  
If something is missing, a setup window appears and can install packages for you (may ask for your password). Later launches go straight to the main window.

---

## Usage

1. Paste a YouTube URL (or press **Ctrl+V**)
2. Click **Fetch Info** (optional) to preview the video
3. Choose **VIDEO** or **AUDIO**
4. Pick the download folder if needed
5. Click **↓ DOWNLOAD** (or **Ctrl+Enter**)

### Keyboard shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl + V` | Paste URL |
| `Enter` | Fetch video info |
| `Ctrl + Enter` | Start download |
| `Esc` | Cancel download / close popup |

---

## Supported URLs

```
https://www.youtube.com/watch?v=VIDEO_ID
https://www.youtube.com/watch?v=VIDEO_ID&t=318s
https://youtu.be/VIDEO_ID
https://www.youtube.com/shorts/VIDEO_ID
```

Playlist parameters (`&list=...`) are ignored — only the single video is downloaded (`--no-playlist`).

---

## Project layout

```text
aceblade-downloader/
├── aceblade_downloader.py   # Entire app (single file)
├── README.md
├── data/                    # settings.json, history.json (created at runtime)
└── logs/                    # aceblade.log
```

Everything lives in **one Python file**. No pip packages required for the core app.

---

## Optional: Deno (JS runtime)

Modern yt-dlp may print:

```text
No supported JavaScript runtime could be found
```

This is **not fatal** — most videos still download.  
For maximum format availability:

```bash
curl -fsSL https://deno.land/install.sh | sh
```

AceBlade shows a non-blocking status tip when a runtime is missing.

---

## Troubleshooting

**yt-dlp not found**
```bash
sudo apt install -y yt-dlp
# or
pipx install yt-dlp
```

**FFmpeg not found**
```bash
sudo apt install -y ffmpeg
```

**Tkinter missing**
```bash
sudo apt install -y python3-tk
```

**Filename too long**  
Titles are sanitized and truncated. You can lower the limit in **Settings → Advanced**.

**PEP 668 / externally-managed-environment**  
Do **not** rely on `pip install --user yt-dlp`. Use the system package or `pipx`. AceBlade does not need the Python module.

---

## License

MIT — free to use, modify, and share.

---

<p align="center">
  <b>⚡ AceBlade Downloader</b><br>
  Fast · Simple · Reliable
</p>
