# Beer Marathon 🍺

An interactive one-page site for the **Beer Marathon** — a 42.2 km run from Hexham to
Walbottle through the Tyne Valley, with a pint at eight pubs along the way
(Saturday 22 August 2026).

Features:
- **Interactive map** (Leaflet + OpenStreetMap/CARTO tiles) showing the real 1108-point
  route with a numbered pin for every pub. Tap a pin for the pub name, leg distance and website.
- **"Plan your day" calculator** — set a start time, running pace and time-per-pub, and the
  arrival/departure time for every stop updates live.
- **Full itinerary** with leg distances, cumulative distance and links to each pub.

Everything is static — no build step, no backend.

## Files
| File | Purpose |
|------|---------|
| `index.html` | The whole page (HTML, CSS, JS). |
| `route.js`   | The route geometry (`window.ROUTE`, 1108 `[lat, lng]` points). |

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
- **Route line:** replace `route.js` (each point is `[latitude, longitude]`).

---
Route data from [plotaroute.com/route/3353839](https://www.plotaroute.com/route/3353839?units=km).
Map © OpenStreetMap contributors, tiles © CARTO.
