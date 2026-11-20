---
tags: [minecraft, referentie]
---
# Scriptevents (console-commando's)

Uitvoeren in de serverconsole (BSM, [[Vriendenpaneel]]-terminal of via `/proc/<pid>/fd/0`): `scriptevent <id> [args]`.

| Id | Addon | Wat |
|---|---|---|
| `kaart:warps` / `setwarp` / `delwarp` / `undelwarp` / `purgetrash` | Homes | warps voor de kaart → [[Bedrock-kaart]] |
| `paneel:warp` | Homes | teleport vanuit het paneel (ongebruikt) |
| `eco:bonus` / `eco:geef` / `eco:winkelweg` / `eco:prijzen` | Homes | → [[Economie en winkel]] |
| `winkel:zoek x z [r]` / `winkel:bouw x z` | Homes | plek zoeken / winkelgebouw bouwen |
| `kliniek:bouw/info/stuur/ontslag` | Homes | → [[Casino, arena en kliniek]] |
| `arena:bouw/info/stop/herstel` | Homes | colosseum |
| `demo:bouw/reset/info/stad` | Homes | → [[Demodorp]] |
| `atoom:start [demo \| x z y]` / `atoom:mega` / `atoom:wolkweg` / `atoom:megaweg` | Homes | → [[Chaos-events]] |
| `obama:bouw`, `bouw:casino/toren/hoogtes/check` | Homes | bouwscripts (niet idempotent!) |
| `meteoor:inslag x z` | Handige | meteoorinslag |
| `aardbeving:start [sec]` | Handige | aardbeving |
| `dans:start [sec]` / `dans:stop` | Handige | dieren laten dansen (stil) |
| `vuur:aan/uit/blus/haard x z` | Handige | razend vuur (staat standaard uit) |
| `stats:erbij <naam> {json}` | Handige | stats corrigeren |

Let op: een bericht dat met `[` begint wordt door de consoleparser geweigerd.
