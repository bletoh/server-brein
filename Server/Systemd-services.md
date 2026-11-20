---
tags: [server, systemd]
---
# Systemd-services (eigen)

| Unit | User | Wat | Notitie |
|---|---|---|---|
| `docker` | root | Docker-engine | [[Docker]] |
| `k3s` | root | Kubernetes (k3s), sinds 2026-10-31 | [[Kubernetes (k3s)]] |
| `netbird` | root | NetBird-client (peer "OVH VPS", 100.109.21.192) | [[NetBird]] |
| `bedrock-server-manager-webui` | root | sinds 2026-10-31 een schakelaar: `mc-k8s-dienst` zet de k3s-deployment `mc-server/bedrock` aan (1) of uit (0); BSM en de server draaien in die pod | [[Minecraft op k3s]] |
| `claude-remote-control` | almalinux | `claude remote-control` (mobiele/web-sessies), in `script` voor een pty | [[claude-remote-control]] |

Weg sinds 2026-10-31 (nu sidecars in de pod `mc-server/bedrock`): `bedrock-map-live`, `bedrock-map-queue`, `mc-discord`, `vriendenpaneel-worker`. Oude unit-files zitten in `/srv/backups/archief-voor-k3s-20261031.tar.gz`.

[[ensure-apps-up.sh]] controleert `docker`, `k3s`, `netbird` en `bedrock-server-manager-webui` elk uur en start ze zo nodig; daarnaast de k8s-deployments en Flux.

> [!tip] Bedrock veilig herstarten
> `sudo systemctl restart bedrock-server-manager-webui` werkt nog steeds: de pod gaat uit en weer aan, en BSM stopt de server netjes op SIGTERM. Stoppen = `systemctl stop …` (slaat de wereld op). Zie [[Bedrock-server]].
