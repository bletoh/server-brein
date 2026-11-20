---
tags: [server, netwerk, dns]
---
# DNS-resolver (op de host)

Sinds 2026-10-11 beheert NetBird de DNS op deze host **niet** meer (`netbird up --disable-dns`, staat in het profiel).

- `/etc/resolv.conf` handmatig: OVH `213.186.33.99` + `1.1.1.1`.
- NetworkManager: `dns=none`.
- Gevolg: `*.netbird.selfhosted` lost op de host niet op → gebruik NetBird-IP's (bijv. NAS `100.109.137.157`).
- Daarvoor duurde elke lookup 2,5–5 s (NetBird-resolver zonder upstreams). Daarom gebruikt [[Reismannetje]] in compose nog steeds `dns: 1.1.1.1, 9.9.9.9`.
- Backup van de oude situatie: `/srv/backups/dns-20261011`.

Voor publieke DNS-records (bij OVH) zie [[Domeinen]]. Gerelateerd: [[NetBird]], [[Valkuilen en lessen]].
