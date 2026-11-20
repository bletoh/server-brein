---
tags: [app, minecraft, systemd]
domein: bsm.benjaminhashi.nl
---
# Bedrock Server Manager (BSM)

> [!note] Sinds 2026-10-31
> BSM 3.10.6 draait met de server in de k3s-pod `mc-server/bedrock` (image `mc-bsm`, hostNetwork, poort 11325 zoals altijd). `systemctl … bedrock-server-manager-webui` werkt nog (schakelaar). → [[Minecraft op k3s]]

Python-beheerprogramma (v3.10.6) voor de [[Bedrock-server]]. **Niet** in Docker.

| | |
|---|---|
| Service | `bedrock-server-manager-webui` (User almalinux), zie [[Systemd-services]] |
| Venv / werkmap | `/opt/bsm-venv`, `/opt/bsm-data` |
| Config + servers | `~/.config/bedrock-server-manager/` (db, json, `data/servers/bedrock_server`, `data/backups`, `data/content/addons`) |
| Webui | poort 11325 → [[bsm.benjaminhashi.nl]] (SSO) |
| Autostart | aan → BSM starten = server starten |

## Gedrag om te onthouden
- Herstart = `sudo systemctl restart bedrock-server-manager-webui` of de knop in de BSM-UI.
- `stop` op stdin ziet BSM als crash en herstart max 3× (teller reset pas bij webui-herstart) → niet op vertrouwen.
- BSM toont `*.mcworld` in de backupmap; het [[Vriendenpaneel]] maakt daar `paneel_*.mcworld`-backups.
- Minecraft-autoupdate staat **uit** (addon-compatibiliteit).

Zie [[Wereldbackups]], [[weekly-update.sh]] (stopt BSM netjes).
