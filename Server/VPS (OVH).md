---
tags: [server]
---
# VPS (OVH)

| | |
|---|---|
| Hostnaam | `vps-f1805963.vps.ovh.net` |
| Publiek IP | `57.129.67.6` (IPv6 `2001:41d0:701:1100::aa6f`) |
| NetBird-IP | `100.109.21.192` (interface `wt0`), zie [[NetBird]] |
| OS | AlmaLinux 9.8 (Olive Jaguar), kernel 5.14 |
| Virtualisatie | KVM / OpenStack Nova |
| CPU / RAM | 6 vCPU, 11 GiB RAM, geen swap |
| Schijf | 99 GB root (`/dev/sda4`), ±44% gebruikt |
| Gebruiker | `almalinux` (sudo); root-taken via `sudo` |

## Wat draait er
- **In Docker**: zie [[Docker]] — [[Traefik]], [[CrowdSec]], [[NetBird]], [[n8n]], [[Calibre-web]], [[Reismannetje]], [[nb-monit]], [[Bedrock-kaart]], [[Vriendenpaneel]].
- **Direct op de host** (systemd): [[Bedrock Server Manager]] met de [[Bedrock-server]], de NetBird-client, [[bedrock-map-queue.py]], [[vriendenpaneel-worker.py]], [[claude-remote-control]]. Zie [[Systemd-services]].

## Belangrijke plekken
- [[Mappenstructuur]] — `/srv/docker`, `/srv/backups`, `/usr/local/sbin`, `~/bin`, `~/apps/map-work`
- [[Firewall (iptables)]] en [[Poorten]]
- [[DNS-resolver]] (handmatig `/etc/resolv.conf`)
- [[Cron-planning]] — wat er wanneer automatisch gebeurt

## Onderhoud
- Wekelijks automatisch bijgewerkt en zo nodig herstart: [[weekly-update.sh]].
- Elk uur gecontroleerd: [[ensure-apps-up.sh]].
- Gebruik CPU: veel idle (±94%); de gebruiker wil dat er méér gebruikt wordt (gzip 9, tick-distance 12, kaart elke 5 min). Zie [[Valkuilen en lessen]].
