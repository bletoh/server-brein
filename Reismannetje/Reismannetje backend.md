---
tags: [reismannetje, code]
map: /srv/docker/reismannetje/src
---
# Reismannetje backend (`src/`)

| Bestand | Regels | Rol |
|---|---|---|
| `server.js` | 107 | Express-app, security headers/CSP, compression, statics (`/vendor/*`), routes koppelen |
| `db.js` | 436 | SQLite-schema (CREATE IF NOT EXISTS bij start), migraties (o.a. hernoemen vakantieplanner.db), helpers |
| `auth.js` | 128 | accounts (scrypt), sessies (cookie `vp_sid`, sha256 in DB), inlogrem |
| `routes/api.js` | 768 | kern-API: secties, items, reizen, polls, datumprikker, uploads, prijzen → [[Reismannetje API]] |
| `routes/social.js` | 439 | teams, uitnodigen, chat, reacties/swipes, chat-opruimen → [[Groepen en chat]] |
| `routes/share.js` | 770 | publieke deelpagina's `/reis`, `/reizen`, `/stem`, OG-plaatjes → [[Deelpagina's en bestemmingsgids]] |
| `routes/gids.js` | 338 | `/bestemmingen`, sitemap, robots, JSON-LD |
| `live.js` | 93 | SSE `/api/live` → [[Planavond]] |
| `push.js` | 103 | Web Push (VAPID) → [[PWA en push]] |
| `tickets.js` | 156 | tickets/boekingen per reis → [[Tickets en prijsalarm]] |
| `prijsalarm.js` | 128 | vluchtprijzen bewaken |
| `kosten.js` | 60 | verdeling uitgaven → [[Wie betaalt wat]] |
| `affiliate.js` | 69 | `/go?u=` partnerlinks → [[Partnerlinks]] |
| `prices.js` | 189 | Airbnb-zoekpagina scrapen, Travelpayouts-vluchten |
| `nearby.js` | 188 | hotels/eten/activiteiten via Photon + Overpass |
| `linkinfo.js` | 251 | URL plakken → og/JSON-LD ophalen (SSRF-veilig) |
| `drive.js` | 63 | rijtijden naar vliegvelden (OSRM) |
| `mail.js` | 35 | wachtwoord-reset via SMTP (nog niet ingesteld) |
| `bundle.js`, `sw.js`, `service-worker.js` | | bundel + service worker met versie-hash |
| `airports.json` | | vaste lijst vliegvelden (OurAirports) |

Scripts: `scripts/check-app.js` (syntaxcheck bundel), `iconen.js` (PNG/ICO via sharp), `kliks.js` (partnerklikrapport), `vliegvelden.js`, `reis-turkije.js` (voorbeeldreis).
