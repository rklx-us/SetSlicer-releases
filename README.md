# SetSlicer — releases

Download page and update channel for **SetSlicer**, a tool that splits a
full concert recording into one clip per song.

This repository holds **only release builds**. It carries no source code;
development happens in a private repository.

## Download

Grab the newest installer from the [Releases](../../releases) page:

- **macOS** — `SetSlicer-macOS.dmg`
- **Windows** — `SetSlicer-Windows-Setup.exe`

## Channels

| Release type | Who sees it |
| --- | --- |
| Prerelease (`v0.2.0-beta.1`, and anything `0.x`) | Users on the **beta** channel |
| Full release (`v1.0.0` and later) | Everyone |

SetSlicer checks this repository for updates from **Help ▸ Check for
updates**, and the channel is selectable there. Everything before `v1.0.0`
is a beta by definition, so early builds only appear on the beta channel.

## First run

These builds are **unsigned**, so the OS will flag them once:

- **macOS** — right-click (or Control-click) the app → **Open** → **Open**.
- **Windows** — SmartScreen shows "Windows protected your PC" → **More info** → **Run anyway**.

Neither installer bundles `ffmpeg` or `whisper-cpp`; the app offers to
install them on first launch.
