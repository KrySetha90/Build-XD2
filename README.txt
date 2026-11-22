FORGE STUDIO  (Android project)

What it is
  An Android app that turns a web project (.zip or .html) into a real installable APK, on the phone,
  with no server and no Gradle. Dark amber look, 4 steps: bring project > test it > name & icon > Forge.

How to build it with WZH 2 APK
  1. Unzip nothing. In WZH 2 APK open the Code tab and import / open this project (the ForgeStudio folder
     or this zip). The manifest is at app/src/main/AndroidManifest.xml and build.gradle is at app/build.gradle.
  2. Press Build. First build needs internet (it downloads Java tools once).
  3. Install the APK it gives you and open "Forge Studio".

How to build it on GitHub instead (no WZH needed)
  1. Make a free GitHub account and a new repository.
  2. Add file > Upload files > choose ForgeStudio.zip (just the zip, no need to unpack it) > Commit.
  3. Add file > Create new file. Name it exactly:  .github/workflows/build.yml
     Paste the contents of build.yml (shipped next to this zip) > Commit.
  4. Open the Actions tab > "Build Forge Studio APK" > wait about 5 minutes.
  5. Open the finished run, scroll to Artifacts, download ForgeStudio-apk, unzip it, install the .apk.
  (The yml unpacks the zip by itself. You can also upload the loose files instead, including .github.)

How to use it
  Choose your .zip/.html > Run demo to test > set the name and icon > Forge APK > Install now.
  The finished APK is also saved in your Downloads folder.

How it works
  The running app copies its own APK, puts your files in assets/app/, changes the package name, app
  name and icon, and signs the copy (v1 signature, key stored in the Android Keystore). An APK made
  this way opens assets/app/index.html full screen in a WebView.

Limits (be aware)
  - Android 10 or newer (minSdk 29). Output apps are signed with a v1 signature, which Android 11+ accepts
    for apps targeting SDK 29. Android may show a "built for an older version" notice on newer phones.
  - Every built app has its own random package name, so each one installs separately.
  - The icon is swapped only if the build keeps res/.../ic_launcher.png paths; the app name only if the
    manifest label is plain text. The screen tells you when either was not applied.
  - Built apps load your files from the phone (file://). Pages that need a web server (some fetch() calls,
    ES modules in some setups) may need small changes.
  - Windows .exe and iPhone .ipa cannot be made on a phone. Use the GitHub build kit from the web page.
  - Checked: the Java compiles against Android's API, and the manifest patching and signing steps were
    tested on a computer (jarsigner reports "jar verified"). NOT tested: running on a real phone.
    If the build or the install fails, send me the error text.
