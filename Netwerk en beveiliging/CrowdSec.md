---
tags: [beveiliging, docker]
map: /srv/docker/crowdsec
---
# CrowdSec

Inbraakdetectie + community-blocklist (sinds 2026-10-12).

- Container `crowdsec` op `books-net`, leest `/srv/docker/traefik/logs/access.log` (`acquis.yaml`).
- Collections: `traefik`, `http-cve`, `base-http-scenarios`, `appsec-virtual-patching`.
- **Bouncers** (keys in `.env`): de Traefik-plugin (middleware `crowdsec` in `site-default`, zie [[Traefik]]) en de [[NetBird reverse proxy]] (`supports_crowdsec=true`, per service "enforce").
- Passthrough-sites komen niet in de Traefik-log → daar beschermt vooral de blocklist via de proxy.

## Whitelist Ghost-admin (weggehaald 2026-10-26 met de blog)
Inloggen op `/ghost/` triggerde `http-admin-interface-probing` en bande het thuis-IP van de eigenaar 4 uur op **alle** sites (2026-10-17 en 2026-10-20). Fix: `ghost-whitelist.yaml` (parser `s02-enrich`) whitelist `benjaminhashi.nl` + pad `/ghost/`. Zie [[Blog (Ghost)]].

## Handig
```bash
sudo docker exec crowdsec cscli decisions list
sudo docker exec crowdsec cscli decisions delete --ip <ip>     # unban
sudo docker exec crowdsec cscli explain --type traefik --log '<regel>'
```
Backup: [[app-backups.sh]] (crowdsec). Zie [[Valkuilen en lessen]].
