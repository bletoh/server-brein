---
tags: [domein, minecraft]
---
# mc.benjaminhashi.nl

> [!note] Sinds 2026-10-31
> Geserveerd door k3s (`mc/bedrock-map`, 10.43.100.50). → [[Minecraft op k3s]]

Alles van Minecraft op het web (sinds 2026-10-14; was `map.` en `vrienden.`):
- `/` — live kaart + ranglijst/stats → [[Bedrock-kaart]], [[Stats en ranglijst]]
- `/beheer/` — [[Vriendenpaneel]] (nginx proxy naar `vriendenpaneel:8080`)
- `/api/warps/*` — warps beheren → [[Bedrock-kaart]] (bedrock-map-api)
- `/live/*.json` — live data van de [[Kaart-collector]]

## Route
- Publiek: [[Traefik]] TCP-passthrough → [[NetBird reverse proxy]] (service `mc`, geo Europa+CV, CrowdSec) → `bedrock-map:80`.
- NetBird-peers (100.109.0.0/16): Traefik termineert zelf en stuurt direct naar `bedrock-map:80` (anders 403, zie [[Geo-blokkade]]).

Gecontroleerd door [[NAS app-check]] (verwacht 200 + "Serverkaart") en [[ensure-apps-up.sh]].
