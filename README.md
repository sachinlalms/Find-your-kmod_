# IBM MQ RDQM kmod Finder

A static page that helps you find the right `kmod-drbd` package for a given
Linux kernel version + IBM MQ version, using IBM's public RDQM compatibility file.

## How it works

Browsers won't let JavaScript on this site fetch IBM's JSON file directly
(IBM's server doesn't send the CORS headers that would allow it — that's true
for any website, not just this one). So instead of fighting that from the
visitor's browser, a scheduled **GitHub Action** downloads the file server-side
(where CORS doesn't apply) and commits it into this repo at
`data/ibm-mq-rdqm-kmods.json`. The page then simply fetches that local file —
same origin, no CORS, no proxies, no manual copy/paste for visitors.

## One-time setup after you fork/clone this

1. Push this repo to GitHub.
2. Enable **GitHub Pages** for it: Settings → Pages → Deploy from branch → `main` / root.
3. Go to the **Actions** tab and run **"Update IBM MQ RDQM kmod data"** once manually
   (workflow_dispatch) so `data/ibm-mq-rdqm-kmods.json` gets populated for the first time.
   After that it refreshes automatically once a day.
4. Visit your Pages URL — the finder should now show real data.

## Files

- `index.html` — the site itself.
- `data/ibm-mq-rdqm-kmods.json` — mirrored copy of IBM's file, refreshed daily.
- `.github/workflows/update-data.yml` — the scheduled job that keeps it fresh.

## Attribution

This is an independent tool, not affiliated with or endorsed by IBM. The
underlying compatibility data belongs to IBM — see the notices embedded in
the mirrored JSON file.
