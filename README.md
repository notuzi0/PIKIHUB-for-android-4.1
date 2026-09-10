# PikiHub APK — Build It Online (No Installs, No Terminal)

This folder is a ready-to-go Android app project (Apache Cordova) wrapping your
PikiHub website in a WebView. It's configured for:

- **minSdkVersion 16** (runs on Android 4.1 Jelly Bean and up)
- **Hardware back button** goes back in page history, and exits the app if
  there's nothing left to go back to

You never touch a command line. GitHub's servers do the actual building.
Follow these steps exactly:

## Step 1 — Create a GitHub account (skip if you have one)
Go to https://github.com/join and sign up. It's free.

## Step 2 — Create a new repository
1. Click the **+** icon top-right → **New repository**
2. Name it anything, e.g. `pikihub-app`
3. Leave it **Public** (Actions minutes are free & unlimited for public repos)
4. Click **Create repository** (don't add a README/gitignore on this screen)

## Step 3 — Upload this project
1. On your new empty repo's page, click **"uploading an existing file"**
   (link shown on the empty repo page)
2. Drag the **entire contents** of this folder (not the folder itself — its
   contents: `config.xml`, `package.json`, `www/`, `res/`, `.github/`) into
   the browser upload box
   - Note: GitHub's drag-and-drop upload UI sometimes hides dot-folders like
     `.github`. If `.github/workflows/build-apk.yml` doesn't appear after
     upload, use "Add file → Create new file", type the path
     `.github/workflows/build-apk.yml` in the name box, and paste in the
     contents of that file manually.
3. Scroll down, click **Commit changes**

## Step 4 — Let it build
1. Click the **Actions** tab at the top of your repo
2. You'll see a workflow run called "Build PikiHub APK" already running
   (it starts automatically on upload). Click it.
3. Wait 3–6 minutes for the green checkmark ✅

## Step 5 — Download your APK
1. Still on that workflow run page, scroll to the bottom **Artifacts** section
2. Click **PikiHub-debug-apk** to download a zip
3. Unzip it — inside is your `.apk` file
4. Transfer it to your Android phone (email it to yourself, Google Drive, USB,
   whatever's easiest) and tap it to install
   - You'll need to allow "install unknown apps" for whatever app you used to
     open the file — Android will prompt you for this automatically

That's it — no Android Studio, no SDK installs, no typing in a terminal.

## Re-building after changes
Every time you edit `www/index.html` and push/upload the change to GitHub,
the Actions workflow re-runs automatically and a fresh APK will appear in
Actions → (latest run) → Artifacts.

## Notes
- This produces a **debug APK** (unsigned/debug-signed), which is fine for
  installing on your own device via "unknown sources," but not for
  publishing to the Play Store. If you eventually want a Play Store release
  build, that needs a signing key — say the word and I'll add that step too.
- `minSdkVersion 16` is quite old (2012-era Android). To make that work I
  pinned the build to an older Cordova Android platform version
  (`cordova-android@7.1.4`) and JDK 8, since newer Cordova versions dropped
  support for such old devices. This is all pre-wired in the workflow file —
  you don't need to do anything for it to take effect.
