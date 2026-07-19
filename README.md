# Beer Marathon 🍺

An interactive one-page site for the **Beer Marathon** — a 42.3 km run from Hexham to
Walbottle through the Tyne Valley, with a pint at eight pubs along the way
(Saturday 22 August 2026).

Features:
- **Interactive map** (Leaflet + OpenStreetMap/CARTO tiles) showing the real 1108-point
  route with a numbered pin for every pub. Tap a pin for the pub name, leg distance and website.
- **Elevation profile** — an SVG chart of the route's hills (EU-DEM 25 m data) with every
  pub marked on it.
- **"Plan your day" calculator** — set a start time, running pace and time-per-pub, and the
  arrival/departure time for every stop updates live. Warns if you'd arrive before a pub
  opens or finish after sunset. Settings persist (localStorage) and are shareable via URL
  (`?start=10:30&pace=7&pub=20&u=mi`).
- **On-the-day tracking** — a "track me" mode (geolocation) showing your live position on
  the map, distance done/to go, the next pub with ETA, and minutes ahead/behind the plan.
- **GPX download** for watches/phones, **add-to-calendar (.ics)**, a **days-to-go countdown**,
  a **km/mi toggle**, and a print stylesheet that turns the page into a pocket itinerary.
- **Full itinerary** with leg distances, cumulative distance, opening times and links to
  each pub.

Everything is static — no build step, no backend.

## Files
| File | Purpose |
|------|---------|
| `index.html` | The whole page (HTML, CSS, JS). |
| `route.js`   | The route geometry (`window.ROUTE`, 1108 `[lat, lng]` points) and the elevation profile (`window.ELEV`, `[km, m]` pairs). |
| `og-image.png` | 1200×630 social-share card (referenced by the Open Graph tags). |

## View it locally
Because `index.html` loads `route.js`, open it through a tiny web server rather than
double-clicking (some browsers block `file://` script loads):

```bash
cd beer-marathon
python -m http.server 8000
# then open http://localhost:8000
```

## Deploy to GitHub Pages (new repo)

1. **Create a new, empty repo** on GitHub (e.g. `beer-marathon`) — no README/licence,
   so it starts empty.
2. **Push these files** from this folder:
   ```bash
   cd beer-marathon
   git init
   git add .
   git commit -m "Beer Marathon route page"
   git branch -M main
   git remote add origin https://github.com/<your-username>/beer-marathon.git
   git push -u origin main
   ```
   *(A local repo with this commit is already initialised for you — you can skip
   `git init`/`git add`/`git commit` and go straight to adding the remote and pushing.)*
3. **Turn on Pages:** repo **Settings → Pages → Build and deployment → Source: “Deploy
   from a branch”**, branch **`main`**, folder **`/ (root)`**, then **Save**.
4. Wait ~1 minute. Your site will be live at
   **`https://<your-username>.github.io/beer-marathon/`**.

## Editing
- **Pub details / distances / date:** edit the `STOPS` array and the hero section near the
  top of `index.html`.
- **Default pace or start time:** change the `value=` attributes on the planner inputs in
  `index.html`.
- **Route line:** replace `window.ROUTE` in `route.js` (each point is `[latitude, longitude]`).
  If you do, regenerate `window.ELEV` too (sample the new route every ~150 m and look up
  elevations, e.g. via opentopodata.org) — or delete it, and the elevation chart hides itself.
- **Opening hours / sunset:** the `opens` values in the `STOPS` array (minutes from midnight)
  and `SUNSET_MIN` in `index.html`. Hours marked `unconf: true` show an asterisk on the page.

---
Route data from [plotaroute.com/route/3353839](https://www.plotaroute.com/route/3353839?units=km).
Map © OpenStreetMap contributors, tiles © CARTO.
