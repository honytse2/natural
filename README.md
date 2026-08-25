# Natural Flow

A 35-second reset that returns you to your own rhythm, whatever the situation is doing.

Two doors in:

- **Reset** — the moment under load. Three beats, then bank the rep.
- **Connect** — the moment under no load. One question about what is in the way, one tap,
  one line, and you are out. Under fifteen seconds by design.

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

## Connect

Open the app at `#connect` and it lands straight on the prompt — no home screen, no tab bar,
nothing to browse. Tap **Done**, read the line it gives back, put the phone down. The screen
dims itself and there is deliberately no way onward from there.

Installed on the home screen it stays ended, and reopening the app starts you back at the
anchor. In an ordinary browser tab there is nothing to be pushed out of, so after the screen
has rested a few seconds it returns to the anchor by itself rather than sitting there looking
crashed.

### Getting the reminder to fire

A static site on GitHub Pages **cannot** send you a notification once it is closed. Web Push
needs a server and a subscription; the Notification Triggers API never shipped broadly. So the
reminder has to come from the phone, not the app:

1. Set a repeating alarm in the **Clock** app, or a repeating event in **Calendar**.
2. Point it at `https://YOUR-USERNAME.github.io/natural-flow/index.html#connect` — the
   address is printed on the Lines tab, ready to copy.
3. One or two a day, at irregular times, **never on the hour**. More than that and the
   prompt becomes wallpaper.

Android also exposes a long-press **Connect** shortcut on the installed app icon.

## Lines

The **Lines** tab is the corpus: eleven connection lines and twenty flow lines to start with,
and anything you add yourself. Each line carries a tag — `connection` lines are what Connect
draws from, and the Anchor screen draws from everything.

Keep a line, tap any line you wrote to edit or delete it. That is the whole feature, and it is
the important one: re-reading your own writing is what the mode is built to reproduce.

## Updating it later

Edit `index.html` on GitHub, commit, then bump `CACHE = 'natural-flow-v4'` to `v5` in `sw.js`.
Without the version bump the service worker keeps serving the old cached copy.

Seeded lines live in the `LINES` and `CONNECT_LINES` arrays, the Connect prompts in `PROMPTS`,
and the three reset beats in `BEATS`. All plain text near the top of the script block — edit
freely. Lines you add in the app live in localStorage, not in the file.

## Your data

- Stored under the key `nf.v1` in localStorage, on that device only: `days` for the log,
  `lines` for anything you kept.
- **Trend → Export as CSV** gives you
  `date, natural_rhythm, reps, heavy_reps, connects, note`.
- Clearing Chrome's site data for the domain wipes it. Export every month or two.
