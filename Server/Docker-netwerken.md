---
tags: [server, docker, netwerk]
---
# Docker-netwerken

| Netwerk | Subnet | Wie zit erop | Waarom |
|---|---|---|---|
| `books-net` | 172.19.0.0/16 | traefik, crowdsec, netbird-*, n8n + postgres, calibre-web, bedrock-map(+api), vriendenpaneel | Hoofdnetwerk: [[Traefik]] en de [[NetBird reverse proxy]] bereiken de apps op containernaam. NetBird vertrouwt `172.19.0.0/16` als proxy (`trustedHTTPProxies`). |
| `web` | 172.22.0.0/16 | traefik, netbird-proxy, n8n, reismannetje, nb-monit | Tweede gedeeld netwerk; n8n zit erop om [[Reismannetje]] en [[nb-monit]] direct te checken ([[Geo-blokkade]]). |
| `netbird_netbird` | 172.20.0.0/16 | netbird-server, dashboard, proxy | Intern NetBird-stack. |
| `downloader_default` | 172.23.0.0/16 | traefik (+ shelfmark als die draait) | Voor [[Shelfmark]]. |
| `docker0` | 172.17.0.0/16 | (niets) | Alleen dit netwerk mag host-poorten bereiken volgens de [[Firewall (iptables)]]. |
| oud: `ebooks_default`, `n8n_default`, `vakantieplanner_default` | | leeg | Restanten van vóór de herindeling. |

> [!warning] Hairpin-NAT
> Een container die een publieke URL van deze server opvraagt komt binnen als `172.19.0.1` → geen land → `403 country_restricted` bij de NetBird-proxy. Daarom checken [[n8n-flows]] apps direct op containernaam. Zie [[Geo-blokkade]].
