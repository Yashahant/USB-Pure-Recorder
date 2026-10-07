# Rebuild and replace the LGPL libusb library

The release APK contains an independent libusb1.0.so for arm64-v8a and x86_64,
loaded dynamically by the app's native transport. The app has no signature
self-check intended to block an interface-compatible library replacement.
Its own application source remains private.

## Library source and a verified standalone build

Download libusb-1.0.30-corresponding-source.zip from the same release. Extract it;
retain COPYING, AUTHORS and the existing copyright notices. The source is the
unmodified libusb 1.0.30 tree used by this APK, including android/config.h and
android/jni/libusb.mk. It needs no USB Pure Recorder source to build.

Install Android NDK r29 (29.0.14206865). From the libusb-1.0.30 directory, use
ndk-build (ndk-build.cmd on Windows) with these arguments, adjusting output paths:

```
ndk-build NDK_PROJECT_PATH=. APP_BUILD_SCRIPT=android/jni/libusb.mk \
  NDK_APPLICATION_MK=android/jni/Application.mk \
  "APP_ABI=arm64-v8a x86_64" APP_PLATFORM=android-31 \
  NDK_OUT=out/obj NDK_LIBS_OUT=out/libs
```

This standalone library build was checked for both packaged ABIs. Use matching
libusb public API/ABI when making a modified replacement. A library change can
break USB capture; do not use a modified build for an irreplaceable recording
before testing it. Preserve the legacy library name libusb1.0.so.

## Replace the library in a local APK

1. Keep a copy of the original APK and save recordings/recovery files externally.
2. In a ZIP/APK editor, replace lib/arm64-v8a/libusb1.0.so and/or
   lib/x86_64/libusb1.0.so with your corresponding rebuilt library. Keep the other
   APK files intact and remove stale APK signatures. APK modification invalidates
   its original signature.
3. Align the modified APK with Android SDK zipalign (including 16 KB native-library
   alignment), then sign it with your own Android APK signing key using apksigner.
   NDK r29 emits native libraries with flexible/16 KB page-size support by default.
4. Android cannot install a different-signature APK as an update over the official
   APK. Save audio/recovery data first; use a disposable emulator or test phone
   and remove the original installation if Android requires it before installing
   your self-signed build. Never publish a modified APK as the official release.
5. Verify the modified APK's signature, start the app, and test supported USB input
   and the stop/save/handoff behavior. The new library must remain ABI-compatible.

These instructions provide the shared-library replacement path; no developer
signing key, private application project or personal data is required or supplied.
Your rights under LGPL-2.1-or-later are not restricted by the free APK terms.
