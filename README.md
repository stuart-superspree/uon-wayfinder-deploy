# UoN Wayfinder

A mobile web app that helps people navigate the University of Nottingham — covering both University Park and Jubilee Campus, with inter-campus shuttle routing. Powered by Superspree RouteLoop.

Built to the Superspree Wayfinding Standard v3: single-file HTML/CSS/JS, Nunito throughout, NFC RouteLoop deep-link support, dark mode, accessibility toggles, route summaries, and detailed feedback wired to the team.

## What's in this repo

```
├── public/
│   └── index.html        ← the app (single file, no build step)
├── package.json          ← Node manifest + start script
├── railway.json          ← Railway deployment config
└── .gitignore
```

The app is a single self-contained HTML file. The Node setup exists only to serve it — there's no backend, no API, no database, no build pipeline.

## Run locally

You need Node 18+.

```bash
npm install
npm start
```

Then open http://localhost:3000.

To use a different port: `PORT=8080 npm start`.

## Deploy to Railway

1. Push this repo to GitHub.
2. In Railway, click **New Project → Deploy from GitHub repo** and pick this one.
3. Railway auto-detects the Node project, runs `npm install`, then `npm start`. The included `railway.json` pins this behaviour so future Railway changes can't break it.
4. Once the build is green, click **Settings → Networking → Generate Domain** to get a public URL.

That's it — no environment variables required, no secrets, no build hooks.

### Custom domain

In Railway: **Settings → Networking → Custom Domain**. Add a CNAME at your DNS provider pointing to the value Railway shows.

## Deep links

The app accepts `?tag=<routeloop-id>` to set the user's starting location, simulating an NFC tap. Example:

```
https://your-domain.example.com/?tag=upk-trent
```

Valid tag IDs are listed in `NFC_TAGS` inside the HTML. Current deployment has 14 RouteLoops across both campuses.

## Feedback

The "Report" / "Send feedback" button composes a `mailto:laura@superspree.com` link with the user's full route context (starting RouteLoop, destination, step number, settings, timestamp) and opens the device's email app to send. Change the recipient by editing the `FEEDBACK_EMAIL` constant near the bottom of `public/index.html`.

## Updating the app

The whole app is in `public/index.html`. Edit it directly, commit, push — Railway redeploys automatically.
