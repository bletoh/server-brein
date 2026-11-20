---
tags: [server, beveiliging, netwerk]
---
# Firewall (iptables)

> [!note] Sinds 2026-10-31
> Erbij voor k3s: filter INPUT-regel 014 (pods 10.42/16 naar de host) en mangle-regels die de NetBird-markbits 0x30000 wissen voor pod-verkeer. → [[k3s-beveiliging]]

Geen firewalld: klassieke **iptables** met regels in `/etc/sysconfig/iptables` (ook in [[app-backups.sh]] → `server`). Docker en NetBird voegen hun eigen ketens toe.

## INPUT-regels (op volgorde)
| Nr | Regel | Waarvoor |
|---|---|---|
| (NetBird) | `wt0` → `NETBIRD-ACL-INPUT`, anders DROP | [[NetBird ACL en groepen]] bepaalt wat via de VPN mag |
| 202 | tcp 3001 | restant van [[nb-monit]] (draait nu zonder host-poort) |
| 000 | RELATED,ESTABLISHED | |
| 002 | lo | |
| 003 | icmp | |
| 010 | alles via `wt0` | VPN-verkeer |
| 011 | `192.168.178.0/24` | thuis-LAN (via NAS-route) |
| 012 | `172.17.0.0/16` via docker0 | containers op docker0 → host |
| 013 | `172.16.0.0/12` → tcp 11325 | [[Traefik]]/[[NetBird reverse proxy]] → [[Bedrock Server Manager]]-webui |
| 015 | `172.16.0.0/12` → `172.17.0.1` tcp 9100 | Prometheus → node-exporter ([[Grafana]], sinds 2026-11-20) |
| 200 | tcp 80, 443 | [[Traefik]] |
| 201 | udp 51820 | NetBird WireGuard |
| 203 | udp 19132 | [[Bedrock-server]] |
| 999 | REJECT alles | |

> [!important] SSH
> Poort 22 staat **niet** open voor internet. SSH gaat via NetBird (`wt0`, ook NetBird-SSH op 22022). Zie [[NetBird]].

> [!note] Gepubliceerde Docker-poorten
> `3478/udp` (STUN) en `51821/udp` (proxy-WireGuard) lopen via Docker's DNAT/FORWARD en dus niet via deze INPUT-regels.

## Valkuil
Containers op `books-net`/`web` mogen standaard **geen** host-poorten bereiken (alleen docker0). Daarom regel 013 voor BSM. Een nieuwe host-dienst achter Traefik → eerst een regel toevoegen, anders 502. Zie [[Valkuilen en lessen]] en [[Poorten]].
