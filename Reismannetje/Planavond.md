---
tags: [reismannetje, functie]
---
# Planavond

(2026-10-23) Groot scherm voor aan tafel (tv/laptop), route `#planavond`.
- QR-code om mee te doen (eigen SVG via `qrcode-generator`), wie er online is, open stemronde met balken, swipe-top met foto's en matches, reizen in de rechterkolom, feed.
- **Live**: `src/live.js` = Server-Sent Events op `/api/live` (heartbeat 25 s, max 8 per gebruiker); na elke wijziging een `change`-event. `Content-Encoding: identity`, anders houdt de compress-middleware van [[Traefik]] de events vast.
- Telefoons krijgen een balkje bovenaan als er een planavond loopt.
- Demo-video's: [[Reismannetje demo-video's]].

Code `11-planavond.js`, test `test/planavond.test.js`.
