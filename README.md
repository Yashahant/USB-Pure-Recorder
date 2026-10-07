# USB Pure Recorder — Free Android USB Audio Recorder (Experimental)

**Record the USB PCM your device sends. Keep its format visible. Save an uncompressed WAV.**

USB Pure Recorder is a small, free Android app for people who want to know what their USB microphone, receiver or analog-to-USB adapter is actually sending to their phone. It uses direct USB Audio Class 1 capture for supported inputs. There are no ads, accounts, paid recording features, subscriptions or automatic uploads in this release.

**Public compatibility test — version 0.1.2-experimental.** This is a GitHub APK prerelease. It is not currently published on Google Play, and broad compatibility has not been established.

## Download and install

[Download the experimental APK](https://github.com/Yashahant/USB-Pure-Recorder/releases/tag/v0.1.2-experimental) · [Report an issue](https://github.com/Yashahant/USB-Pure-Recorder/issues) · [Testing guide](TESTING.md)

1. Download `USB-Pure-Recorder-0.1.2-experimental.apk` from that release.
2. Android 12 or newer, USB host/OTG support, and a compatible 64-bit ARM phone are required. An x86_64 build is also bundled for emulator tests.
3. Allow installation from the browser/file manager you used, then install the APK. It is signed, non-debuggable, and contains no emulator fixture activities.
4. Connect the USB audio device and approve USB access when asked. Permission alone never starts a recording.
5. Inspect the advertised formats, choose a supported input/format, then tap Record. During recording, the screen shows the verified active USB capture format. Tap Stop to finalize and save the WAV.

This is a direct download. Google Play installation and automatic updating are not provided by this prerelease. Always use the release page and its checksum to identify the official APK.

## Why try this app?

- **Format transparency:** see the USB input's advertised options and the active format once capture starts. A device's playback capabilities are not treated as microphone-input capabilities.
- **Incoming PCM preserved:** no app noise reduction, AGC, echo cancellation, EQ, limiter, normalization, resampling, up-conversion, mixing or lossy encoding is applied to the master recording.
- **USB input stays explicit:** there is no built-in phone microphone or Bluetooth recording fallback. USB removal stops capture and finalizes the partial WAV where possible.
- **Free and offline:** no app account, ad SDK, analytics SDK or Internet permission. The master audio stays on the device unless you share it yourself.
- **Small, focused workflow:** Record/Stop, two-channel meters, recent recordings, local playback, rename, dark mode and folder selection.
- **Useful diagnostics:** format selection, USB setup, accepted/written bytes, transport errors and timing-risk counters make compatibility problems easier to investigate.

These are concrete design strengths. They are not evidence that this beta beats every Play Store recorder or every manufacturer audio path. Honest bit-depth reporting is useful; 16-bit audio is not automatically bad audio, and a 24-bit USB format does not prove 24 bits of effective microphone resolution.

## Free USB Audio Recorder PRO alternative for Android

USB Pure Recorder is a free, focused alternative for people who need direct USB PCM-to-WAV recording from supported UAC1 microphones, receivers and ADC adapters. It shows the selected USB input format and preserves its incoming PCM without app DSP or lossy encoding.

This experimental release supports the formats listed below; it does not claim the same features, device coverage or proven reliability as USB Audio Recorder PRO. Test your exact phone and USB device. This project is independent and is not affiliated with or endorsed by USB Audio Recorder PRO or its developer.

## Supported USB recording formats

| Property | This UAC1 experimental app |
| --- | --- |
| USB protocol | USB Audio Class 1, Type I signed integer PCM |
| Channels | 1 or 2, as exposed by the selected input |
| Sample layout | 16 bits / 2 bytes; packed 24 bits / 3 bytes; 32 bits / 4 bytes |
| Sample rates | Advertised 8,000–192,000 Hz; 48,000 Hz preferred when offered |
| Endpoint | One isochronous IN data endpoint; USB full/high speed; bInterval=1 |
| Rate selection | Advertised discrete rates or offered values within an advertised continuous range; variable-rate inputs require rate control and confirmation |
| Configuration | Active USB configuration; the app does not switch configurations |
| Master file | Uncompressed little-endian PCM WAV; sample metadata matches stored bytes |

Not supported in this app: UAC2/UAC3, floating-point PCM, 24 valid bits in a 32-bit container, more than two channels, extra/feedback endpoints, other endpoint intervals, SuperSpeed USB audio, proprietary protocols, Bluetooth audio or the phone's built-in microphone. Those limitations are intentional boundaries of this small UAC1 test app.

The native driver checks the selected USB format and route again before capturing. It copies complete frame-aligned packet payloads into a queue and writes their PCM bytes unchanged. Stop cancels future transfers, drains already accepted audio and patches the WAV header. Transport faults are reported; timing warnings estimate coverage risk and are not an exact lost-sample count. No software can certify device-internal processing or data loss solely from USB descriptor information.

## Mono versus two-channel audio

A mono microphone connected through an adapter can arrive as two USB channels containing the same mono signal. The app preserves both when that is the selected format; it does not manufacture stereo separation or silently downmix. Genuine independent left/right audio requires the device to send independent channel content.

A receiver may mix, limit or otherwise process audio before USB. The app preserves what reaches USB; it cannot remove the receiver's processing or infer the microphone's original ADC resolution.

## Features and storage

The ready screen shows device connection, selectable advertised format and recent recordings. Recording opens a separate page with a timer, independent channel meters and Stop. Meters inspect samples without changing the stored PCM. Stopped takes save automatically with a timestamped default name. Rename and playback are available from the recording list.

The inherited default destination is **Music/DJIRecorder/** with `DJI_*.wav` names. Settings lets you select a local Android storage folder and set dark mode for the app. Names and the folder name are historical branding, not a claim that only DJI devices work. Playback uses normal Android audio output and may be converted by Android for listening; the original WAV remains unchanged. Public saving uses MediaStore or a user-selected local folder. A failed public save retains the original in app storage where possible; report the error before removing the app.

Capture runs in a foreground service with a visible notification and a wake lock, so it can continue in the background or with the screen off. Phone power policies and hardware still need physical tests. There is no pause, editing, cloud storage, AI processing, RF64 or automatic file splitting. Recording stops before the classic WAV size limit.

## What has been tested?

| Setup / check | Evidence and limits |
| --- | --- |
| Galaxy S23 + BOYA BY-M1 through SPACETOUCH USB Audio adapter (0666:0880) | The 0.1.1 driver baseline produced a valid 29.177-second 48 kHz, two-channel, 16-bit WAV. Nonzero audio; identical L/R samples; all accepted PCM bytes written; no reported transport fault or timing warning in that short take. The adapter's 24-bit alternate is playback only. |
| DJI Mic Mini | Earlier DJI-only build physically tested on Galaxy S23; the retained real descriptor dump is a regression fixture. A user reports the generalized 0.1 build also worked. |
| Fifine K669B | User reports successful recording with the preceding generalized build; not a new certification for 0.1.2. |
| Public 0.1.2 build | Build/lint, descriptor/privacy unit tests and emulator native/WAV/release checks. Full validation results are in VALIDATION.md. |

The public release retains the 0.1.1 recording driver and BOYA adapter fix. Changes concern status wording, shared diagnostic redaction and release notices. Emulator tests validate code behavior; they cannot certify a physical USB clock, Android kernel handoff, power supply, TRRS wiring or every device's reliability. **This is where community testing helps.**

## Help make the compatibility list useful

Try a short disposable recording with your own USB device. Both successful and unsuccessful reports are welcome. Tell us the device/adapter model, phone model, Android version, selected format, steps and result. For an error, open **Details → Share diagnostics**, review the text, and paste it into a GitHub issue. No audio sample is required.

[Start with the testing guide](TESTING.md). Check [PRIVACY.md](PRIVACY.md) before posting public logs. Reports help identify exactly what fails instead of guessing a higher bit depth or falling back to a different microphone.

## Free distribution; app source remains private

The APK is free to download and use. This repository contains release documentation, feedback and third-party notices; **the app's own Kotlin/C++ source and signing keys are not published**. GitHub's automatically generated source archives contain this documentation repository, not the app project.

The APK dynamically uses unmodified **libusb 1.0.30**, licensed LGPL-2.1-or-later. Its complete corresponding upstream source, license and Android build/replacement instructions are distributed with the release. This existing open-source dependency is separate from the app's private code. See [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md) and [TERMS.md](TERMS.md). No proprietary USB Audio Recorder PRO source is used.

DJI, BOYA, FIFINE, Samsung and other product names identify hardware only. This project is independent and is not an official manufacturer app or endorsement.

## Common questions

**Can I use this instead of USB Audio Recorder PRO?**
For a supported UAC1 input, you can try this free app for direct PCM-to-WAV recording.
Check the format limits and testing guide first; compatibility with one recorder
does not establish compatibility with this experimental app.

**Can I record a USB microphone on Android without changing its PCM format?**
For the supported UAC1 layouts in this app, capture preserves the selected input's
incoming PCM bytes and writes accurate WAV metadata. Unsupported formats are
rejected with diagnostics; the app does not silently resample or change bit depth.

**Does this give every Android USB microphone 24-bit recording?**
No. Packed 24-bit WAV capture is offered only when the USB recording input
advertises the supported native 24-bit layout and stream setup succeeds. A 16-bit
USB ADC stays 16-bit. Playback-only 24-bit support is not microphone-input support.

**Can I try a DJI Mic Mini, Fifine K669B or BOYA BY-M1 USB adapter?**
These are useful starting points for community compatibility reports. See the
tested-setup table above; a BOYA analog mic needs a suitable ADC adapter, and the
adapter sets the USB format. Test your exact phone/device combination.
