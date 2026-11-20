---
tags: [reismannetje, functie]
---
# Tickets en prijsalarm

**Tickets** (2026-10-23, `src/tickets.js`, `08-tickets.js`): boardingpasses/boekingen per reis uploaden (jpg/png/webp/heic/pdf, max 15 MB, 60 per reis). Opslag in `DATA_DIR/docs` (mode 600, **niet** publiek), te bekijken via `/tickets/:id` met cookie + lidmaatschapscheck. Offline beschikbaar via de service-worker-cache `rm-tickets`. Zit in [[reismannetje-backup.sh]].

**Prijsalarm** (`src/prijsalarm.js`): volg een vlucht (AMS → XXX); elke 30 min worden volgers gecheckt die 6 uur niet bekeken zijn. Bij ≥ €5 en 3% goedkoper: push + chatbericht. Tabel `flight_watches`. Prijzen via Travelpayouts ([[Externe diensten (Reismannetje)]]).

Zie [[PWA en push]], [[Reisvenster en reisstand]].
