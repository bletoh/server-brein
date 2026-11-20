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

## Valkuilen
- **Proxy-doel:** NetBird-service `dbei4o9mn2ec738gc0g0` → `grafana:8080` (cluster, direct upstream). Tot de nieuwe API-token (20-11) liep dit via de alias `loadmon`; die is weg.
- **cAdvisor scant schijfgebruik** van alle containers: dat kostte 3-4 cores. Daarom `disk,diskIO` uit en `cpus: 0.5`.
- **Firewall:** containers op books-net/monitoring mogen standaard niet naar de host. Regel 015 laat `172.16.0.0/12` alleen bij `172.17.0.1:9100` ([[Firewall (iptables)]]).
- **SQLite-plugin:** de macro's `$__unixEpochFrom()` werken niet in de backend; gebruik `($__from/1000)` en `($__to/1000)`. De app-tabel heeft honderden namen (kortlevende processen), dus altijd een top-N.

Bijgehouden door [[weekly-update.sh]] en [[ensure-apps-up.sh]] (APPS), backup via [[app-backups.sh]] (kleine_apps, zonder Prometheus-data). Zie [[Geheugen]], [[Monitoring en meldingen]], [[Docker]].
