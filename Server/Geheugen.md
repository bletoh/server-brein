# Geheugen

> [!note] Sinds 2026-10-31
> k3s gebruikt ongeveer 500 MB, Flux ongeveer 100 MB. loadmon toont k8s-pods via `loadmon-containers.sh` (crictl), bijvoorbeeld "Minecraft-server (k8s)". → [[Monitoring en meldingen]]

Na een herstart gebruikte de server ~27% geheugen; daarna liep het langzaam op tot ~45%. Wat er vóór de herstart vastzat was niet meer na te gaan, dus op 2026-10-26 is ingesteld:

- **Limiet per container**: elk compose-bestand heeft `mem_limit` (n8n 1,5 GB; Reismannetje en [[Calibre-web]] 1 GB; [[Traefik]], [[CrowdSec]], NetBird, postgres 512 MB; kleine apps 128-256 MB). Een lek herstart alleen die app. Oude compose-bestanden: `/srv/backups/compose-*.voor-geheugenlimiet-20261026.yml`.
- **Meten per app**: loadmon (load.benjaminhashi.nl, kaart "Geheugen per app") slaat elke 5 minuten het eigen geheugen (RssAnon+RssShmem) per container of programma op; oranje = gegroeid in de gekozen periode. Containernamen uit `/srv/docker/loadmon/data/containers.json`, elke 5 min geschreven door `/etc/cron.d/loadmon-containers`.
- **Logs bewaren**: `/etc/systemd/journald.conf.d/bewaren.conf` (persistent, max 1 GB, 2 maanden) → `journalctl -b -1` voor de vorige boot.
- **Minder zinloos werk**: `dnf-makecache.timer` uit; [[Bedrock-kaart]] kopieert de wereld met rsync; [[Vriendenpaneel]]-worker leest de serverlog alleen als die veranderd is; rate-limit-tabellen in kaart-API, vriendenpaneel en [[nb-monit]] (sessies) worden opgeruimd; nginx gzip-niveau 9 → 5; Reismannetje gooit verlopen caches dagelijks weg.
- [[Blog (Ghost)]] verwijderd (MySQL alleen al ~530 MB).

Let op: [[weekly-update.sh]] herstart de server alleen als `dnf needs-restarting -r` dat vraagt, dus niet elke week.

## CPU-voorrang (2026-11-12)
Doel: Reismannetje gaat voor, de mc-site mag deels afgeschaald worden. In rust was de CPU al ~4%; pieken komen van Claude-sessies en Playwright-containers.
- k8s (gitops a1bf31c): CPU-request Reismannetje prod 2 (mem 384Mi), bedrock 2 → 1, reismannetje-test 100m.
- MC-CronJobs minder vaak: kaart-render */10, kaart-collect */3, mijlpalen */5, weer */15 (k3s.service van 13-18% naar ~9% van een core).
- [[bedrock-map.sh]] slaat het renderen over als er geen spelers zijn en de vorige render ook leeg was (marker `~/apps/map-work/render-zonder-spelers`).
- Host: `docker update --cpu-shares 4096 traefik` + `cpu_shares` in compose; `user.slice` en `claude-remote-control.service` CPUWeight=40, IOWeight=40.

Volgorde van voorrang: Reismannetje prod > Minecraft > Reismannetje test. Zie [[Minecraft op k3s]], [[Reismannetje op k3s]].
