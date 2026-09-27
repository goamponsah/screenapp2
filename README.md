# Screen Recorder (Android)

A minimal native Android app that records the device's own screen using
MediaProjection + MediaRecorder, and saves the .mp4 file to
**Movies/ScreenRecordings** (visible in the Gallery/Files app, via MediaStore).

## How to build
1. Open this folder in Android Studio (File → Open).
2. Let Gradle sync (it will download the wrapper automatically).
3. Connect a phone (USB debugging on) or use an emulator, then Run ▶.

## How it works
- `MainActivity.kt` — UI with Start/Stop buttons, requests screen-capture
  permission via `MediaProjectionManager`.
- `RecordingService.kt` — foreground service that does the actual capture
  and writes the video with `MediaRecorder`, saved through `MediaStore`
  so it works on Android 10+ scoped storage as well as older versions.
- Minimum SDK: Android 7.0 (API 24). Target/compile SDK: 34.

## Get an APK without installing Android Studio
This project includes a GitHub Actions workflow (`.github/workflows/build-apk.yml`)
that builds a debug APK automatically on GitHub's servers.

1. Create a new repo on GitHub and push this whole folder to it.
2. Go to the repo's **Actions** tab — the "Build Debug APK" workflow runs
   automatically on push (or click "Run workflow" to trigger it manually).
3. Once it finishes (a couple of minutes), open the completed run and
   download the **app-debug-apk** artifact — that's your installable APK.
4. Transfer it to your phone and install it (you'll need to allow
   "install unknown apps" for whichever app you use to open it, since
   it isn't from the Play Store).

## Notes
- Recording continues in the background as a foreground service with a
  persistent notification (required by Android for screen capture).
- No GitHub/Railway hosting is needed for this — it's a native app, built
  and installed via Android Studio or distributed as an APK/AAB.
- To publish, generate a signed APK/bundle: Build → Generate Signed Bundle/APK.
