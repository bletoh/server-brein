---
tags: [minecraft, tool, code]
map: ~/apps/map-work/chunk-merge
---
# Chunk-merge hersteltool

Zelfgebouwde node-tool (leveldb-zlib, eigen `node_modules`) om **een deel** van de wereld terug te zetten uit een backup, zonder de rest kwijt te raken.

```bash
# server moet UIT staan: sudo systemctl stop bedrock-server-manager-webui
CIRKEL=x,z,r EXTRA=cx:cz,... node merge.js <backup-db> <live-db> cx0 cx1 cz0 cz1 [--apply]
```
- Zonder `--apply` = proefdraaien.
- Kopieert chunks plus entities (digp/actorprefix) en VILLAGE-keys.
- Gebruikt om het casino, de atoomkrater, het vuur en de chaos-middag terug te draaien.

`lees.js <db> x0 x1 y0 y1 z0 z1` leest blokken uit een wereldkopie als JSON (voor precieze bouwdiffs, zie [[Boomhut bletoh1]]).

Zie [[Wereldbackups]], [[Chaos-events]].
