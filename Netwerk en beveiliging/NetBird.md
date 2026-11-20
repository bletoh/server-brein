---
tags: [netwerk, vpn, docker]
map: /srv/docker/netbird
---
# NetBird

Self-hosted WireGuard-mesh-VPN (server 0.80+, client 0.81.2). Bereikbaar op [[netbird.benjaminhashi.nl]].

## Onderdelen (compose `netbird`)
| Container | Rol |
|---|---|
| `netbird-server` | combined: management + signal + relay + STUN (3478/udp), config `config.yaml` |
| `netbird-dashboard` | web-UI |
| `netbird-proxy` | [[NetBird reverse proxy]] — publiceert apps met SSO/geo/CrowdSec |

Data in volume `netbird_netbird_data` (`store.db`, `idp.db`, `events.db`). `trustedHTTPProxies` = `172.19.0.0/16` (books-net, [[Traefik]]).

## Deze server als peer
- Peer "OVH VPS", IP `100.109.21.192`, interface `wt0`, NetBird-SSH aan.
- Is **exit node** (route `exit-node-ovh` 0.0.0.0/0, optioneel per apparaat).
- DNS-beheer uit op de host → [[DNS-resolver]].

## Toegang en beheer
- Groepen/policies/posture/geo: [[NetBird ACL en groepen]], apparaten: [[Apparaten]].
- API: service-user "automation", token in `/srv/docker/netbird/api-token` (root 600); helper [[nb-api]]. [[nb-monit]] gebruikt hetzelfde token.
- SSO voor beheerapps via NetBird-IdP (groep `beheerders`).

## Regels
- Geen HTTP/3 op Traefik (relay-QUIC), zie [[Traefik]].
- De Claude-autoclassifier blokkeert sommige API-acties (DELETE, services aanmaken, owner-groepen) → eigenaar doet die in het dashboard. Zie [[Claude Code sessies]].

Backup: [[app-backups.sh]] (netbird).
