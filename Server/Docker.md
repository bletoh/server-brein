---
tags: [server, docker]
---
# Docker

Alle web-apps draaien als Docker Compose-project onder `/srv/docker/<app>` (zie [[Mappenstructuur]]). Elke `compose.yml` heeft een vaste `name:`, zodat containers en volumes hun oude namen houden (bijv. `ebooks` voor Calibre-web, `downloader` voor Shelfmark).

## Containers (stand 2026-10-31)

> [!note] Sinds 2026-10-31 draaien Reismannetje en alles rond Minecraft niet meer in Docker maar in [[Kubernetes (k3s)]]. Docker blijft voor de onderstaande apps en voor het bouwen van images.

| Container | Image | Project | Netwerken | Notitie |
|---|---|---|---|---|
| traefik | traefik:v3 (3.7) | traefik | books-net, web, downloader_default | [[Traefik]] |
| crowdsec | crowdsecurity/crowdsec | crowdsec | books-net | [[CrowdSec]] |
| netbird-server | netbirdio/netbird-server | netbird | netbird, books-net | [[NetBird]] |
| netbird-dashboard | netbirdio/dashboard | netbird | netbird, books-net | [[NetBird]] |
| netbird-proxy | netbirdio/reverse-proxy | netbird | netbird, books-net, web | [[NetBird reverse proxy]] |
| n8n-n8n-1 | n8nio/n8n (2.43) | n8n | books-net, web | [[n8n]] |
| n8n-postgres-1 | postgres:16 | n8n | books-net | [[n8n]] |
| calibre-web | linuxserver/calibre-web | ebooks | books-net | [[Calibre-web]] |
| nb-monit | eigen build (node:24-alpine) | nb-monit | web | [[nb-monit]] |
| loadmon | python:3.12-alpine | loadmon | geen (meter) | [[Grafana]] |
| grafana | grafana/grafana | grafana | books-net, monitoring | [[Grafana]] |
| prometheus | prom/prometheus | grafana | monitoring | [[Grafana]] |
| node-exporter | prom/node-exporter | grafana | host | [[Grafana]] |
| cadvisor | ghcr.io/google/cadvisor | grafana | monitoring | [[Grafana]] |
| *(shelfmark)* | calibrain/shelfmark | downloader | — | [[Shelfmark]] (staat uit) |

Naar k3s verhuisd: reismannetje → [[Reismannetje op k3s]]; bedrock-map, bedrock-map-api, vriendenpaneel, mcxboxbroadcast → [[Minecraft op k3s]].

Tijdelijk zie je soms een `mcr.microsoft.com/playwright`-container (`--network host`): dat is een testbrowser van Claude, zie [[Playwright-testen]].

## Netwerken en opslag
- [[Docker-netwerken]] — vooral `books-net` en `web` (extern, gedeeld tussen projecten)
- [[Docker-volumes]] — certificaten, databases

## Beheer
```bash
cd /srv/docker/<app>
sudo docker compose up -d                      # starten / wijzigingen toepassen
sudo docker compose pull && sudo docker compose up -d
sudo docker compose logs -f
```
- Wekelijks `pull`/`build --pull`/`up -d` door [[weekly-update.sh]]; elk uur gecontroleerd door [[ensure-apps-up.sh]]. Voor k3s: [[k3s-onderhoud]].
- Let op `$` in `.env`: Compose interpoleert het → enkele quotes. Zie [[Valkuilen en lessen]].
- Gebruiker `almalinux` zit niet in de `docker`-groep: altijd `sudo docker`.
