# Privacy — experimental 0.1.2

The app is offline and has no Internet permission, analytics/ad SDK, account login, cloud backup or automatic upload. It does not include the developer's private recordings, physical-test logs, computer username/paths, wireless-debugging details or signing keys.

## Data stored locally

The app stores recordings as WAV, local capture diagnostics and state, playback/recording-list information, theme preference and the chosen local recording-folder permission. It reads USB descriptors to identify and validate input formats. Android supplies manufacturer/model and OS version for a diagnostic report; the app does not request a phone serial number or read contacts, messages or location.

Audio and per-capture logs stay on the device. Android MediaStore indexes public recordings. A custom local folder is selected through Android's document picker. Cloud document providers are not an intended recording destination. App backup/data extraction is disabled in this build. Removing the app can remove its private recovery files; public WAVs generally belong to shared storage.

## Optional sharing

**Details → Share diagnostics** opens Android's share sheet only after a user action. It does not send anything automatically or include recorded audio. The shared text includes app version, phone model, Android version, USB product/VID/PID, raw binary descriptors, selected format, counters, error details and kernel-handoff status where available.

The app redacts session identifiers, recording filenames, public recording locations, content URIs and recognizable Android/Windows storage paths from the shared text. This does not scrub arbitrary personal text in USB product names or all possible error messages. Review the report before posting. Raw logcat, screenshots, manually copied logs and optional WAV attachments require separate review.

If you post a report on public GitHub Issues, it is public and handled under GitHub's policies. Include technical details needed to reproduce the issue; no personal audio or account details are required. No report is uploaded to GitHub by the app itself.

## Permissions

- USB device permission: access the explicitly selected external USB input.
- USB host feature: Android phone/tablet must support USB host/OTG.
- Foreground service / connected-device service: keep the explicit USB capture running with a notification.
- Notifications: recording status and a Stop action.
- Wake lock: keep capture running when the screen is off.
- User-selected folder access: create WAVs in that local folder.

The APK has no microphone runtime permission because this version captures directly from the permitted USB device rather than AudioRecord. There is no phone-microphone or Bluetooth fallback.

Questions or privacy reports can be raised through the repository's Issues page without uploading audio or sensitive information.
