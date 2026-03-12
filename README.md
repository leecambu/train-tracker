# GO Train Tracker

A lightweight, single-file web app that detects your location and shows the next 5 GO Transit departures from whichever station you're closest to — Whitby GO or Union Station.

## How it works

1. **Location detection** — uses the browser's Geolocation API to get your current position
2. **Station comparison** — calculates the distance (via Haversine formula) to both Whitby GO Station and Union Station GO
3. **Smart direction** — if you're closer to Whitby GO, it shows trains heading west towards Union Station; if you're closer to Union Station, it shows trains heading east towards Whitby GO
4. **Next 5 departures** — lists the upcoming trains with departure times and live countdowns
5. **Manual fallback** — if location access is unavailable, you can manually select your station

## Stations covered

| Station | Line | Coordinates |
|---|---|---|
| Whitby GO | Lakeshore East | 43.8731° N, 78.9426° W |
| Union Station | Lakeshore East | 43.6453° N, 79.3806° W |

## Schedule data

Times are based on published GO Transit Lakeshore East timetables and are embedded directly in the HTML. The app uses separate weekday and weekend schedules. **Times may not reflect real-time delays, service changes, or seasonal schedule updates** — always verify at [gotransit.com](https://www.gotransit.com).

## Running locally

No build step or dependencies required. Open `index.html` directly in a browser, or serve it with any local server:

```bash
# VS Code Live Server, Python, npx serve, etc.
python3 -m http.server 8000
```

> **Note:** Geolocation requires a secure context. For best results, access the page over HTTPS (e.g. via GitHub Pages) rather than `127.0.0.1`. The manual station picker works without location access.

## Deployment

The app is a single self-contained `index.html` file with no external dependencies. It can be hosted anywhere static files are served — GitHub Pages is recommended.

```bash
git init
git add index.html
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/go-tracker.git
git push -u origin main
```

Then enable GitHub Pages in the repo settings (Source: `main` branch). Your app will be live at `https://YOUR_USERNAME.github.io/go-tracker/`.
