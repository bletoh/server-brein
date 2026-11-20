---
tags: [agent]
---
# Openstaand

Bijgehouden door de agents (zie [[Agents]]). `[~]` = gedaan maar wacht op de eigenaar. Vink zelf af of zeg in een sessie "pak punt X van Openstaand op".

## Server

- [x] 2026-11-20 | prioriteit midden | Grafana door kernel OOM-gekilld (limiet 768m) | controleer `docker inspect grafana --format '{{.State.OOMKilled}} {{.RestartCount}}'`; bij herhaling mem_limit naar 1g (opgelost 2026-11-20: de kill was om 19:51 bij de oude limiet van 384m; sindsdien 768m, ~420 MB in gebruik, 0 herstarts)
- [x] 2026-11-20 | prioriteit laag | OOM-query in Prometheus/Grafana geeft "geen data" terwijl er wel een kill was | alertregel op `container_oom_events_total` (cAdvisor) (opgelost 2026-11-20: regel "Container door geheugenlimiet gestopt" bestond al; de kill was vóór cAdvisor meette)
- [x] 2026-11-20 | prioriteit laag | flux-update dry-run mislukte 2026-11-16 | kijk of het bij de volgende weekly-update terugkomt (opgelost 2026-11-20: dry-run botste met velden van kustomize-controller; nu `--field-manager=kustomize-controller`, en het script wacht tot Flux de commit echt heeft toegepast. Flux handmatig bijgewerkt naar v2.10.0. Bijvangst: die sync haalde de kubectl-pauze van mc/mc-server weg, nu staat `suspend: true` in Git en past `minecraft-weer-aan.sh` dat aan)
- [x] 2026-11-20 | prioriteit laag | Gestopte containers pl-test en rmreview en oude `*.voor-*-20261120` back-upkopieën | opruimen als niet meer nodig (containers verwijderd 2026-11-20; de `.voor-*-20261120`-kopieën blijven tot 2026-11-27)

## Reismannetje

- [x] 2026-11-20 | prioriteit hoog | 553 x 502 op `/api/prices/flight` (8 %): Travelpayouts-4xx/429 en datums in het verleden worden 502 | voorstel 1 van [[2026-W47]] (geen bug: alle 502's kwamen van Traefik (OriginStatus 0), 719 van de 862 op 13-11 rond 23:00 = het overbelastingsincident, opgelost op 16-11 met 'Prijzen rustig ophalen'. Na 16-11 nog 1 op flight)
- [x] 2026-11-20 | prioriteit hoog | 275 x 502 en p95 103 s op `/api/prices/stay` (Airbnb) | voorstel 2 van [[2026-W47]] (meten, stroomonderbreker, max 30 s) (p95 103 s kwam van 13-11; sinds 17-11 p95 ~3 s, max 6 s, dus geen stroomonderbreker nodig. De resterende 502's: plekken zonder Airbnb-woningen (China e.d.) gaven 'pagina niet te lezen'. Fix 00eb0f9 live op productie 2026-11-20 21:50)
- [x] 2026-11-20 | prioriteit midden | npm audit: undici (high, vastgezet op ~6.29.0), nodemailer (moderate), @simplewebauthn/server (low) | voorstel 3 van [[2026-W47]] (undici 6.29.1, nodemailer 10.6.1, @simplewebauthn/server 13.3.3: audit 0, 219 tests ok; live op productie 2026-11-20 met 00eb0f9)
- [~] 2026-11-20 | prioriteit midden | Idee: Lijst-paneel (#planner) op de Wereldkaart opheffen en inhoud verdelen | plan in [[2026-W47]], eerst branch claude/wereldkaart-volledig bekijken (gedaan 2026-11-20: tab Plannen was al weg sinds 12-11; nu plekken als strook op de kaart, paneel zonder dubbelingen. Commit 2a37a42 op branch `claude/kaart-lijst-desktop`, live op test, wacht op merge naar main)
- [~] 2026-11-20 | prioriteit laag | Idee: desktop dichter bij mobiel | eerst screenshots 390/1280 px per route, zie [[2026-W47]] (laptop was sinds 12-11 al grotendeels gelijk; screenshots 390/1280 per scherm vergeleken: nu ook de kaart (zelfde strook) en Groep (gecentreerd) gelijk. Zelfde commit 2a37a42, wacht op merge)
- [x] 2026-11-20 | prioriteit laag | Snapshot-filter mist app-logregels van prijzen (`prijzen vlucht`, `airbnb`) | filter van de snapshot uitbreiden (serverkant) (opgelost 2026-11-20: filter vangt nu ook prijzen/airbnb/aviasales/timeout/5xx)
- [x] 2026-11-20 | prioriteit laag | Idee: troep in /home/almalinux opruimen | geen Reismannetje-zaak; serversessie, zie plan in [[2026-W47]] (al gedaan op 2026-11-12, zie ~/archief/LEESMIJ.md; home bevat nu alleen werkmappen. Idee mag uit ideen.md)
