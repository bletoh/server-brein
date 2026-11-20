---
tags: [reismannetje, functie]
---
# Kladblok

Sinds 2026-11-17. De eigenaar vond de app te ingewikkeld en wilde een plek om links en een ruwe opzet te verzamelen tijdens het brainstormen. Het kladblok hoort **bij de groep**, niet bij een reis.

- **Backend:** `src/kladblok.js`, tabel `kladblok` ([[Reismannetje database]]).
- **Plekherkenning** (aan de clientkant, uit `bestemmingen.json`): weergave "Per plek", met een knop om de reis te kiezen.
- **Delen:** openbare alleen-lezen pagina `/kladblok/<code>` (ook `?plek=Porto`), code in `team_settings.kladblok_deel` ([[Deelpagina's en bestemmingsgids]]).
- **Airbnb:** prijs van één woning via `prices.stayPrice` (de zoekpagina rond de coördinaten van de woning; niet gevonden = niet beschikbaar).
- **Vluchten:** kolom `vlucht`, `GET /api/kladblok/vluchten` (luchthavens binnen 150 km van de bestemming).
- **Lokale verhuurders:** `public/data/verhuurders.json`, 127 sites bij 64 plekken (alleen vakantieverhuur). Grote platforms (Booking, Vrbo, Expedia en dergelijke) blokkeren gewone opvragingen; dat wordt bewust **niet** omzeild.
- Branch `claude/meer-verhuurdata` (meer info uit links halen) is gepusht maar niet gemerged.

Rond dezelfde tijd is de Groep-pagina vereenvoudigd: alleen naam, uitnodigingslink (delen/kopiëren/QR), leden en verlaten. Voorkeuren en reisprofiel staan nu onder Instellingen.

Zie [[Reismannetje]], [[Groepen en chat]].
