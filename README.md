# BoxBlayde Shipment Tracker

Internal operations tracker for 214 Central Industries / BoxBlayde inbound shipments across Amazon FBA, J&J Columbus/Las Vegas, and direct vendor flows.

**Live URL:** _(set after first GitHub Pages or Vercel deploy)_

## What this is

A single-file HTML application that shows the current state of every open shipment — origin, vessel, ETA, milestones, tracking links. Updates are pushed by replacing `index.html` and committing.

Editor: Dan Ginsberg (sole editor).
Viewers: 214 Central Industries operations team.

## How it works

- The entire app is in `index.html` — React, ReactDOM, and the JSX are all inlined. No build step, no dependencies, no internet required after first load.
- Shipment data is baked into the HTML at build time as the `SEED` constant.
- The browser stores a working copy in `localStorage` keyed by `bb-shipments-version`. Each new HTML revision bumps the version constant, which triggers an automatic reseed on next page load so viewers always see current state.
- Viewers cannot persist edits beyond their own browser session. Status changes, edits, and deletions only affect their local cache.

## Update workflow

1. New information arrives (email screenshot, supplier note, Seller Central status, Brittan check-in).
2. Dan sends the update to Claude with the relevant context.
3. Claude regenerates `index.html` with refreshed seed data and a new version stamp.
4. Dan downloads the file and commits it to this repo, overwriting `index.html`.
5. GitHub Pages (or Vercel) auto-deploys within ~30 seconds.
6. Viewers refresh their tab and see the new state.

## File layout

```
boxblayde-tracker/
├── index.html       Single-file React app (~215KB self-contained)
├── README.md        This file
└── .gitignore       Standard ignores
```

## Notes

- Repo is private. The deployed URL is public by default — share only with the operations team.
- If anything in the tracker breaks, the previous version is always one `git revert` away.
- For sensitive changes (vendor names, balances, internal pricing), check the new HTML before committing.
