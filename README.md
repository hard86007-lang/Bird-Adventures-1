# Birds Around the World Adventures – build guide
## Run / install as an app (Android, iOS, desktop)
1. Host this folder over HTTPS (Netlify, GitHub Pages, Firebase Hosting). Open it in Chrome/Edge/Safari and choose "Install app" / "Add to Home Screen". The manifest, service worker (offline play) and icon.svg are already set up.
2. Generate PNG icons: `npm i && npm run icons` (creates icon-192.png / icon-512.png).
## Native Android/iOS build (Capacitor)
`npm i && npm run icons && npx cap add android && npx cap sync && npx cap open android` (use `ios` on a Mac). Build the APK/AAB in Android Studio. Use `npx @capacitor/assets generate` to create all launcher sizes from a 1024px icon.
## Google Sign-In
1. Google Cloud Console → APIs & Services → Credentials → OAuth client ID (Web). Add your hosting URL as an Authorized JavaScript origin.
2. Put the client ID in `auth.js` (CLIENT_ID).
3. Progress is stored locally; to keep it across devices, deploy a tiny backend (Firebase Function, Supabase, etc.) that verifies the Google ID token and stores/returns the save JSON per `sub`, then set SYNC_URL in `auth.js`. Without SYNC_URL, sign-in works but saves stay on the device.
4. For the native Capacitor app, use the `@codetrix-studio/capacitor-google-auth` plugin (web GSI popups are unreliable inside WebViews).
