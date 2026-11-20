---
tags: [netwerk, proxy, beveiliging]
---
# NetBird reverse proxy

> [!note] Sinds 2026-10-31
> Het doel van service `mc` is via de API veranderd van `bedrock-map:80` naar `10.43.100.50:80` (k3s). → [[Minecraft op k3s]]

Container `netbird-proxy` (`netbirdio/reverse-proxy`) in de [[NetBird]]-stack. Publiceert interne apps op internet **met** NetBird-SSO, landenfilter en [[CrowdSec]].

- Domein `proxy.benjaminhashi.nl` + eigen domeinen (`*.benjaminhashi.nl` geregistreerd/gevalideerd). Config `proxy.env` (token, PRIVATE=true, WG-poort 51821/udp).
- [[Traefik]] stuurt het verkeer via **TLS-passthrough + PROXY protocol v2** door (TCP-router `netbird-proxy`).
- Services worden beheerd in het NetBird-dashboard of via [[nb-api]] (target_type `cluster` = direct upstream vanuit de proxycontainer).

## Services
| Service | Domein | Upstream | Toegang |
|---|---|---|---|
| books | [[books.benjaminhashi.nl]] | `calibre-web:8083` | publiek + geo |
| n8n | [[n8n.benjaminhashi.nl]] | `n8n:5678` | publiek + geo |
| monitor | [[monitor.benjaminhashi.nl]] | `nb-monit:3001` | SSO (`beheerders`), geen geo meer |
| bsm | [[bsm.benjaminhashi.nl]] | `host.docker.internal:11325` | SSO + geo |
| nas | [[nas.benjaminhashi.nl]] | peer BACKUPNAS:5000 | SSO + geo |
| mc | [[mc.benjaminhashi.nl]] | `bedrock-map:80` | publiek + geo |

Alle services: `crowdsec enforce`, `pass_host_header`. Proxy-accesslog via `GET /api/events/proxy`.

## Valkuilen
- `allowed_countries` max 50 landen per service.
- `allowed_cidrs` is een **extra** allowlist (AND), geen uitzondering → bij mc ging de site voor iedereen plat. Zie [[Geo-blokkade]].
