# Changelog

## 0.1.2-experimental — 2026-10-07

First public GitHub compatibility prerelease; free APK, with the app's own source kept private.

- Replace the fixed non-DJI “device not physically verified” ready-screen label with a neutral “USB format detected” status. Active capture remains separately verified.
- Redact recording filenames, storage locations, session identifiers and recognizable storage paths from explicitly shared diagnostic text.
- Include distribution terms and third-party notices/licenses with the release.
- Retain the existing UAC1 driver, format boundaries, PCM/WAV behavior and USB routing safeguards.

## 0.1.1-experimental — earlier local test build

- Fix discovery when malformed playback-only class-format descriptors rejected an independent valid input.
- Add regression tests using the SPACETOUCH 0666:0880 adapter descriptor dump, while keeping malformed recording inputs rejected.
- Physically verify a short BOYA BY-M1/adapter recording on Galaxy S23 at 48 kHz, two channels, 16-bit PCM; preserve the adapter's identical mono content in both channels.

## 0.1-experimental — earlier local test build

Descriptor-driven UAC1 mono/stereo signed-integer PCM capture, WAV storage, meters, recording list, playback, rename, theme/folder settings and optional diagnostics. Earlier DJI-only and advanced UAC2/UAC3 experiments are separate apps and are not part of this release.
