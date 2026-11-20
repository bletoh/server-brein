---
tags: [automatisering, script]
bestand: /usr/local/sbin/dagelijkse-opruiming.sh
---
# dagelijkse-opruiming.sh

Sinds 2026-11-02. Elke dag om 18:00 (NL-tijd) via `/etc/cron.d/dagelijkse-opruiming`. Log: `/var/log/dagelijkse-opruiming.log`.

Ruimt op:
- dangling Docker-images en build-cache ouder dan 7 dagen
- tags in de [[Lokale registry]] (`127.0.0.1:5000`), behalve de nieuwste 3 per repo
- k3s-images (`crictl rmi --prune`)
- `/tmp/claude-1000`, `/tmp/vp-*` en coredumps ouder dan 3 dagen
- journal ouder dan 30 dagen, dnf-pakketcache, geroteerde logs ouder dan 60 dagen

Blijft **af** van `/srv/backups`, BSM-backups en app-data. De oude `.voor-*`-kopieën in `/srv/backups` worden bewust met de hand opgeruimd.

Zie [[Cron-planning]], [[weekly-update.sh]], [[srv-backups]].
