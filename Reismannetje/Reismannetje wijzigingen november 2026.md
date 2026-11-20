---
tags: [reismannetje, geschiedenis]
---
# Reismannetje wijzigingen november 2026

Kort overzicht; details per commit staan in de git-log en in auto-memory (`reismannetje-app.md`). Live = via main, test en rooktest ([[Reismannetje op k3s]]).

| Datum | Wijziging |
|---|---|
| 04-11 | Voor thuis vernieuwd: één scherm zoals een Instagram-DM (verhalen, statuschips, echte chat met thuis via tabel `parent_chat`) |
| 06-11 | Fix voor het foutscherm RM-NET (Leaflet-renderer); valuta-omrekenblok weg |
| 08-11 | Groep verlaten/verwijderen |
| 09-11 | Instapkaart scannen (zxing-wasm, CSP `wasm-unsafe-eval`), automatisch prijsalarm, wereldkaart, reismatch; UI-ronde (tikdoelen 44 px) |
| 11-11 | Echte vluchtroutes (Wikipedia, alleen bestaande routes); schattingen duidelijk gemarkeerd; boeken verbeterd; Ontdekken (lijst) in plaats van Swipen; welkomstpagina voor de Instagram-link; op de telefoon niet meer eerst de kaart; "minder slop" (rustiger teksten) |
| 12-11 | Lanceerplan: `src/geo.js` (Nominatim), Esri als terugvalkaart; tabs Ontdekken/Reis/Sociaal (Plannen weg); geen zijwaarts scrollen op iPhone (velden 16 px); reis samenstellen (vlucht → verblijf) |
| 13-11 | Datumvelden op iPhone; evenementen weg; filters delen; chatbolletje + chat-pop-up; [[Gebruiksanalyse]] |
| 14-11 | Stempels en uitnodiging als instapkaart; "Uit het raam" (welk land/gebergte je overvliegt, `src/overvlieg.js`) + demo; service worker haalt na een melding eerst de nieuwste versie |
| 16-11 | Samen boeken (boekmoment); bugfix voor een eindeloze recursie in `bookCount`; prijzen rustiger opgehaald en "In de buurt" sneller |
| 17-11 | [[Kladblok]] (met delen, Airbnb, vluchten, lokale verhuurders); Groep-pagina eenvoudiger |

Open branches (gepusht, niet gemerged): `claude/plan-b`, `claude/meer-verhuurdata`, `claude/wereldkaart-volledig`, `claude/wereldkaart-popups`.

Zie [[Reismannetje]], [[Reismannetje stijlgeschiedenis]].
