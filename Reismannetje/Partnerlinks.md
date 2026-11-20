---
tags: [reismannetje, functie, inkomsten]
---
# Partnerlinks

`src/affiliate.js`: externe links (Booking, Aviasales, DiscoverCars, GetYourGuide, Skyscanner, Airbnb, Kayak) lopen bij een klik via `/go?u=`, dat de partnercode uit `.env` toevoegt (`BOOKING_AID`, `TRAVELPAYOUTS_MARKER`, `DISCOVERCARS_AID`, `GETYOURGUIDE_PARTNER_ID`) en kliks per dag/partner telt (`outbound_clicks`, geen gebruikersdata).

- Rapport: `sudo docker exec reismannetje node scripts/kliks.js 30`.
- Codes nog niet ingevuld; advies (2026-10-22): eerst codes + Search Console, display-advertenties pas later en alleen op publieke `/bestemming`-pagina's.

Zie [[Deelpagina's en bestemmingsgids]].
