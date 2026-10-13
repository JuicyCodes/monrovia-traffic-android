# Monrovia Traffic — Cloud-Connected Android APK (v1.3)

This is an **Android test build project**, using the same Capacitor app ID as your previous APK:
`com.monrovia.trafficlive`. It opens the live Google Cloud Run application at:

https://monrovia-traffic-live-990990560897.europe-west1.run.app

The website runs on your server; the Android APK is a web-view client. No API key is
needed in this repository or inside the APK. **Do not commit API keys to GitHub.**

## QUICK UPDATE — easiest with your existing GitHub repository

You already have a successful GitHub Actions build. **You only need to update one file:**

1. Visit the existing repository `JuicyCodes/monrovia-traffic-android`.
2. Open **Code → capacitor.config.json** in the repository root (not the `www` folder).
3. Click the edit/pencil icon and replace the file with the new `capacitor.config.json` from this ZIP. Commit directly to `main`.
4. GitHub will automatically run **Actions → Build Android APK**.
5. Open the most recent **successful** build → scroll to **Artifacts** → download `Monrovia-Traffic-Android-APK`.
6. Unzip the artifact, transfer `app-debug.apk` to your Android phone, and install it.

**This simple one-file update keeps your existing project files, app ID and icon/build approach.**
You do **not** need to replace `www/index.html` to switch the app to its live server.

## FULL PROJECT ALTERNATIVE

The ZIP includes a standalone project (`package.json`, `capacitor.config.json`, `www/`,
`.github/workflows/build-apk.yml`). Upload its contents to a repository root (retain
`.github/workflows/`) and follow the same Actions build instructions.

## How it works

- The APK loads the live HTTPS website every time the app starts (network access required).
- A changed/redeployed website is shown after reload/reopen; it does not usually require another Android build.
- Server-hosted authentication and database features only work if **the website itself** implements them.
- The APK **does not** make sample traffic information become real live traffic.
- This does **not** transfer the previous v1.2 local UI changes to the published website.
  Modify the live UI in Google AI Studio and redeploy to change what Android users see.
- Any server downtime, login restrictions or hosting/billing changes also affect the APK.

## Testing considerations

This is a proof-of-concept APK build. Capacitor's external `server.url` is designed
for development/live-reload, **not recommended as the final production architecture**.
Before public distribution, plan a production-quality wrapper or PWA/TWA, stable
signing, security review, and testing of location, camera/file uploads, notifications,
Google sign-in, hardware back navigation and any mapping dependencies. Embedded WebViews
sometimes handle Google OAuth sign-in differently from normal browsers.

The GitHub Actions workflow produces a **debug-signed** APK, not a Play Store release.
Fresh GitHub runners may use different debug signing keys. If Android rejects the update
because of a signature mismatch, you may need to uninstall the old demo first. Uninstalling
will delete local-only settings/reports; back them up before doing so.

## API key security

The user-provided API key is **deliberately excluded** from this ZIP. Keep credentials
server-side in Google AI Studio Secrets/Cloud Run configuration and rotate any key
that has been publicly shared. Never embed a private key in an APK or committed code.

## Technical manifest

- Capacitor 6 Android
- App ID: `com.monrovia.trafficlive` (unchanged)
- App name: Monrovia Traffic
- Build workflow: `.github/workflows/build-apk.yml` (same proven workflow)
- Remote URL: `server.url` in `capacitor.config.json`
- HTTPS only; `cleartext: false`
- Error fallback: `www/offline.html`
