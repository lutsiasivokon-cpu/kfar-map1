# Kfar Hasidim interactive map

React + Vite + Leaflet + OpenStreetMap. Real building footprints from Overpass, clickable buildings,
geolocation, search/filters, editing, GeoJSON import/export. Hebrew (RTL), Russian, English.

## Run
```
npm install
npm run probe     # Stage 0: what does OSM really contain for Kfar Hasidim? (needs internet)
npm run dev       # http://localhost:5173  (geolocation works on localhost and HTTPS)
npm run build     # production build in dist/
```

## First thing to do
1. `npm run probe` -> prints places named Kfar Hasidim, building counts and a suggested bbox.
2. Put the real bbox into `src/data/config.js` (`BBOX`). The coordinates there now are PROVISIONAL.
3. `npm run dev` and check that buildings appear. Missing ones: use "Add building".

## Rules followed
- No invented geometry, names or numbers. Empty until typed by a person.
- Overpass data is cached locally (7 days) and is not a production database; export GeoJSON to back up.
- OSM relations (multipolygon buildings) are skipped, not guessed.
- Location is never sent anywhere; requested once on start, `watchPosition` cleaned up on unmount.
- Endpoints are configurable: `VITE_OVERPASS_URL`, `VITE_TILE_URL` (use your own tile provider for heavy traffic).

## Structure
`src/components/{Map,Building,Search,Filters,Location}`, `src/services/{overpass,geolocation}.js`,
`src/data` (config, i18n), `src/utils`. Edits/manual objects live in localStorage
(`kh-edits`, `kh-manual`); `storage.js` is the single place to swap for Supabase later.

## Status
Written but NOT yet run: no network/npm in the authoring environment. Expect small fixes on first run.
