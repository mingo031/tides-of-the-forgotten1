# Tides of the Forgotten — Android (Capacitor) starter

Your 2013 Mac only needs to run **a web browser + Git**. All the heavy lifting
(Android SDK, Gradle) happens **in the cloud** — so your hardware is not the blocker.

## Folder layout
```
tides-app/
├─ package.json
├─ capacitor.config.json     ← change "appId" to your own (e.g. com.yourname.tides)
├─ www/
│  └─ index.html             ← the hardened game (already mobile-ready)
└─ .github/workflows/
   └─ android.yml            ← cloud build: makes an installable APK for you
```

## Path A — GitHub Actions (recommended, zero local tools)
1. Make a free GitHub account and create a new repository.
2. Upload these files (keep the folder structure). You can drag-drop in the browser.
3. Open **capacitor.config.json** and change `appId` to your own reverse-domain id.
4. Go to the **Actions** tab → the "Build Android (debug)" workflow runs automatically
   (or click "Run workflow"). It takes a few minutes.
5. Open the finished run → **Artifacts** → download `tides-debug-apk`.
6. Copy the `.apk` to your Android phone and install it (allow "install unknown apps").
   That's your game running as a real app.

## Path B — GitHub Codespaces (interactive, more control)
1. In your repo, click **Code → Codespaces → Create codespace**. This gives you a full
   Linux machine in the browser (free tier ~60 hrs/month) — no install on your Mac.
2. In its terminal:
   ```
   npm install
   npx cap add android
   npx cap sync android
   cd android && ./gradlew assembleDebug
   ```
3. Download `android/app/build/outputs/apk/debug/app-debug.apk` from the file explorer.

## Going to the Play Store (later)
- The Play Store needs a **signed .aab**, not a debug .apk. When you're ready, we add a
  keystore + repo "secrets" and switch the workflow to `bundleRelease`. Ask and I'll
  generate that workflow.
- New **personal** Play accounts must run a **closed test with 12 testers for 14
  continuous days** before production. Plan for that (real people, real devices).
- You collect **no user data**, which makes the Data Safety + privacy forms simple.

## Even simpler alternative — PWABuilder (no Capacitor at all)
If you'd rather avoid the toolchain entirely: host `www/index.html` online (e.g. GitHub
Pages — free), add a web-app manifest + offline service worker, then paste the URL into
**pwabuilder.com**, which generates a Play-ready Android package in the browser. Trade-off:
it uses a Trusted Web Activity, so it needs that hosted URL. Ask if you want to try this route.
