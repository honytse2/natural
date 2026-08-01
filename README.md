# Natural Flow

A 35-second reset that returns you to your own rhythm, whatever the situation is doing.

Offline-first PWA. No account, no server, no network calls. All data stays in the browser's
local storage on your phone.

---

## Deploy (about 4 minutes)

1. Go to <https://github.com/new>. Name the repo `natural-flow`. Set it **Public**. Create.
2. On the empty repo page, click **uploading an existing file**.
3. Drag in all six files:
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
   - `icon-192.png`
   - `icon-512.png`
   - `icon-maskable-512.png`
4. Commit.
5. **Settings → Pages**. Source: `Deploy from a branch`. Branch: `main`, folder: `/ (root)`. Save.
6. Wait ~60 seconds, then open:
   `https://YOUR-USERNAME.github.io/natural-flow/`

HTTPS comes free with GitHub Pages, which is what the service worker needs.

## Install on the phone

1. Open that URL in **Chrome on Android**.
2. Menu (⋮) → **Add to Home screen** / **Install app**.
3. It launches full-screen with no browser chrome, and works with no signal.

On iOS use Safari → Share → **Add to Home Screen**. Chrome on iOS cannot install PWAs;
that is an Apple restriction, not a bug in the app.

> Put the icon in the bottom dock, not on page 3. The icon being visible is the reminder —
> the app can't send you a notification, and shouldn't.

## Updating it later

Edit `index.html` on GitHub, commit, then bump `CACHE = 'natural-flow-v1'` to `v2` in `sw.js`.
Without the version bump the service worker keeps serving the old cached copy.

Personal lines live in the `LINES` array. The three reset beats live in `BEATS`.
Both are plain text at the top of the script block — edit freely.

## Your data

- Stored under the key `nf.v1` in localStorage, on that device only.
- **Trend → Export as CSV** gives you `date, natural_rhythm, reps, heavy_reps, note`.
- Clearing Chrome's site data for the domain wipes it. Export every month or two.
