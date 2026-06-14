# WC26 Shares

A small web app for a World Cup 2026 shares pool. Runs as a static site on
GitHub Pages, installs to the iPhone home screen, and pulls live results
automatically.

## Files

| File | What it is | Do you edit it? |
|------|------------|-----------------|
| `index.html` | Page shell, loads libraries | rarely |
| `app.jsx` | The whole app | only to change features |
| `picks.json` | Who picked which teams | **yes — once, when picks come in** |
| `manifest.webmanifest`, `icon-*.png` | Home-screen install bits | no |

## How results work

On load the app fetches the public-domain
[openfootball](https://github.com/openfootball/worldcup.json) schedule+scores
file and computes everyone's points. If that fetch fails (offline, feed down),
it falls back to the schedule embedded in `app.jsx`, so the app always renders.
Group results, "reached the knockouts" (+1), and knockout rounds are all
derived automatically — no data entry. The **Admin** tab is a manual override,
stored only on your device, for the rare case the feed is wrong or slow.

## Scoring rules

Each player gets 10 shares, max 4 in one team. Team points: group win 1 /
draw 0.5, reaching the knockouts 1, then 2 / 4 / 8 / 16 per knockout round won,
third-place match 8, final 32. Your points from a team = team points × your
shares ÷ total shares held in that team across all players.

## Deploy (one time)

1. Put all these files in the root of your repo and push to `main`.
2. Repo **Settings → Pages → Build and deployment → Source: Deploy from a
   branch**, branch `main`, folder `/ (root)`, **Save**.
3. Wait ~1 minute. Your site is at
   `https://cswavola.github.io/world-cup-shares/`.

## Set the real picks

1. Open the site, go to the **Picks** tab, enter everyone's teams.
2. Tap **Export picks.json**, commit the downloaded file to the repo
   (replacing the starter one).
3. At kickoff of the first match, set `"locked": true` in `picks.json`
   (or use the lock button, then re-export). Locked = no edits, per the rules.

## Editing the app later

`app.jsx` compiles in the browser, so you can edit it right on github.com and
the change is live after the commit — no Mac, no build tools. (To preview
locally you need a local web server, e.g. `python3 -m http.server`, because
browsers block the in-page compiler on `file://`.)
