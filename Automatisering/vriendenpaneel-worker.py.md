---
tags: [automatisering, script, minecraft]
bestand: ~/bin/vriendenpaneel-worker.py
---
# vriendenpaneel-worker.py

> [!note] Sinds 2026-10-31
> Draait als sidecar `paneel-worker` in de pod `mc-server/bedrock`. Herstarten gaat via `BSM_HERSTART=bsm-herstart` in plaats van systemctl. → [[Minecraft op k3s]]

Systemd-service `vriendenpaneel-worker` (±660 regels). Controleert elke aanvraag uit `/srv/docker/vriendenpaneel/queue` opnieuw en voert hem uit: console-regel, BSM-herstart (met 30 s waarschuwing), `.mcworld`-backup (onder het kaartslot), server.properties aanpassen, geplande commando's.

Schrijft naar `state/`: `status.json` (elke 10 s, ook CPU/RAM/schijf), `info.json` (gamerules, instellingen, ops, allowlist), `log.json`, `serverlog.json` (elke 2 s, zonder ruis), `planning.json`. Ook de publieke `www/live/server.json` voor de [[Bedrock-kaart]]. Volledige log met IP in `~/apps/map-work/vriendenpaneel.log`.

Zie [[Vriendenpaneel]], [[bedrock-map-queue.py]].
