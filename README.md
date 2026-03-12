# GO Train Tracker

A lightweight, single-file web app that shows the next 5 GO Transit departures for your commute — across all 7 GO rail lines. Set your route once, and the app uses GPS to automatically detect which end of your commute you're at and shows trains in the right direction.

---

## Features

- **All 7 GO rail lines** — Barrie, Kitchener, Lakeshore East, Lakeshore West, Milton, Richmond Hill, Stouffville
- **Smart GPS detection** — detects whether you're at your home station or destination and flips direction automatically
- **4 schedule types** — Weekday, Friday (extended service), Saturday, Sunday
- **Personalised setup** — saved to your browser so it's instant on every return visit
- **Manual fallback** — if location is denied, tap which station you're at
- **No dependencies** — single `index.html` file, no build step, works offline after first load

---

## How it works

### First visit — 3-step setup

1. **Select your line** — choose from all 7 GO rail lines, shown with their official line colours
2. **Select your home station** — the station you usually board at
3. **Select your destination** — where you're heading (typically Union Station, but any stop works)

Your route is saved to `localStorage` and never asked again.

### Return visits — automatic

1. The app requests your GPS location
2. It calculates the distance to both your saved stations (using the Haversine formula)
3. **If you're closer to your home station** → shows trains towards your destination
4. **If you're closer to your destination** → automatically flips and shows trains back home

No tapping required — it just knows which way you're going.

---

## Lines & stations covered

Schedule data is sourced from the official **GO Transit GTFS feed** (updated March 2026).

| Line | Terminus | Stops |
|------|----------|-------|
| Barrie | Allandale Waterfront GO ↔ Union | 11 |
| Kitchener | Kitchener GO ↔ Union | 13 |
| Lakeshore East | Durham College Oshawa GO ↔ Union | 10 |
| Lakeshore West | Confederation GO (Hamilton) ↔ Union | 13 |
| Milton | Milton GO ↔ Union | 9 |
| Richmond Hill | Bloomington GO ↔ Union | 7 |
| Stouffville | Old Elm GO ↔ Union | 10 |

> **Note:** Milton and Richmond Hill run weekday service only. The app shows a "no service" message on weekends for those lines.

---

## Schedule data

Times are embedded directly in the HTML from the GO Transit GTFS static feed. The app uses four schedule types:

| Type | Days |
|------|------|
| Weekday | Monday – Thursday |
| Friday | Friday (extended late service) |
| Saturday | Saturday |
| Sunday | Sunday |

**Times may not reflect real-time delays, cancellations, or service changes.** Always verify at [gotransit.com](https://www.gotransit.com).

---

## Running locally

No build step or dependencies required. Open `index.html` in a browser, or serve it locally:

```bash
python3 -m http.server 8000
```

> **Note:** Geolocation requires a secure context (HTTPS). For GPS to work, access the app over HTTPS — e.g. via GitHub Pages. The manual station toggle works without location access.

---

## Deployment

The app is a single self-contained `index.html` file. Host it anywhere static files are served.

**GitHub Pages (recommended):**

```bash
git add index.html README.md
git commit -m "Deploy GO Train Tracker"
git remote add origin https://github.com/YOUR_USERNAME/go-tracker.git
git push -u origin main
```

Enable GitHub Pages in the repo settings (Source: `main` branch). Your app will be live at:

```
https://YOUR_USERNAME.github.io/go-tracker/
```

---

## Add to iPhone home screen (PWA)

The app can be added to your iPhone home screen and used like a native app:

1. Open the app URL in **Safari** (must be Safari, not Chrome)
2. Tap the **Share** button (box with arrow pointing up)
3. Tap **"Add to Home Screen"**
4. Give it a name and tap **Add**

It will appear on your home screen as a standalone app icon and open full-screen without the browser UI.

> **Tip:** For the best experience — including GPS working reliably — the app should be hosted over HTTPS (e.g. GitHub Pages).
