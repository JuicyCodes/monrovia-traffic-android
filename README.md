# Monrovia Traffic — Android build project

This is a Capacitor-based Android wrapper for the supplied single-page HTML app.
The installable APK is compiled by GitHub Actions (no Android Studio required on your computer).

## Build your APK on GitHub (beginner-friendly)

1. Extract `monrovia-android-ready.zip` on your computer.
2. Sign in to https://github.com and click the + menu > New repository.
3. Call it `monrovia-traffic-android`, select Private or Public, and create it.
4. In the repository click **Add file > Upload files** and upload all files/folders INSIDE the extracted `monrovia-android-ready` folder. **Include `.github`** (it may be a hidden folder).
5. Click **Commit changes**. The automatic **Build Android APK** workflow will start.
6. Select **Actions**, then **Build Android APK**, then its most recent run.
   If the run did not start: click **Run workflow**, choose main, and run.
7. When the green-check successful run finishes, under **Artifacts** download `Monrovia-Traffic-Android-APK`.
8. Unzip the downloaded artifact to find `app-debug.apk`.
9. Copy `app-debug.apk` onto your Android phone, open it in Files, and approve **Install unknown apps** for Files if Android asks. Install and open **Monrovia Traffic**.

The project produces a *debug APK*, suitable for personal installation/testing, not a production-signed Play Store release. It requires the GitHub Actions build runner to access the internet during compilation.

## IMPORTANT: Demo data, not live traffic

The original HTML includes built-in/sample traffic updates, map overlays, travel times, alerts and apparent source/verifications. It does **not** connect to real Google traffic, Facebook traffic groups, radio, police systems, or a traffic data API. SMS verification uses the demo code `123456`; social sign-in, photos, voice memos, public broadcasts, and background notifications are mock features (no real server or broadcast). New incident reports are stored only in the app/browser on the device. Do not use sample traffic conditions to make driving or routing decisions.

A genuine live traffic Android app would additionally need authenticated backend services, a mapping/traffic data provider, backend persistence and verified feeds, real account verification, notifications, and device integration.

## Original project

`www/index.html` holds the whole web UI and demo JavaScript. `capacitor.config.json` defines the Android app display name and ID. `.github/workflows/build-apk.yml` contains the build steps.
