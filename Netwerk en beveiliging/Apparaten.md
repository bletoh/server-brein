---
tags: [netwerk, vpn]
---
# Apparaten (NetBird-peers)

| Apparaat | Groep | NetBird-IP | Opmerking |
|---|---|---|---|
| OVH VPS | Server | 100.109.21.192 | deze server, exit node — [[VPS (OVH)]] |
| BACKUPNAS (Synology DS118) | nas | 100.109.137.157 | backups + app-check — [[backupnas (Synology)]] |
| Benjamin iPhone | eigen-apparaten | | client-versie `ci-…` |
| wsl_laptop_thuis | eigen-apparaten | | via exit node → geen land → [[Geo-blokkade]] |
| WSL-Werk | eigen-apparaten | | relayed peer (gevoelig voor HTTP/3-probleem, zie [[Traefik]]) |
| iPhone papa | familie | | alleen exit node |

Zie [[NetBird ACL en groepen]], [[NetBird]].
