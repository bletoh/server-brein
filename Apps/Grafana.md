---
tags: [app, monitoring]
aliases: [Prometheus, loadmon]
map: /srv/docker/grafana
---
# Grafana

Sinds 2026-11-20 staat op [[load.benjaminhashi.nl]] een volledige Grafana in plaats van de eigen loadmon-pagina. Achter de [[NetBird reverse proxy]] met SSO (groep `beheerders`), dus binnen Grafana geen tweede login: anoniem = Admin-rol in de organisatie. De serverbeheerder `admin` heeft een wachtwoord in `/srv/docker/grafana/.env` ([[Geheimen]]).

## Onderdelen (`/srv/docker/grafana/compose.yml`)
| Container | Wat | Netwerk | Geheugen |
|---|---|---|---|
| grafana | Grafana 13, taal nl-NL, plugin `frser-sqlite-datasource` | books-net + monitoring | 768m |
| prometheus | 90 dagen bewaren (max 5 GB), scrape elke 30 s | monitoring | 512m |
| node-exporter | hostmetrics (CPU, geheugen, schijf, netwerk, systemd-units) | **host**, luistert alleen op `172.17.0.1:9100` | 128m |
| cadvisor | CPU/geheugen/netwerk per Docker-container (`--docker_only`) | monitoring | 256m, 0,5 CPU |
| loadmon | blijft meten (elke minuut + geheugen per app elke 5 min, ook k3s-pods) in `/srv/docker/loadmon/data/loadmon.db` | geen (`network_mode: none`) | 128m |

## Dashboards (map "Server", provisioned uit `/srv/docker/grafana/dashboards`)
- **Overzicht** (startpagina): nu-tegels, CPU per soort, load, geheugen, netwerk, schijf-IO en -ruimte, Docker-containers, geheugen per app (loadmon, top 15).
- **Geschiedenis (loadmon, 90 dagen)**: de oude loadmon-reeksen vanaf 24-10 via SQLite.
- **Node Exporter Full** (grafana.com 1860) en **Containers (cAdvisor)** (grafana.com 19792).

Overzicht en Geschiedenis worden gegenereerd met `/srv/docker/grafana/maak-dashboards.py dashboards`; wijzigingen in de UI mogen (`allowUiUpdates`), maar een herstart zet de bestanden terug. Wat je wilt houden: exporteren naar JSON en in de map zetten.

## Databasemonitoring (sinds 2026-11-20)
Dashboard **Databases** (`maak-db-dashboard.py dashboards`), in de lichte Percona-variant: Percona's `pg_stat_monitor` in de Postgres van [[n8n]], zonder PMM-server.
- **Postgres (n8n):** eigen image `n8n-postgres-pgsm:16` (`/srv/docker/n8n/postgres/Dockerfile`: postgres:16 + pg_stat_monitor 2.4.0 uit de broncode, want het zit niet in de PGDG-repo). `shared_preload_libraries=pg_stat_statements,pg_stat_monitor`, buckets van 5 min, 288 buckets (24 uur), 64 MB; `track_io_timing`, trage queries (>1 s) in de log.
- **Rol `monitoring`:** alleen-lezen (`pg_monitor`, `default_transaction_read_only`, timeout 10 s, max 5 verbindingen); wachtwoord `PG_MONITOR_PASSWORD` in `/srv/docker/grafana/.env`.
- **postgres-exporter** (books-net + monitoring) → Prometheus job `postgres`; Grafana-datasource `PostgreSQL (n8n)` voor de queryanalyse.
- **SQLite:** `/usr/local/sbin/db-metrics.sh` (cron elke 5 min, `/etc/cron.d/db-metrics`) schrijft bestandsgroottes (+WAL) van Reismannetje (prod/test), loadmon, Grafana, Calibre en de NetBird-store naar `/var/lib/node_exporter/textfile/sqlite.prom` (node-exporter textfile-collector).
- Onderdelen van het dashboard: serverstatistieken, querybelasting (zoals 'Load' in PMM), aanroepen per soort, tijd per applicatie, top-queries (klik op id → details met responstijd-histogram), queries met fouten, actieve sessies, locks, tabellen met dode rijen/vacuum, SQLite-groottes.
- **Onderhoud 2026-11-20:** handmatig `VACUUM (ANALYZE)` op de hele n8n-database en `VACUUM (FULL, ANALYZE)` op kleine tabellen (<5 MB, <100 rijen) met veel dode rijen; alle dode rijen naar 0, database 22 → 21 MB (bv. `workflow_entity` 256 → 104 kB). Niet periodiek nodig: autovacuum doet het, maar pas boven een drempel, dus bij kleine tabellen blijft "dood %" soms hoog (onschuldig). Opnieuw doen (als user `n8n`, niet `monitoring`):
  ```bash
  sudo docker exec n8n-postgres-1 psql -U n8n -d n8n -c "SET lock_timeout='5s'" -c "VACUUM (ANALYZE)"
  ```
- Bij een herstart van Postgres krijgt n8n een paar seconden "terminating connection" en herstelt zichzelf.

## Alerts (sinds 2026-11-20)
`maak-alerts.py provisioning/alerting` genereert 10 regels + contactpunt `ntfy` (webhook naar het bh-server-topic met ntfy-templating `?tpl=yes&t={{.title}}&m={{.message}}`). Groepering per alertnaam, herhaling na 12 uur, ook een melding bij herstel. De voorspelling "schijf binnen 14 dagen vol" telt pas mee met 2+ dagen meetdata. Grafana 13 heeft de oude test-API voor receivers niet meer (410); testen door rechtstreeks naar de ntfy-URL te posten. Zie [[Agents]].

## Valkuilen
- **Proxy-doel:** NetBird-service `dbei4o9mn2ec738gc0g0` → `grafana:8080` (cluster, direct upstream). Tot de nieuwe API-token (20-11) liep dit via de alias `loadmon`; die is weg.
- **cAdvisor scant schijfgebruik** van alle containers: dat kostte 3-4 cores. Daarom `disk,diskIO` uit en `cpus: 0.5`.
- **Firewall:** containers op books-net/monitoring mogen standaard niet naar de host. Regel 015 laat `172.16.0.0/12` alleen bij `172.17.0.1:9100` ([[Firewall (iptables)]]).
- **SQLite-plugin:** de macro's `$__unixEpochFrom()` werken niet in de backend; gebruik `($__from/1000)` en `($__to/1000)`. De app-tabel heeft honderden namen (kortlevende processen), dus altijd een top-N.

Bijgehouden door [[weekly-update.sh]] en [[ensure-apps-up.sh]] (APPS), backup via [[app-backups.sh]] (kleine_apps, zonder Prometheus-data). Zie [[Geheugen]], [[Monitoring en meldingen]], [[Docker]].
