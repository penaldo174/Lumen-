# Lumen

Gallery app for Android (Kotlin + Jetpack Compose).
Ente-Photos-style photo library, Disney+-style video tab, full-featured video player.

## Open it in Android Studio
1. **File > Open** and choose this `Lumen` folder.
2. Let Gradle sync (needs internet the first time). If Studio offers to upgrade AGP / Kotlin / library
   versions, accept. The versions here are pinned to a known-compatible set.
3. Run on a phone or emulator running **Android 10 (API 29) or newer**. Grant photo/video access on first launch.

Requirements: Android Studio with JDK 17, Android SDK 35.

## What's inside
| Area | Where | Notes |
|---|---|---|
| Photos tab | `ui/photos` | Date-grouped grid (Today / Yesterday / …), video duration badges |
| Albums | `ui/albums` | Folder-based albums + album detail |
| Photo viewer | `ui/viewer` | Swipe, pinch / double-tap zoom, EXIF info sheet, share, delete |
| Videos tab | `ui/videos` | Hero banner, Continue watching, Recently added, Movies, Quick clips, per-folder rows |
| Player | `ui/player` | See below |
| Settings > Appearance > Theme | `ui/settings` | Hex codes for logo colour and playback-timeline colour (live preview, presets, reset) |
| Data | `data/` | MediaStore reader, EXIF reader, DataStore theme store, resume positions |

### Player
- ExoPlayer (Media3): MP4, MKV/WebM, MPEG-TS, FLV, Ogg, AVI and more. Video decoding uses the phone's hardware
  decoders. Audio falls back to bundled FFmpeg decoders (AC-3, E-AC-3, DTS, TrueHD, Opus, Vorbis, FLAC, ALAC…).
- English audio is selected automatically when the file has an English track; any other track is one tap away.
- Subtitles: embedded tracks, plus **Add subtitle file…** for third-party `.srt`, `.vtt`, `.ass/.ssa`, `.ttml`
  (non-UTF-8 files are converted automatically).
- Speed 1× to 2× (slider in 0.05 steps + presets).
- −10 s, −5 s, +5 s, +10 s buttons; double-tap left/right half of the screen for ±10 s.
- Resumes where you stopped; seek bar uses your chosen timeline colour.

## Known limits / next steps
- **Launcher icon colour** can't be changed with an arbitrary hex at runtime (Android only allows switching between
  pre-declared icons). The hex setting changes the logo shown inside the app.
- No software *video* decoder: a codec the phone's hardware can't decode (e.g. HEVC/AV1 on older phones) shows an
  error screen.
- Not yet included: in-app OpenStreetMap map, search, backup/sync, RAW editing. RAW files are listed and shown using
  the system preview.

## If the build complains
- `media3-ffmpeg-decoder` not found: check the latest version at https://github.com/jellyfin/jellyfin-androidtv or
  Maven Central under `org.jellyfin.media3` and set it to match the `media3` version in `app/build.gradle.kts`
  (or remove that line, MKV/MP4 still play, only extra audio codecs are lost).
- `PlayerView` theme errors: change `Theme.Lumen` parent in `res/values/themes.xml` to an AppCompat/Material theme.
