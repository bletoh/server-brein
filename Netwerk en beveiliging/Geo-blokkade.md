---
tags: [beveiliging, netwerk, valkuil]
---
# Geo-blokkade

De [[NetBird reverse proxy]]-services hebben `allowed_countries` = Europa (zonder RU/BY) + Kaapverdië. Dezelfde lijst zit als posture check op de [[NetBird ACL en groepen|NetBird-policies]].

## Het probleem
Verkeer zonder land krijgt `403 country_restricted`:
- **containers op deze server** die een publieke URL opvragen (hairpin-NAT → bron `172.19.0.1`);
- **NetBird-peers** (bron `100.109.x.x`), bijv. de laptop op de exit node.

## Oplossingen per geval
| Waar | Oplossing |
|---|---|
| [[n8n-flows]] uptime-checks | apps direct op containernaam checken (`calibre-web:8083`, `reismannetje:4000`, …); n8n zit op netwerk `web` |
| [[ensure-apps-up.sh]] | accepteert 403 als "draait" (bewijst dus minder) |
| [[mc.benjaminhashi.nl]] | Traefik-split: peers → direct naar `bedrock-map`, rest → proxy (zie [[Traefik]]) |
| [[monitor.benjaminhashi.nl]] | geo verwijderd (SSO blijft) — 2026-10-17 |
| n8n, bsm, nas, books | nog steeds 403 voor NetBird-clients |

> [!warning] `allowed_cidrs` is geen uitzondering
> Het is een extra allowlist (EN-voorwaarde met landen). Toevoegen maakte mc voor iedereen onbereikbaar.

Zie [[Valkuilen en lessen]].
