---
tags: [automatisering, script, moc]
map: /home/almalinux/bin
---
# Scripts in ~/bin

> [!note] Sinds 2026-10-31
> De scripts staan nog in `~/bin`, maar draaien in k3s: `bedrock-map-live`, `bedrock-map-queue`, `mc-discord` en `vriendenpaneel-worker` als sidecars; collector, mijlpalen en weer als CronJobs. `deploy.py` herstart na een wijziging alleen de betreffende sidecar. → [[Minecraft op k3s]]

| Script | Draait | Notitie |
|---|---|---|
| `bedrock-map.sh` | cron elke 5 min | [[bedrock-map.sh]] |
| `bedrock-map-collect.py` | cron elke minuut | [[Kaart-collector]] |
| `bedrock-map-queue.py` | systemd | [[bedrock-map-queue.py]] |
| `vriendenpaneel-worker.py` | systemd | [[vriendenpaneel-worker.py]] |
| `bedrock-ertsscan.sh` + `.js` | cron 04:40 | [[Mijnhoogte en ertsscan]] |
| `bedrock-map-mask.py` | ongebruikt | grotlagen maskeren (lagen zijn verwijderd) |
| `nb-api` | handmatig | [[nb-api]] |

Ook in de backup `server` van [[app-backups.sh]].
