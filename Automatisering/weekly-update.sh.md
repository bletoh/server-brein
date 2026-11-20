---
tags: [automatisering, script]
bestand: /usr/local/sbin/weekly-update.sh
---
# weekly-update.sh

> [!note] Sinds 2026-10-31
> Doet ook: Reismannetje prod en test opnieuw bouwen (`reismannetje-k8s-deploy.sh --pull`), `registry-opruimen.sh`, `flux-update.sh` en `k8s-images-bijwerken.sh` (terwijl Minecraft uit staat). Reismannetje, bedrock-map en vriendenpaneel staan niet meer in de lijst met Docker-apps. → [[k3s-onderhoud]]

Maandag 03:00 (nacht van zondag op maandag), `/etc/cron.d/weekly-update`, log `/var/log/weekly-update.log`.

1. [[Bedrock-server]] netjes stoppen (`systemctl stop bedrock-server-manager-webui`, zo nodig `stop` op stdin).
2. `dnf -y upgrade --refresh`.
3. Per app in `APPS` (nu: traefik crowdsec calibre-web n8n nb-monit netbird loadmon grafana): `compose pull`, `build --pull`, `up -d --remove-orphans`; daarna `docker image prune`.
4. Herstart als `dnf needs-restarting -r` dat zegt; anders direct [[ensure-apps-up.sh]].

Shelfmark staat er bewust niet in. Minecraft zelf wordt niet automatisch bijgewerkt. Nieuwe app → toevoegen aan `APPS` hier én in [[ensure-apps-up.sh]].

Zie [[Cron-planning]], [[Docker]].
