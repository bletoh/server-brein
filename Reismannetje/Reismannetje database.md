---
tags: [reismannetje, code, database]
---
# Reismannetje database

SQLite `reismannetje.db` in volume `reismannetje_data` (`/app/data`). Schema wordt bij elke start aangemaakt/bijgewerkt (`CREATE TABLE IF NOT EXISTS` in `db.js`).

| Groep | Tabellen |
|---|---|
| Accounts | `users`, `sessions` (sha256-token), `password_resets` |
| Groepen | `teams`, `team_members`, `team_settings`, `messages` → [[Groepen en chat]] |
| Kaart/inhoud | `sections` (tabs/soorten), `items` (pinnen, vluchten, verblijven, activiteiten, eten, auto) |
| Reizen | `trips`, `trip_picks`, `trip_stops` ([[Rondreis]]), `trip_todos`, `trip_plan`, `trip_rsvp`, `trip_expenses` ([[Wie betaalt wat]]), `trip_docs` ([[Tickets en prijsalarm]]), `trip_bundles`, `trip_bundle_trips` |
| Beslissen | `polls`, `poll_options`, `poll_votes`, `available_days` → [[Datumprikker en stemronde]] |
| Swipen | `dest_reactions`, `dest_matches` → [[Ideeën en swipen]] |
| Overig | `settings`, `price_cache`, `drive_cache`, `push_subs`, `flight_watches`, `outbound_clicks` |

Bestanden naast de DB: `uploads/` (publiek, foto's), `docs/` (tickets, mode 600, niet publiek), `vapid.json`, `.last-backup`.

Backups vóór grote migraties staan los in [[srv-backups]] (`reismannetje-voor-*.db`). Nachtelijks: [[reismannetje-backup.sh]].
