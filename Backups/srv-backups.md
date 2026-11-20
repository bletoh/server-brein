---
tags: [backup]
map: /srv/backups
---
# /srv/backups

> [!note] Sinds 2026-10-31
> Nieuw: `/srv/backups/k3s/` (dagelijks) en het eenmalige archief `archief-voor-k3s-20261031.tar.gz`. → [[k3s-onderhoud]]

Lokale backups op de VPS (root, 700).

| Map | Grootte (±) | Van |
|---|---|---|
| `bedrock/` | 900 MB | [[app-backups.sh]] |
| `netbird/`, `calibre-web/`, `reismannetje/`, `kleine-apps/`, `crowdsec/`, `traefik/`, `n8n/`, `server/` | 1–80 MB | nachtelijke scripts |
| `voor-herindeling-20261003/` | 39 MB | alle oude configs van vóór de verhuizing naar `/srv` |
| `reismannetje-voor-*.db` | 2–4 MB | vóór migraties ([[Reismannetje ontwikkelworkflow]]) |
| `*-voor-*` / `*.voor-*` | klein | config-kopieën vóór elke wijziging (traefik, netbird-services, compose, scripts, dns) |

Conventie: vóór een wijziging een kopie `<naam>.voor-<wat>-<datum>` maken. Zie [[Backup-strategie]].
