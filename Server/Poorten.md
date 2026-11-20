---
tags: [server, netwerk]
---
# Poorten

> [!note] Sinds 2026-10-31
> k3s: API-server 6443 en kubelet 10250, van buiten dicht. Registry alleen op 127.0.0.1:5000; NodePorts alleen op 127.0.0.1. Minecraft en BSM blijven op 19132 en 11325 (hostNetwork). → [[k3s-beveiliging]]

| Poort | Proto | Luistert | Publiek? | Wat |
|---|---|---|---|---|
| 80, 443 | tcp | docker-proxy → [[Traefik]] | ja | alle websites ([[Domeinen]]) |
| 19132 (v6 19133) | udp | bedrock_server | ja | [[Bedrock-server]] (`minecraft.benjaminhashi.nl`) |
| 51820 | udp | NetBird-client | ja | WireGuard van deze peer, [[NetBird]] |
| 51821 | udp | netbird-proxy | ja | WireGuard van de [[NetBird reverse proxy]] |
| 3478 | udp | netbird-server | ja | STUN, [[NetBird]] |
| 11325 | tcp | BSM (python) | alleen docker/VPN | [[Bedrock Server Manager]] webui (`bsm.benjaminhashi.nl`) |
| 5678 | tcp | 127.0.0.1 → n8n | nee | [[n8n]] (webhook voor [[n8n-daily-stats.sh]]) |
| 8080 / 8081 | tcp | 127.0.0.1 → netbird dashboard/server | nee | [[NetBird]] |
| 22 | tcp | sshd | nee (firewall) | alleen via NetBird |
| 22022 | tcp | NetBird-SSH op `100.109.21.192` | VPN | [[NetBird]] |
| 53 | tcp/udp | NetBird DNS op wt0 | VPN | |
| 4100–4171 | tcp | node (tijdelijk) | nee | testservers van [[Reismannetje ontwikkelworkflow]] |

Zie ook [[Firewall (iptables)]].
