---
tags: [agent]
---
# Openstaand

Bijgehouden door de agents (zie [[Agents]]). Vink zelf af of zeg in een sessie "pak punt X van Openstaand op".

## Server

- [ ] 2026-11-20 | prioriteit midden | Grafana door kernel OOM-gekilld (limiet 768m) | controleer `docker inspect grafana --format '{{.State.OOMKilled}} {{.RestartCount}}'`; bij herhaling mem_limit naar 1g
- [x] 2026-11-20 | prioriteit laag | OOM-query in Prometheus/Grafana geeft "geen data" terwijl er wel een kill was | alertregel op `container_oom_events_total` (cAdvisor) (opgelost 2026-11-20: regel "Container door geheugenlimiet gestopt" bestond al; de kill was vóór cAdvisor meette)
- [ ] 2026-11-20 | prioriteit laag | flux-update dry-run mislukte 2026-11-16 | kijk of het bij de volgende weekly-update terugkomt
- [ ] 2026-11-20 | prioriteit laag | Gestopte containers pl-test en rmreview en oude `*.voor-*-20261120` back-upkopieën | opruimen als niet meer nodig

## Reismannetje

- [ ] 2026-11-20 | prioriteit hoog | 553 x 502 op `/api/prices/flight` (8 %): Travelpayouts-4xx/429 en datums in het verleden worden 502 | voorstel 1 van [[2026-W47]]
- [ ] 2026-11-20 | prioriteit hoog | 275 x 502 en p95 103 s op `/api/prices/stay` (Airbnb) | voorstel 2 van [[2026-W47]] (meten, stroomonderbreker, max 30 s)
- [ ] 2026-11-20 | prioriteit midden | npm audit: undici (high, vastgezet op ~6.29.0), nodemailer (moderate), @simplewebauthn/server (low) | voorstel 3 van [[2026-W47]]
- [ ] 2026-11-20 | prioriteit midden | Idee: Lijst-paneel (#planner) op de Wereldkaart opheffen en inhoud verdelen | plan in [[2026-W47]], eerst branch claude/wereldkaart-volledig bekijken
- [ ] 2026-11-20 | prioriteit laag | Idee: desktop dichter bij mobiel | eerst screenshots 390/1280 px per route, zie [[2026-W47]]
- [ ] 2026-11-20 | prioriteit laag | Snapshot-filter mist app-logregels van prijzen (`prijzen vlucht`, `airbnb`) | filter van de snapshot uitbreiden (serverkant)
- [ ] 2026-11-20 | prioriteit laag | Idee: troep in /home/almalinux opruimen | geen Reismannetje-zaak; serversessie, zie plan in [[2026-W47]]
