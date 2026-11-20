---
tags: [automatisering, script, backup]
bestand: /usr/local/sbin/reismannetje-backup.sh
---
# reismannetje-backup.sh

> [!note] Sinds 2026-10-31
> Leest de data uit `/srv/k8s/reismannetje/data` (k3s-PersistentVolume) in plaats van het Docker-volume. → [[Reismannetje op k3s]]

Elke nacht 01:30, log `/var/log/reismannetje-backup.log`.
1. SQLite online backup van `reismannetje.db` + `integrity_check`.
2. Inpakken met `uploads/`, `docs/` (tickets) en `vapid.json`.
3. 30 dagelijks + maandelijks in `/srv/backups/reismannetje`, laatste 30 op de NAS.
4. Schrijft `.last-backup` → `/healthz?backup=1` geeft 503 als de laatste backup ouder is dan 30 uur (gecheckt door de [[NAS app-check]], regel `vp-backup`).

Terugzetten staat in de README van de repo. Zie [[Reismannetje]], [[Backup-strategie]].
