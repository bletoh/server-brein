---
tags: [backup, nas]
domein: nas.benjaminhashi.nl
---
# backupnas (Synology)

> [!note] Sinds 2026-10-31
> De NAS controleert de server nu ook van buitenaf en meldt storingen zelf in Discord (DSM-taak elke 15 min). → [[NAS app-check]], [[Monitoring en meldingen]]

Synology **DS118**, DSM 7.3.2, thuis. NetBird-peer `BACKUPNAS`, IP `100.109.137.157`, gebruiker `Jamaal`.
- Ontvangt de nachtelijke backups in `~/backups/<app>` (laatste 30 per app) → [[Backup-strategie]].
- Draait elk kwartier de [[NAS app-check]] (DSM Taakplanner, mail bij fout).
- Routeert het thuisnetwerk 192.168.178.0/24 in NetBird → [[NetBird ACL en groepen]].
- DSM-webinterface via [[nas.benjaminhashi.nl]] (SSO).
- SSH vanaf de VPS met de sleutel in `~/.config/nas-check/` (geen sudo op de NAS).

Zie [[Apparaten]].
