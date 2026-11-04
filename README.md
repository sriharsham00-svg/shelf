# Shelf: Android app project

Wraps the Shelf web app (www/index.html) as an Android app with Capacitor.
Native extras: reminders that fire when the app is closed, and keep-screen-on while reading.

## Easiest: build the APK in the cloud (no Android tools needed)
1. Create a new GitHub repository and upload everything in this folder (keep the .github folder).
2. Open the repo's Actions tab, choose "Build APK", press "Run workflow".
3. When it finishes, download the "shelf-apk" artifact, unzip it, and copy app-debug.apk to your phone.
4. Open it on the phone and allow "Install unknown apps" when asked.

## Or build locally (needs Node 20+, JDK 17, Android Studio)
    npm install
    mkdir -p www/vendor && cp node_modules/pdfjs-dist/build/pdf*.min.js www/vendor/
    sed -i 's#https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/#vendor/#g' www/index.html
    npx cap add android && npx cap sync android
    cd android && ./gradlew assembleDebug
The APK appears at android/app/build/outputs/apk/debug/app-debug.apk

This produces a debug APK for your own phone. Publishing to Google Play needs a signed release build.
