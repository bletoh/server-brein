---
tags: [automatisering, monitoring, nas]
bestand: /srv/nas-check/app-check.sh
---
# NAS app-check

> [!note] Sinds 2026-10-31
> De DSM-taak bestond tot vandaag niet; de gebruiker heeft hem aangemaakt (elke 15 min, gebruiker Jamaal). Het script probeert fouten na 15 s opnieuw, meldt zelf in Discord en via ntfy (dead man's switch), zet een tijdstempel in `~/scripts/.app-check-laatste`, en checkt mc via `/login.html`. → [[Monitoring en meldingen]]

Lichte curl-check **vanaf de NAS** (dus van buitenaf), elk kwartier via de DSM Taakplanner; mailt alleen bij fouten. Bron op de VPS `/srv/nas-check/app-check.sh`, op de NAS `/var/services/homes/Jamaal/scripts/app-check.sh`.

| Check | Verwacht |
|---|---|
| books `/login` | 200 "Calibre-Web" |
| n8n `/healthz` | 200 "ok" |
| netbird `/` en `/api/users` | 200 / 401 |
| monitor, bsm, nas | 302 → NetBird-oauth2 (SSO werkt) |
| bsm-direct `100.109.21.192:11325/api/info` | 200 |
| reismannetje.nl `/` | 200 "Reismannetje" |
| vp-backup `/healthz?backup=1` | 200 "recent" |
| mc `/` | 200 "Serverkaart" |

Wijzigen: VPS-kopie aanpassen, dan naar de NAS kopiëren (`ssh … 'cat > file' < file`). De eigenaar wil nul merkbare belasting op de NAS.

Camera-opnames afspeelbaar maken: [[camera-afspeelbaar.sh]].

Zie [[backupnas (Synology)]], [[Domeinen]].
