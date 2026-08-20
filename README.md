# SetSlicer

**Split a full concert or show recording into one clip per song.**

You point SetSlicer at a single long recording — a two-hour FOH capture,
say — and it helps you find where each song starts and ends, name them,
and cut them into separate files with a README listing every timestamp.

This repository is the **download page and update channel**. It holds no
source code; development happens in a private repository.

### [⬇ Download the latest build](../../releases)

*(GitHub's "latest release" link only ever points at a full release, and everything before `v1.0.0` is a beta - so until then this goes to the releases list, newest first.)*

| | |
| --- | --- |
| **macOS** | `SetSlicer-macOS.dmg` |
| **Windows** | `SetSlicer-Windows-Setup.exe` |

---

## First run

These builds are **unsigned** — there is no Apple Developer ID and no
Windows code-signing certificate — so your OS will warn you once:

- **macOS** — Gatekeeper refuses to open it normally. Right-click (or
  Control-click) the app → **Open** → **Open** in the dialog. Once only.
- **Windows** — SmartScreen shows *"Windows protected your PC"*. Click
  **More info** → **Run anyway**.

### It will ask to install two tools

SetSlicer needs `ffmpeg` (video cutting, waveforms) and `whisper-cpp`
(offline speech-to-text). They're too large to bundle, so on first launch
the app checks for them and offers to install:

- **macOS** — an **Install with Homebrew** button. Needs [Homebrew](https://brew.sh).
- **Windows** — an **Install missing dependencies** button. `ffmpeg` comes
  from winget; `whisper-cli` is downloaded straight from the official
  whisper.cpp releases into the app's own folder. No PATH changes, no
  manual downloads.

Everything runs **on your machine**. Your recording is never uploaded.

---

## How you'd actually use it

1. **New project** — pick your video file and where clips should go.
2. **Detect candidate boundaries** — a first pass using silence detection.
   It's a starting point, not an answer: it will split banter into fake
   songs and miss quiet intros.
3. **Fix the boundaries.** Drag segments on the waveform, drag their edges
   to trim (the playhead follows the edge, so you see the exact frame
   you're landing on), or shift-drag empty waveform to draw a new segment.
   `Ctrl+Z` undoes anything.
4. **Name them.** Press `N` to jump to the next untitled segment and hit
   `Enter` to file a name and move to the next one.
5. **Export** — cuts every clip and writes a README with all timestamps.
   Only clips whose boundaries actually changed get re-encoded.

### Optional: AI Assist

If you paste in your own [Anthropic API key](https://console.anthropic.com),
SetSlicer can look up the real setlist for the show, compare it against
your segments, flag a long segment hiding two songs, and propose titles.
It transcribes short ranges locally to check itself.

This is **bring-your-own-key** — requests go from your machine to
Anthropic on your account, and calls cost real money (the app shows an
estimate before starting). It's entirely optional; the app works fully
without it.

---

## Updates

**Help ▸ Check for updates** inside the app, on one of two channels:

| Channel | What you get |
| --- | --- |
| **Stable** | Full releases only. Beta builds are never offered. |
| **Beta** | Every build, including prereleases — new features first, less tested. |

Everything before `v1.0.0` publishes as a prerelease, so **right now all
builds are beta-channel only.** A beta build defaults to the beta channel
so it keeps seeing newer betas.

The app only *checks* and downloads — you run the installer yourself.

---

## Known limitations

- Song identification is a judgement call, not something this fully
  automates. It surfaces the evidence — transcript, spectrogram, timecode
  math, setlist — so you can decide quickly.
- The `copy` export preset is fastest but only frame-accurate if your cut
  points land on keyframes. If a clip's first second looks off, switch the
  project to `h264`/`h265` and re-export.
- Silence detection cannot tell banter from a song. Expect to fix its
  first pass by hand.

## Reporting a problem

Open an [issue](../../issues) with your OS, the version from
**Help ▸ About SetSlicer**, and what you were doing.
