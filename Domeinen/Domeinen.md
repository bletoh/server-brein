---
tags: [moc, domein]
---
# Domeinen

> [!note] Sinds 2026-10-31
> Nieuw: reismannetje-test.benjaminhashi.nl (Traefik, basic auth, noindex) → [[Reismannetje op k3s]]

DNS bij **OVH**. A-records → `57.129.67.6`; `*.benjaminhashi.nl` wildcard en `*.proxy` CNAME → `proxy.benjaminhashi.nl`.

| Domein | Route | App | Toegang |
|---|---|---|---|
| [[benjaminhashi.nl]] (+www) | - | geen site (blog verwijderd 26-10) | 404 |
| [[reismannetje.nl]] (+www) | Traefik direct | [[Reismannetje]] | publiek, eigen accounts |
| [[vakantieplanner.benjaminhashi.nl]] | Traefik redirect | → reismannetje.nl | 301 |
| [[mc.benjaminhashi.nl]] | proxy (peers direct) | [[Bedrock-kaart]] + [[Vriendenpaneel]] | publiek + geo |
| [[minecraft.benjaminhashi.nl]] | UDP 19132 | [[Bedrock-server]] | publiek |
| [[n8n.benjaminhashi.nl]] | proxy | [[n8n]] | publiek + geo |
| [[books.benjaminhashi.nl]] | proxy | [[Calibre-web]] | publiek + geo |
| [[books-download.benjaminhashi.nl]] | Traefik direct | [[Shelfmark]] | (uit) |
| [[netbird.benjaminhashi.nl]] | Traefik direct | [[NetBird]] | publiek (login) |
| [[monitor.benjaminhashi.nl]] | proxy | [[nb-monit]] | SSO |
| [[bsm.benjaminhashi.nl]] | proxy | [[Bedrock Server Manager]] | SSO + geo |
| [[nas.benjaminhashi.nl]] | proxy | [[backupnas (Synology)]] | SSO + geo |
| [[proxy.benjaminhashi.nl]] | proxy | [[NetBird reverse proxy]] | — |

Gecontroleerd door: [[ensure-apps-up.sh]] (SITES), [[n8n-daily-stats.sh]] (certs), [[NAS app-check]], [[n8n-flows]] (Uptime-alarm).
