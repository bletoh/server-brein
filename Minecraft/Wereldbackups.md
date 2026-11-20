---
tags: [minecraft, backup]
map: ~/.config/bedrock-server-manager/data/backups/bedrock_server
---
# Wereldbackups (Bedrock)

Drie soorten:
1. **Nachtelijk** via [[app-backups.sh]] (bedrock): hele wereld + instellingen + BSM-config → [[srv-backups]] en de NAS.
2. **Vóór elke grote ingreep** door Claude: mappen `voor_<actie>_<datum>` in de BSM-backupmap (bijv. `voor_casino_20261013-1653`, `voor_atoombom_…`, `voor_boomhut3_…`, `voor_winkelgebouw_…`), ook `na_chaos_20261017-1335`.
3. **Paneel-backups** `paneel_<datum>_<naam>.mcworld` via het [[Vriendenpaneel]] (laatste 5, terug te zetten in BSM).

Totaal ±2 GB. Herstellen van een deel van de wereld: [[Chunk-merge hersteltool]]. Hele wereld: server uit, map terugzetten in `worlds/`.

Zie [[Bedrock-server]], [[Backup-strategie]].
