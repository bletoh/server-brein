---
tags: [automatisering, script, backup]
bestand: /usr/local/sbin/app-backups.sh
---
# app-backups.sh

> [!note] Sinds 2026-10-31
> Nieuwe backup `k3s`: Secrets (yaml), Flux deploy key, k3s-token, `/etc/rancher/k3s`, clusterdatabase en de gitops-werkkopie. → [[k3s-onderhoud]]

Elke nacht 01:15 (`/etc/cron.d/app-backups`, log `/var/log/app-backups.log`). Per app een `tar.gz` in `/srv/backups/<app>/daily` (30 dagen) + `monthly/` (±6 maanden), en de nieuwste naar de NAS `backups/<app>` (laatste 30).

| App | Inhoud |
|---|---|
| n8n | `pg_dump` (gecontroleerd op "dump complete") + compose/.env/data-config + `/srv/n8n-flows` → [[n8n]] |
| netbird | store/idp/events.db (SQLite online backup + integrity_check) + config + proxy-certs → [[NetBird]] |
| calibre-web | `app.db` + boeken → [[Calibre-web]] |
| traefik | config + `acme.json` → [[Traefik]] |
| crowdsec | `crowdsec.db` + config → [[CrowdSec]] |
| kleine-apps | nb-monit, vriendenpaneel, bedrock-map (zonder tegels), shelfmark |
| bedrock | wereld via save hold/query/resume onder `/tmp/bedrock-map.lock` + server.properties/allowlist/permissions + BSM-config/addons → [[Wereldbackups]] |
| server | `/usr/local/sbin`, `/etc/cron.d`, systemd-units, iptables, resolv.conf, `/srv/README.md`, nas-check, `~/bin`, crontab |

Eén app los: `sudo app-backups.sh bedrock` (namen met underscore). Eén mislukte app stopt de rest niet.

Zie [[Backup-strategie]], [[backupnas (Synology)]], [[reismannetje-backup.sh]].
