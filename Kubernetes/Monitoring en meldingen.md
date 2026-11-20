---
tags: [kubernetes, monitoring, discord]
aliases: [Monitoring, ntfy-discord, k8s-wachter, Dead man's switch]
---
# Monitoring en meldingen

Sinds 2026-10-31 komen alle servermeldingen ook in een **eigen Discord-kanaal** (naam "Servermeldingen"). Het Minecraft-kanaal van de vrienden krijgt alleen nog de spelerberichten ([[Minecraft-alarm (Discord)]], mijlpalen, Xbox-status).

## De lagen
| Laag | Wat | Waar |
|---|---|---|
| ntfy | alle scripts en n8n sturen push-meldingen naar het ntfy-topic | [[n8n-flows]], [[Uptime-alarm]], [[Dagelijks serverrapport]] |
| **ntfy-discord** | volgt het ntfy-topic en zet elk bericht als gekleurde embed in Discord (rood/oranje bij problemen, groen bij herstel of deploy). Nooit @everyone. Draait als 1 pod (`Recreate`, anders dubbele berichten). | k3s `monitoring` |
| **k8s-wachter** | CronJob elke 5 min. Meldt crashende pods, OOMKilled, 3 of meer herstarts per uur, Pending langer dan 10 min, deployments niet beschikbaar (replicas 0 telt niet mee), mislukte jobs, Flux niet Ready en geheugen- of schijfdruk. Eén keer per probleem, en "weer in orde" bij herstel. | k3s `monitoring` |
| **NAS van buitenaf** | dead man's switch: de NAS controleert 12 apps elke 15 min en meldt zelf in Discord en ntfy, ook als de hele server plat ligt | [[NAS app-check]] |
| uurlijkse check | [[ensure-apps-up.sh]] herstart wat niet draait en kijkt ook naar k3s, de pods en Flux | host |
| loadmon | geheugen per app, nu ook voor k8s-pods (`loadmon-containers.sh` via crictl) | [[Geheugen]] |
| [[Grafana]] | dashboards op load.benjaminhashi.nl: Prometheus (host + containers, 90 d) + loadmon-geschiedenis | Docker |

## Geheimen
- Webhook van het serverkanaal: Secret `monitoring/ntfy-discord`, `/srv/k8s/server-discord-webhook` en `~/scripts/.discord-webhook` op de NAS.
- Minecraft-webhook: `/srv/n8n-flows/.discord-webhook`.

Zie [[Geheimen]].

## Webhook vervangen
Secret `ntfy-discord` opnieuw aanmaken en `rollout restart deploy/ntfy-discord`; daarnaast het bestand op de NAS vervangen.

## Getest
Een bewust mislukte job gaf binnen 5 minuten "Kubernetes: probleem" in Discord, en na het opruimen "Kubernetes: weer in orde".
