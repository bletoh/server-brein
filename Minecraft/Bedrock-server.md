---
tags: [minecraft, moc]
map: ~/.config/bedrock-server-manager/data/servers/bedrock_server
---
# Bedrock-server

> [!note] Sinds 2026-10-31
> De server, BSM en de workers draaien in k3s (namespace `mc-server`); de kaart en MCXboxBroadcast in `mc`. Beheer werkt zoals altijd via systemctl, `cmd.sh` en `deploy.py`. → [[Minecraft op k3s]]

Minecraft Bedrock Dedicated Server **1.26.51.1**, beheerd door [[Bedrock Server Manager]]. Verbinden: [[minecraft.benjaminhashi.nl]] poort 19132 (UDP, transport raknet).

## Instellingen (server.properties)
survival, difficulty hard, cheats aan, max 10 spelers, allow-list uit, view-distance 24, **tick-distance 12** (max, eigenaar wil een levendige wereld), max-threads 8 (niet aanraken), wereld "Bedrock level". Gamerules: showdaysplayed, slapen 50%, coördinaten aan, **pvp uit** (wordt elke minuut afgedwongen).

## Eigen addons (alleen scripts, stable API @minecraft/server 2.10.0)
- [[Addon Homes & Teleport]] (v1.4.0) — homes, warps, tpa, casino, arena, kliniek, economie, bouwscripts, chaos-events
- [[Addon Handige Extra's]] (v1.6.0) — AFK, speeltijd/stats, oogsten, kisten sorteren, item-opruiming, kaartlogging, events

Regel van de eigenaar: alleen quality-of-life, geen echt gameplayvoordeel, minimale belasting, geen resource packs (uitzonderingen zijn weer verwijderd).

## Rond de server
- Webkaart + stats: [[Bedrock-kaart]], [[Kaart-collector]], [[Stats en ranglijst]], [[Mijnhoogte en ertsscan]]
- Beheer door vrienden: [[Vriendenpaneel]]
- Console-commando's: [[Scriptevents]]
- Wereld: [[Locaties in de wereld]], [[Spelers]], [[Demodorp]], [[Boomhut bletoh1]]
- Spel: [[Economie en winkel]], [[Casino, arena en kliniek]], [[Chaos-events]]
- Herstellen: [[Wereldbackups]], [[Chunk-merge hersteltool]]
- Bewaking: [[Minecraft-alarm (Discord)]], [[Discord status-commando]]

## Veilig omgaan
- Herstart: `sudo systemctl restart bedrock-server-manager-webui` (of BSM-UI / paneel).
- Console: schrijven naar `/proc/<pid>/fd/0` van `pgrep -x bedrock_server` (niet het BSM-python-proces).
- Consistente kopie: `save hold` → `save query` (wachten op "Files are now ready to be copied") → kopiëren → `save resume`, onder slot `/tmp/bedrock-map.lock`.
- `reload` in de console laadt gewijzigde scripts zonder herstart; een **nieuw** .js-bestand of nieuwe slash-commando's vragen wel een herstart.
- De melding "TRANSPORT TYPE ERROR … NetherNet" bij het opstarten is onschuldig.
- Na een Minecraft-update controleren of de addons nog laden.

Backups: [[app-backups.sh]] (bedrock, wereld via save hold), [[Wereldbackups]].

## NPC-skins (sinds 2026-10-31)
Alle NPC's zien eruit als LeBron James: resource pack `npc_lebron_RP` vervangt alle 60 vanilla NPC-texturen door één skin (goudgeel tenue met 23, hoofdband, baard). Generator en uitleg in `generators/npc-lebron` van de glanerbrugcraft-repo. Terug naar normaal: het pack uit `server/world_resource_packs.json` halen en herstarten. → [[Minecraft op k3s]]
