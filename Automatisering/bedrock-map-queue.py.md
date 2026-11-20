---
tags: [automatisering, script, minecraft]
bestand: ~/bin/bedrock-map-queue.py
---
# bedrock-map-queue.py

> [!note] Sinds 2026-10-31
> Draait als sidecar `kaart-queue` in de pod `mc-server/bedrock`, niet meer als systemd-service. → [[Minecraft op k3s]]

Systemd-service `bedrock-map-queue`. Leest warp-aanvragen die de container `bedrock-map-api` in `/srv/docker/bedrock-map/queue` zet, stuurt ze als `scriptevent kaart:setwarp|delwarp|undelwarp` naar de serverconsole ([[Addon Homes & Teleport]] voert ze uit), logt IP + actie in `~/apps/map-work/warp-actions.log` en draait de [[Kaart-collector]] zodat de kaart binnen seconden klopt.

Patroon *container → queue-map → host-worker → console* wordt ook gebruikt door het [[Vriendenpaneel]]. Zie [[Bedrock-kaart]].
