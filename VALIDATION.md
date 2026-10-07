# Validation for 0.1.2-experimental

- Debug and release builds succeeded. Release is signed, non-debuggable and excludes debug-only emulator fixture activities.
- 42 JVM tests passed: WAV integrity, descriptor parsing, preserved DJI/SPACETOUCH fixtures, invalid-input rejection, meters/storage helpers and shared-diagnostic redaction.
- Debug/release lint completed with zero errors and existing dependency/style warnings.
- 19 native transport checks passed in the emulator: packet framing, ring queue, error handling, concurrent producer/consumer, cancellation/drain and descriptor validation.
- 24 synthetic mono/stereo WAVs across integer 16/24/32 bits and 8/44.1/48/96 kHz independently matched every PCM byte and header on a PC.
- Synthetic stop/drain, packet-fault and disconnect WAV checks passed, as did public WAV publication.
- The libusb dependency rebuilt independently for arm64-v8a and x86_64 without any app source.
- Exact signed release install/launch, no-USB disabled Record, format/device-selection UI and explicit diagnostic-share chooser were tested in the emulator.
- The distribution APK was checked for known private identifiers, local computer paths, physical-test recordings/logs, signing keys and app source. These are excluded from the release artifacts. Third-party copyright notices remain intact.

The recording driver is unchanged from the 0.1.1 BOYA adapter fix. The earlier
physical S23/BOYA-adapter test measured 29.177 seconds, 48 kHz, two identical
channels, 16-bit PCM, all 5601984 accepted audio bytes written, no reported native
fault and no timing-coverage warning in that take. This is a short physical
baseline for the driver; 0.1.2 itself is emulator-tested, not a fresh physical
certification. DJI/Fifine reports from preceding builds are labeled accordingly
in README.md. No general or long-run compatibility guarantee is made.

Build licenses/notices are embedded in the APK. The app's own source/signing keys
are local and private; public corresponding-source material covers libusb only.
