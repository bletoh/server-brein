---
tags: [minecraft, addon, code]
---
# Addon Homes & Teleport

Zelf geschreven behavior pack (uuid `a40778c6-…`), v1.4.0, ±4.500 regels in `behavior_packs/homes_teleport_BP/scripts/main.js`. Afhankelijk van `@minecraft/server` 2.10.0 en `@minecraft/server-ui` 2.2.0. Bronkopieën als `.mcpack` in `data/content/addons/` (gebouwd met Python zipfile; er is geen `zip` op de host).

## Spelersfuncties
- `/sethome /home /delhome /homes /spawn /back /tpa /tpahere /tpaccept /tpdeny`, gedeelde warps `/warp /setwarp /delwarp` (world property `homes:warps`), menu via `/homes` of een kompas.
- Handelsmenu NPC "Zwerver Unox" (alleen nog 1 emerald → 16 Unox rookworst).
- [[Casino, arena en kliniek]]
- [[Economie en winkel]] (bank, centrale winkel, NPC's Bankier en Winkelier)

## Console/scriptevents
Warps vanaf de kaart (`kaart:*`), panel-warp, bouwscripts (casino/toren/obama/winkel), demodorp en atoombommen → [[Scriptevents]], [[Chaos-events]], [[Demodorp]].

## Logging
Schrijft `[Kaart] warps`, `[Kaart] casino`, `[Kaart] eco`, `[Kaart] handel`, `[Paneel] resultaat` naar de serverlog → [[Kaart-collector]], [[vriendenpaneel-worker.py]].

Backups van `main.js` vóór elke wijziging: `~/apps/map-work/homes_main.voor_*.js`. Zie [[Addon Handige Extra's]].
