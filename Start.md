---
tags: [moc, start]
aliases: [Home, Server-brein]
bijgewerkt: 2026-11-20
---
# Server-brein

Alles over de OVH-server **vps-f1805963** (`57.129.67.6`) en wat erop draait. Elke notitie linkt naar haar buren: open de **Graph view** om het web te zien.

> [!info] Hoe lees je dit
> - Begin bij een *kaart* (MOC) hieronder en klik door.
> - Kleuren in de graph: per map (Server, Kubernetes, Netwerk, Apps, Reismannetje, Minecraft, Automatisering, Backups, Domeinen, Werkwijze).
> - Geheimen staan hier **niet** in, alleen waar ze op de server liggen: zie [[Geheimen]].

## Kaarten
- **Server** — [[VPS (OVH)]] · [[Mappenstructuur]] · [[Docker]] · [[Docker-netwerken]] · [[Docker-volumes]] · [[Firewall (iptables)]] · [[Poorten]] · [[DNS-resolver]] · [[Systemd-services]] · [[Cron-planning]] · [[Geheugen]]
- **Kubernetes** — [[Kubernetes (k3s)]] · [[Flux en GitOps]] · [[Lokale registry]] · [[Reismannetje op k3s]] · [[Minecraft op k3s]] · [[Monitoring en meldingen]] · [[k3s-beveiliging]] · [[k3s-onderhoud]]
- **Netwerk en beveiliging** — [[Traefik]] · [[CrowdSec]] · [[NetBird]] · [[NetBird reverse proxy]] · [[NetBird ACL en groepen]] · [[Apparaten]] · [[Geo-blokkade]] · [[Certificaten (Let's Encrypt)]] · [[Geheimen]]
- **Domeinen** — [[Domeinen]]
- **Apps** — [[Reismannetje]] · [[n8n]] · [[Calibre-web]] · [[Shelfmark]] · [[nb-monit]] · [[Bedrock-server]] · [[Bedrock-kaart]] · [[Vriendenpaneel]] · [[Bedrock Server Manager]] · [[Grafana]]
- **Reismannetje (code)** — [[Reismannetje]] (hub met alle code- en functienotities)
- **Minecraft** — [[Bedrock-server]] (hub met addons, events, kaart, economie)
- **Automatisering** — [[Monitoring en meldingen]] · [[Cron-planning]] · [[weekly-update.sh]] · [[ensure-apps-up.sh]] · [[n8n-flows]] · [[NAS app-check]] · [[Scripts in ~-bin]]
- **Backups** — [[Backup-strategie]] · [[backupnas (Synology)]] · [[srv-backups]]
- **Werkwijze** — [[Claude Code sessies]] · [[Playwright-testen]] · [[Valkuilen en lessen]] · [[Tijdlijn]]

## In één zin per onderdeel
| Onderdeel | Wat | Notitie |
|---|---|---|
| Edge | Traefik v3 op 80/443, TLS-passthrough naar NetBird-proxy | [[Traefik]] |
| VPN | Self-hosted NetBird (management, signal, relay, reverse proxy) | [[NetBird]] |
| Kubernetes | k3s naast Docker, alles via Git en Flux (sinds 2026-10-31) | [[Kubernetes (k3s)]] |
| Reisapp | Node/Express + SQLite + MapLibre, reismannetje.nl, op k3s met testomgeving | [[Reismannetje]] |
| Minecraft | Glanerbrugcraft, Bedrock 1.26.61 via BSM, eigen addons; op k3s. **Tijdelijk uit sinds 19-11** ([[Minecraft uit (november 2026)]]) | [[Bedrock-server]] |
| Kaart + stats | uNmINeD-kaart + live stats op mc.benjaminhashi.nl | [[Bedrock-kaart]] |
| Automatisering | n8n-flows, cron-scripts, k3s-CronJobs, NAS-check | [[n8n]] |
| Meldingen | ntfy + eigen Discord-kanaal, k8s-wachter, NAS van buitenaf | [[Monitoring en meldingen]] |
| Monitoring | Grafana + Prometheus op load.benjaminhashi.nl, alerts naar ntfy | [[Grafana]] |
| Agents | dagelijkse onderhoudsagent + wekelijkse Reismannetje-agent, rapporten in `Agents/` | [[Agents]] |
| Backups | elke nacht lokaal + naar de Synology NAS | [[Backup-strategie]] |
