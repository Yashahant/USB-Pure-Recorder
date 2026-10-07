# Test a USB input and report the result

Thank you for trying the free experimental build. We need physical reports across USB microphones, receivers, adapters and Android phones; a successful test is useful too.

## First short test

1. Close other apps that may be using the USB device. Connect it using the cable/OTG adapter you normally use.
2. Launch USB Pure Recorder Test, grant USB access, and open Details. Record the advertised input formats. Empty or unsupported formats should have a reason; the app must not fall back to the phone microphone.
3. Choose the desired supported format. Record for 10–20 seconds, watching for Actual USB capture and any warning. Speak into the connected microphone. Stop, then check that the WAV appears in the recording list and your selected folder.
4. Listen using the list's playback control. If possible, inspect the WAV on a PC for its sample rate, channel count and bit depth. Playback uses Android's normal output; the master WAV remains unchanged.
5. For a device with two independent inputs, record input 1 alone for five seconds, two seconds of silence, then input 2 alone for five seconds. Check L/R mapping on the PC. For a mono mic/adapter, identical channels can be normal; do not assume a two-channel file proves independent stereo.

## Follow-up checks

Use disposable recordings. Try Stop and a second take, background/screen-off capture, rename/playback, and saving to a chosen local folder. For removal testing, unplug during a short take: the app should stop, report removal and save a partial WAV when possible. Reconnect and test a fresh take. Stop and save before changing settings or switching apps that use the USB device.

Longer recordings can reveal power, clock or scheduling issues that a short take misses. Note the duration and any timing warning. Counters showing all accepted bytes written do not rule out every form of device-side loss.

For an analog lavalier through a USB ADC adapter, the **adapter** determines USB format. Check whether its socket expects TRRS headset wiring or TRS microphone wiring and set the lavalier's phone/camera mode accordingly. Successful USB enumeration alone does not prove the analog connection is correct.

## Send an error report

1. In the app, open **Details → Share diagnostics**.
2. Review the text. Recording filenames/locations and session identifiers are redacted from shared reports. Phone model, Android version, USB model/VID/PID, raw binary descriptors, selected format and capture counters remain useful.
3. Open this repository's Issues page and choose a compatibility/error report. Paste the reviewed diagnostic text or attach it as `.txt`.
4. Include app version, device and adapter models, phone/Android version, requested and active formats, exact steps, expected result and actual result. For power/disconnect problems, include cable/hub details and whether a hub supplies external power. Include firmware version only if you know it.

Do not post account information, payment details, passwords, phone/USB serial numbers, private storage paths or private recordings. Custom USB product names or unexpected device/error text can still identify someone; redaction is a convenience, not a guarantee. Screenshots and raw adb/logcat dumps are not automatically redacted. Audio is optional: use a harmless sample only if it is necessary and you choose to share it.

We cannot promise support for every USB device. Clear reports let us reproduce failures, document working combinations and avoid silent format changes. Support currently focuses on the UAC1 formats listed in README.md.
