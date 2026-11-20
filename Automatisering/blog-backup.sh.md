---
tags: [automatisering, script, backup]
bestand: /usr/local/sbin/blog-backup.sh
---
> **Verwijderd op 2026-10-26** op verzoek van de eigenaar (geheugen besparen). Laatste stand: `/srv/archive/blog-20261026` (ghost.sql + blog-map.tar.gz). Hieronder de oude situatie, ter naslag.

# blog-backup.sh

Elke nacht 01:45, log `/var/log/blog-backup.log`. `mysqldump --single-transaction` (gecontroleerd op "Dump completed") + `content/` (zonder logs) → `/srv/backups/blog` (30 dagelijks + maandelijks) en de NAS. Telt het aantal berichten in de log.

Terugzetten: tar uitpakken, `content/` terug, `docker exec -i blog-db sh -c 'MYSQL_PWD="$MYSQL_ROOT_PASSWORD" mysql -uroot ghost' < ghost.sql`.

Zie [[Blog (Ghost)]], [[Backup-strategie]].
