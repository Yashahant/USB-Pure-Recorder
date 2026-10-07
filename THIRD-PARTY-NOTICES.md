# Third-party notices

The application dynamically links **unmodified libusb 1.0.30**, licensed under
LGPL-2.1-or-later. libusb copyright attribution remains in its distributed source.
A complete copy of LGPL 2.1 is LICENSE-LGPL-2.1.txt and is embedded in the APK.
The release asset libusb-1.0.30-corresponding-source.zip includes the exact upstream
source tree used in the build, its Android config/build files, COPYING and AUTHORS.
No USB Pure Recorder application source is in that archive.

The separate libusb shared library is lib/<ABI>/libusb1.0.so in the APK. The app's
native transport dynamically links it; interface-compatible replacements are
permitted. See LIBUSB-REPLACEMENT.md for build/replacement instructions. The
release uses the LGPL 2.1 shared-library mechanism and preserves user modification
and reverse-engineering rights for debugging such modifications.

The app also uses Kotlin, AndroidX/Jetpack Compose and the Android NDK C++ runtime.
See DEPENDENCIES.txt for resolved libraries. Their upstream license texts/notices,
and the Android NDK distribution NOTICE, are supplied in Third-Party-Notices.zip
and embedded under assets/ in the APK. These authors' copyright/attribution names
are third-party legal notices, not the app developer's personal data. They remain
intact. Android platform components are supplied by Android/the phone vendor.

This repository does not license USB Pure Recorder's own private source as open
source. Its free APK distribution terms are in TERMS.md. Third-party license
rights remain unaffected. No proprietary USB Audio Recorder PRO code is used.
