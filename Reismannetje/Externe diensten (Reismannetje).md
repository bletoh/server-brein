---
tags: [reismannetje, extern]
---
# Externe diensten (Reismannetje)

| Dienst | Waarvoor | Opmerking |
|---|---|---|
| OpenFreeMap | vectortegels | gratis, ook commercieel → [[Kaart (MapLibre)]] |
| OpenStreetMap-rastertegels | fallback | |
| Esri World Imagery | satelliet | |
| Nominatim / Photon | zoeken, plaatsnamen, hotels/eten | geen sleutel |
| Overpass | activiteiten, extra hotelinfo | vaak 429/504, niet afhankelijk van maken |
| OSRM (router.project-osrm.org) | rijtijden naar vliegvelden | 1 req/s, cache 60 d |
| Airbnb zoekpagina | echte verblijfsprijzen (scrapen) | cache 12 u, max 2 tegelijk |
| Travelpayouts (Aviasales) | vluchtprijzen | token in `.env`, cache 6 u → [[Tickets en prijsalarm]] |
| Wikimedia Commons | bestemmingsfoto's | handmatig gekozen |
| Pushdiensten (Google/Apple/Mozilla/Microsoft) | Web Push | → [[PWA en push]] |
| SMTP | wachtwoord vergeten | nog niet ingesteld |

Booking.com geeft een botcheck; alleen de naam wordt uit de URL gehaald. Zie [[Reismannetje backend]].
