---
tags: [server, docker, opslag]
---
# Docker-volumes

> [!note] Sinds 2026-10-31
> `reismannetje_data` en het oude `vakantieplanner_vakantie_data` zijn weg (gearchiveerd in `/srv/backups/archief-voor-k3s-20261031.tar.gz`); de data staat nu in `/srv/k8s/reismannetje/data`. → [[Reismannetje op k3s]]

| Volume | Inhoud | App | Backup |
|---|---|---|---|
| `traefik_traefik_certs` | `acme.json` (Let's Encrypt) | [[Traefik]] | [[app-backups.sh]] (traefik) |
| `netbird_netbird_data` | `store.db`, `idp.db`, `events.db`, GeoLite | [[NetBird]] | [[app-backups.sh]] (netbird) |
| `netbird_netbird_proxy_certs` | certificaten `*.proxy`/eigen domeinen | [[NetBird reverse proxy]] | [[app-backups.sh]] |
| `crowdsec_crowdsec_data` / `_config` | beslissingen-db, config, bouncer-keys | [[CrowdSec]] | [[app-backups.sh]] |
| `reismannetje_data` | `reismannetje.db` (SQLite), `uploads/`, `docs/` (tickets), `vapid.json` | [[Reismannetje]] | [[reismannetje-backup.sh]] |
| `vakantieplanner_vakantie_data` | oud volume van vóór de hernoeming | [[Reismannetje]] | — (mag later weg) |
| `netbird_netbird_traefik_letsencrypt` | restant | — | — |

Bind-mounts (geen volume): n8n `./data` + `./postgres-data`, Calibre `./config` + `./books`, kaart `./www`. Fysiek: `/var/lib/docker/volumes/<naam>/_data`.
