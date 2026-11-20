---
tags: [reismannetje, code]
---
# Reismannetje architectuur

> [!note] Sinds 2026-10-31
> Runtime: k3s-Deployment (Recreate, uid 1000, read-only, NetworkPolicy) achter Docker-Traefik. → [[Reismannetje op k3s]]

```mermaid
flowchart TB
  subgraph Browser
    APP["/js/app.js (gebundeld uit public/js/app/*.js)"]
    SW[service worker /sw.js]
    ML[MapLibre + Leaflet]
  end
  T[Traefik reismannetje.nl] --> E
  subgraph Container reismannetje
    E[Express server.js] --> API[routes/api.js]
    E --> SOC[routes/social.js]
    E --> SH[routes/share.js]
    E --> G[routes/gids.js]
    E --> LV[live.js SSE]
    API & SOC --> DB[(SQLite reismannetje.db)]
    API --> NB[nearby.js] & PR[prices.js] & LI[linkinfo.js] & DR[drive.js]
    SOC --> PU[push.js]
    E --> TK[tickets.js] & PA[prijsalarm.js] & AF[affiliate.js]
  end
  APP --> T
  NB --> OSM[(Nominatim/Photon/Overpass)]
  PR --> AB[(Airbnb / Travelpayouts)]
  DR --> OSRM[(OSRM)]
  ML --> OFM[(OpenFreeMap)]
```

- **Eén proces**, geen build-stap: `src/bundle.js` plakt de front-endbestanden aan elkaar tot één IIFE op `/js/app.js`.
- **Multi-tenant per groep**: elke API-call heeft header `X-Team`; alle tabellen hebben `team_id` → [[Groepen en chat]].
- **Realtime**: Server-Sent Events (`/api/live`) + polling-fallback → [[Planavond]].
- **Caches in SQLite**: prijzen 12 u, vluchten 6 u, plekken in de buurt 14 d, rijtijden 60 d.

Zie [[Reismannetje backend]], [[Reismannetje frontend]], [[Reismannetje database]], [[Externe diensten (Reismannetje)]].
