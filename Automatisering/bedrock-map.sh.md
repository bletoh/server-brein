---
tags: [automatisering, script, minecraft]
bestand: ~/bin/bedrock-map.sh
---
# bedrock-map.sh

> [!note] Sinds 2026-10-31
> Draait als k3s-CronJob `kaart-render` (elke 5 min), niet meer uit de crontab. → [[Minecraft op k3s]]

Elke 5 minuten (user-crontab; was 15). Met slot `/tmp/bedrock-map.lock` (`flock -n`).
1. `scriptevent kaart:warps` (warps naar de log).
2. `save hold` → `save query` tot "Data saved. Files are now ready to be copied." → kopie van `db`, `level.dat` naar `~/apps/map-work/world` → `save resume`.
3. [[uNmINeD]] rendert de overworld incrementeel naar `/srv/docker/bedrock-map/www/overworld`.
4. Schrijft `live/kaart.json` (tijd van de laatste render) en draait de [[Kaart-collector]].

`cron.log` krijgt alleen regels bij fouten. Zie [[Bedrock-kaart]].
