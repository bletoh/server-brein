---
tags: [moc, kubernetes, k3s]
aliases: [k3s, Kubernetes, k8s]
bijgewerkt: 2026-10-31
---
# Kubernetes (k3s)

Sinds **2026-10-31** draait naast [[Docker]] een single-node **k3s** (v1.36) op de [[VPS (OVH)]]. Stap voor stap zijn [[Reismannetje]] en alles rond de [[Bedrock-server]] erheen verhuisd. Docker-[[Traefik]] blijft de voordeur; k3s heeft geen eigen Traefik of load balancer.

> [!info] Kort
> - Alles staat in Git: branch `k8s` van `bletoh/vakantieapp`, op de server `/srv/k8s/gitops` → [[Flux en GitOps]]
> - Eigen images in een [[Lokale registry]] op `127.0.0.1:5000`
> - Uitgebreide beheerdocumentatie op de server: `/srv/k8s/README.md`
> - kubectl: `sudo /usr/local/bin/k3s kubectl ...` (sudo en cron kennen `/usr/local/bin` niet)

## Wat draait er
| Namespace | Wat | Notitie |
|---|---|---|
| `reismannetje` | Reismannetje productie (reismannetje.nl), ClusterIP 10.43.100.40 | [[Reismannetje op k3s]] |
| `reismannetje-test` | testomgeving (reismannetje-test.benjaminhashi.nl), ClusterIP 10.43.100.41 | [[Reismannetje op k3s]] |
| `mc` | kaartsite, kaart-API, vriendenpaneel-API, MCXboxBroadcast; ClusterIP kaart 10.43.100.50 | [[Minecraft op k3s]] |
| `mc-server` | BSM + Bedrock-server met 4 workers als sidecars, Minecraft-cronjobs | [[Minecraft op k3s]] |
| `monitoring` | ntfy-naar-Discord-relay en k8s-wachter | [[Monitoring en meldingen]] |
| `registry` | lokale image-registry | [[Lokale registry]] |
| `flux-system` | Flux (source- en kustomize-controller) | [[Flux en GitOps]] |
| `system-upgrade` | automatische k3s-patches | [[k3s-onderhoud]] |

Wat bewust buiten k3s blijft: [[NetBird]] (WireGuard, veel UDP), [[Traefik]] en [[CrowdSec]] (de voordeur), [[n8n]], [[Calibre-web]], [[nb-monit]], loadmon, en beheerscripts als `deploy.py`, de `mc-*`-rootscripts en de backups.

## Hoe het verkeer loopt
Docker-containers (Traefik, n8n, NetBird-proxy) bereiken pods via **vaste ClusterIP's** in 10.43.0.0/16. Dat adres is niet publiek; NodePorts luisteren alleen op 127.0.0.1. Zo kan niemand om Traefik en CrowdSec heen.

## Config
- `/etc/rancher/k3s/config.yaml`: traefik, servicelb en metrics-server uit, SELinux aan, `nodeport-addresses=127.0.0.1/32`
- `/etc/rancher/k3s/registries.yaml`: [[Lokale registry]]
- Data van apps staat op vaste host-mappen via PersistentVolumes met `Retain` (bijv. `/srv/k8s/reismannetje/data`)
- Firewall-aanpassingen: [[k3s-beveiliging]] en [[Firewall (iptables)]]

## Zie ook
[[Flux en GitOps]] · [[Lokale registry]] · [[Reismannetje op k3s]] · [[Minecraft op k3s]] · [[Monitoring en meldingen]] · [[k3s-beveiliging]] · [[k3s-onderhoud]] · [[Valkuilen en lessen]] · [[Tijdlijn]]
