---
tags: [reismannetje, analyse]
---
# Gebruiksanalyse (2026-11-13)

Gemaakt op verzoek ("welke onderdelen worden het minst gebruikt"), zodat de app kan worden ingekort tot wat mensen echt gebruiken. **Tel opnieuw voordat een functie weggaat**; de eigenaar beslist.

## Methode (alleen lezen)
- Database: `sudo sqlite3 -readonly /srv/k8s/reismannetje/data/reismannetje.db ".backup <scratch>/rm.db"` (de map is alleen voor root), daarna rijen en datums per tabel tellen.
- Traefik JSON-accesslog (`/srv/docker/traefik/logs`, gz per dag): filteren op `RequestHost` reismannetje.nl en API-paden per IP per dag tellen. Er staat geen gebruikers-id in, dus IP is maar een ruwe benadering.

## Uitkomst
Ongeveer 10 gebruikers, waarvan een paar testaccounts.
- **(Bijna) nooit gebruikt:** polls/stemmen, kosten/bonnen/IBAN, to-do's, alles in `samen.js` (album, bingo, check-in, locatie delen, playlist, slots), handmatig prijsalarm, passkeys, agenda-abonnement, herinneringen, wereldkaart, reismatch, evenementen, DM's/likes, deelpagina's `/reis /reizen /stem /join`, tickets/documenten, bundels/stops. In de groepschat staat sinds 31-10 alleen nog systeemberichten.
- **Wel gebruikt:** Ontdekken (reistijd, prijzen, luchthavens in de buurt, reacties op bestemmingen), Voor thuis, sociale tijdlijn/zoeken, mijn voorkeuren.

Daarna weggehaald: evenementen (2026-11-13). Zie [[Reismannetje wijzigingen november 2026]].
