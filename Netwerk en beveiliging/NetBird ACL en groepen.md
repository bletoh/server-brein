---
tags: [netwerk, vpn, beveiliging]
---
# NetBird ACL en groepen

Ingericht 2026-10-12 (keuzes van de eigenaar).

## Groepen
| Groep | Leden |
|---|---|
| eigen-apparaten | Benjamin iPhone, wsl_laptop_thuis, WSL-Werk |
| Server | OVH VPS ([[VPS (OVH)]]) |
| nas | BACKUPNAS ([[backupnas (Synology)]]) |
| familie | iPhone papa |
| internet-exit | doel van de exit-route |
| beheerders | SSO-groep voor de [[NetBird reverse proxy]] |

Zie [[Apparaten]].

## Policies
- **Eigen apparaten → alles**
- **VPS ↔ NAS** (nodig voor backups en de [[NAS app-check]]) — posture "NetBird ≥ 0.65"
- **SSH eigen → servers** (NetBird-SSH)
- **Exit node gebruik** (eigen + familie → internet-exit)
- **Familie → exit node peer** (alleen ICMP; anders geen tunnel)
- Oude policies (Extern >> Intern, OVH << >> Thuis, SSH) staan uit.

## Routes
- `exit-node-ovh` 0.0.0.0/0 via de VPS (skip_auto_apply).
- `thuis-netwerk-route` 192.168.178.0/24 via de NAS (alleen eigen-apparaten).

## Posture checks
- "OS actueel" op eigen/SSH/exit/familie.
- "Europa + Kaapverdië" (52 landen, zonder RU/BY) op alle policies → [[Geo-blokkade]].
- Nooit een NetBird-versiecheck op eigen-apparaten: de iPhone-client heeft versie `ci-…`.
