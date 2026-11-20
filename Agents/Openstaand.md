---
tags: [agent]
---
# Openstaand

Bijgehouden door de agents (zie [[Agents]]). Vink zelf af of zeg in een sessie "pak punt X van Openstaand op".

## Server

- [ ] 2026-11-20 | prioriteit midden | Grafana door kernel OOM-gekilld (limiet 768m) | controleer `docker inspect grafana --format '{{.State.OOMKilled}} {{.RestartCount}}'`; bij herhaling mem_limit naar 1g
- [ ] 2026-11-20 | prioriteit laag | OOM-query in Prometheus/Grafana geeft "geen data" terwijl er wel een kill was | alertregel op `container_oom_events_total` (cAdvisor)
- [ ] 2026-11-20 | prioriteit laag | flux-update dry-run mislukte 2026-11-16 | kijk of het bij de volgende weekly-update terugkomt
- [ ] 2026-11-20 | prioriteit laag | Gestopte containers pl-test en rmreview en oude `*.voor-*-20261120` back-upkopieën | opruimen als niet meer nodig

## Reismannetje
