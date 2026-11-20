---
tags: [server, automatisering, cron]
---
# Cron-planning

Alle tijden Europe/Amsterdam (`CRON_TZ`). Root-jobs in `/etc/cron.d/`. De Minecraft-jobs uit de crontab van `almalinux` zijn sinds 2026-10-31 k3s-CronJobs (zelfde schema en logbestanden, zie [[Minecraft op k3s]]); in die crontab staan alleen nog de `deploy.py`-regels van glanerbrugcraft.

> [!warning] Sinds 2026-11-19 staat Minecraft uit
> De mc-CronJobs zijn gesuspend, de `mc-*`-bestanden in `/etc/cron.d` heten `*.uit` en de `deploy.py`-regels beginnen met `#MCUIT#`. → [[Minecraft uit (november 2026)]]

## Elke dag / nacht
| Tijd | Job | Notitie |
|---|---|---|
| 01:15 | `app-backups.sh` (n8n, netbird, calibre, traefik, crowdsec, kleine apps, bedrock, server) | [[app-backups.sh]] |
| 01:30 | `reismannetje-backup.sh` | [[reismannetje-backup.sh]] |
| 04:40 | `bedrock-ertsscan.sh` (user) | [[Mijnhoogte en ertsscan]] |
| 18:00 | `dagelijkse-opruiming.sh` | [[dagelijkse-opruiming.sh]] |
| 07:00 | `n8n-daily-stats.sh` → n8n-webhook → ntfy-push | [[n8n-daily-stats.sh]] |

## Steeds
| Interval | Job | Notitie |
|---|---|---|
| elke 3 min (sinds 12-11) | `bedrock-map-collect.py` (k3s CronJob `kaart-collect`) | [[Kaart-collector]] |
| elke 10 min (sinds 12-11, alleen na spelen) | `bedrock-map.sh` (k3s CronJob `kaart-render`) | [[bedrock-map.sh]] |
| elke 5 min (sinds 12-11) | `mc-mijlpalen.py` (k3s CronJob `mijlpalen`) | [[Stats en ranglijst]] |
| elke 15 min (sinds 12-11) | `mc-weer.py` (k3s CronJob `weer`) | [[Scripts in ~-bin]] |
| :07 :22 :37 :52 | `borden_bouw.py` (k3s CronJob `borden-bouw`) | [[Bedrock-kaart]] |
| elke 2 min | `reismannetje-autodeploy.sh` (prod) en `reismannetje-test-autodeploy.sh` (test) | [[Reismannetje op k3s]] |
| elke 2 min | `deploy.py auto` (user, glanerbrugcraft) | [[Minecraft op k3s]] |
| elke 5 min | k3s CronJob `k8s-wachter` | [[Monitoring en meldingen]] |
| elke 5 min | `/etc/cron.d/db-metrics`: SQLite-groottes voor Grafana (`db-metrics.sh`) | [[Grafana]] |
| elke 5 min | `/etc/cron.d/loadmon-containers`: containernamen voor loadmon (`loadmon-containers.sh`: Docker + k3s via crictl → `containers.json`) | [[Geheugen]] |
| elk uur :30 | `ensure-apps-up.sh --quiet` | [[ensure-apps-up.sh]] |
| elke minuut | n8n "Uptime-alarm" + "Minecraft-alarm" (in n8n zelf) | [[n8n-flows]] |
| elk kwartier | NAS app-check (DSM Taakplanner op de NAS, echt actief sinds 2026-10-31; meldt zelf in Discord) | [[NAS app-check]] |

## Wekelijks
| Tijd | Job | Notitie |
|---|---|---|
| ma 03:00 | `weekly-update.sh` (dnf, images, k3s-images, Flux-update, registry opruimen, evt. reboot) | [[weekly-update.sh]], [[k3s-onderhoud]] |
| ma 04:00–05:00 | k3s-patches (system-upgrade-controller) | [[k3s-onderhoud]] |
| ma 04:00 | `ensure-apps-up.sh` | [[ensure-apps-up.sh]] |
| @reboot +120 s | `ensure-apps-up.sh` | |
| ma ≥00:05 | weekbonus emeralds (via de collector) | [[Economie en winkel]] |

Volgorde 's nachts: backups (01:15–01:30) → ertsscan (04:40) → rapport (07:00). Alles wat de Bedrock-wereld aanraakt deelt het slot `/tmp/bedrock-map.lock`.

**Zomer/wintertijd:** plan niets met `CRON_TZ=Europe/Amsterdam` tussen 02:00 en 03:00. cronie beschermt alleen zijn eigen klok (UTC) tegen de klokwissel; `CRON_TZ`-jobs in dat uur draaien eind oktober twee keer en eind maart helemaal niet. Daarom staan de backups sinds 2026-10-24 op 01:15–01:45 (stonden op 02:15–02:45).
