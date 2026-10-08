# Ding!

Cook several foods so they all finish at the same time.

## Hosting (GitHub + Cloudflare Pages)
The app is plain files in `public/`. There is no build step.

1. Put this folder in a GitHub repository (README.md and public/ at the top level) and push it.
2. In Cloudflare: Workers & Pages > Create > Pages > Connect to Git, and choose the repository.
3. Build settings: Framework preset **None**, Build command **exit 0**, Build output directory **public**.
4. Deploy. Cloudflare gives you an address ending in .pages.dev (you can add your own domain later).

Every push to the repository redeploys automatically. When you change the app, also change the
version number at the top of `public/sw.js` (the CACHE line) so phones drop the old offline copy.

## Put it on your iPhone
1. Open the .pages.dev address in **Safari** on the iPhone.
2. Tap Share, then **Add to Home Screen**, then Add.
3. Open Ding! from the Home Screen icon. It runs full screen with its own launch screen, like a normal app.

## Files (in public/)
- index.html: the whole app (scheduling engine, screens, starter food list)
- manifest.webmanifest, icons/: Home Screen name and icon
- splash/: launch screens for iPhone 15, 15 Pro, 15 Plus and 15 Pro Max (light and dark)
- sw.js: offline cache
- _headers: tells Cloudflare not to cache the app page and service worker, so updates arrive promptly

## How the timing works
Every time shown is recomputed from the same inputs: your dinner time, each food's cooking time plus any
+/- adjustments, and the moment you pressed Mark started or Mark done. A food that hasn't started yet
starts at (dinner time - cooking time). In "Finish together" mode the dinner time becomes the latest of:
your chosen time, the finish of anything already cooking, and now + cooking time for anything that should
already have started. Times are stored in milliseconds and only rounded for display.

Your foods and the meal in progress are saved on the phone, so closing the app mid-meal doesn't lose the timers.

## iPhone notes
- Keep Ding! open on screen while cooking. iOS pauses web apps in the background, so start/ready alerts
  sound when the app is on screen. The app asks iOS to keep the screen awake during a meal.
- Tap anything once after opening so iOS allows sound.
- Buttons give a light haptic tap on iOS 18 and later.
