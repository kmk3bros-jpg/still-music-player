# Still — your personal music player
- Local IndexedDB audio storage, playlists, shuffle, repeat off/all/one, seek, and Media Session controls/metadata where the browser supports them.
- Installable PWA with an offline-cached interface. Files you import while online remain playable offline on that same device.
- Responsive interface with a compact player and home-screen icon.


## Windows setup


1. Install a current version of Node.js LTS from [nodejs.org](https://nodejs.org/) (only needed for the optional local server).
2. Extract or copy the `pocket-player` folder somewhere convenient.
3. Open PowerShell in that folder (File Explorer address bar → type `powershell` → Enter).
4. Run `npx.cmd http-server . -p 8080 -c-1` and allow the package download if prompted. Alternatively, install Python and run `python -m http.server 8080`.
5. On the PC, open `http://localhost:8080`. Import a few audio files and test playback, playlists, and reload behavior.


A local HTTP server is needed: service workers and IndexedDB do not work reliably from a `file://` page. `localhost` is treated as a secure context for development.


## Free HTTPS deployment


### GitHub Pages


1. Create a GitHub account/repository and upload the *contents* of this folder to the repository's root.
2. In repository **Settings → Pages**, choose deploy from the main branch and root folder.
3. Wait for GitHub Pages to publish, then open its `https://...github.io/.../` address.


### Cloudflare Pages


1. Sign in to Cloudflare and choose **Workers & Pages → Create → Pages → Upload assets**.
2. Upload this folder (or a ZIP containing its contents), give the project a name, and deploy.
3. Use the resulting HTTPS address.


Both provide free HTTPS hosting for this static project. Follow each provider's current dashboard prompts; their screens may change. The host serves only the app files: your imported audio remains in browser storage and is not uploaded.


## Install on iPhone


1. Publish the site over HTTPS using one of the options above.
2. On the iPhone, open the published address in **Safari**.
3. Tap **Share** → **Add to Home Screen** → **Add**.
4. Open **Still** from the Home Screen. Import songs while the app is open, and keep it open until the import finishes. Once imported, songs can play offline on that iPhone.


Imported music is stored separately per browser/device. Moving or deleting the website does not transfer the audio library. Keep a copy of your original audio files.


## iOS and browser notes


- iOS Safari and installed web apps support audio playback and often continue audio after locking the screen, with lock-screen controls through Media Session where supported. iOS can suspend web apps, and behavior can vary by iOS release, power state, and how playback was started; this cannot be guaranteed like a native player. Start playback from a user tap and try Add to Home Screen for the app-like experience.
- Background downloads are not provided. Keep Still open in the foreground while importing; large files can take time.
- The app caches its interface separately from the songs. IndexedDB audio remains on the device, but browser storage can be cleared by the user or evicted by the operating system when space is low. Export/backup of the library is not currently built in, so preserve your original files.
- Storage capacity varies by browser and free device space. The app reports no upload or account use; the browser owns the local database.
- Safari's folder chooser may not appear. Use **Add music** to select files individually or multiple files.
- Background playback, lock-screen metadata, and media keys depend on browser/OS support. The app uses the standard Media Session API when available; some controls may not appear on every iPhone/browser version.
