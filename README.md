# in-app-browser-test

A single-page diagnostic used to check whether a web page can escape a social-app
in-app browser (Facebook, Instagram, Messenger, TikTok, Viber) into the real browser,
and whether clipboard access works there.

Open the hosted page inside the app under test, tap the buttons top to bottom and copy
the log at the bottom.

## Two pages

- `index.html` — the raw diagnostic: every probe on its own button, nothing decided for you.
- `flow.html` — the DEV-48595 step-1 gate as a working prototype. Open it and follow the
  screen; it blocks or passes on its own and shows a live camera once access is granted.
  The user journey it implements is drawn in [FLOW.md](FLOW.md). Append `?ua=<string>` to
  simulate another app's user agent when testing detection on a desktop.

No dependencies, no build step — `index.html` is the whole thing.

## Run locally

Serve the file over HTTP (in-app browsers won't open `file://` links):

```bash
python3 -m http.server 8000
# or
npx serve .
```

Then open `http://localhost:8000` — on a phone, use your machine's LAN IP or a tunnel (e.g. `ngrok http 8000`) so the in-app browser on the device can reach it.

## Deploy to GitHub Pages

GitHub Pages is already configured to serve from the `main` branch root (https://sergejsd-sf.github.io/in-app-browser-test/). Deploying is just:

```bash
git push origin main
```

GitHub rebuilds the page automatically within a minute or two of the push.
