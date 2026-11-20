---
tags: [automatisering, script, monitoring]
bestand: /usr/local/sbin/ensure-apps-up.sh
---
# ensure-apps-up.sh

> [!note] Sinds 2026-10-31
> Kijkt ook naar de `k3s`-service, de Reismannetje-deployment, de mc-pods en of alle Flux-objecten Ready zijn. De worker-services zijn sidecars geworden. → [[k3s-onderhoud]]

> [!warning] Sinds 2026-11-19
> Zolang `/etc/minecraft-uit` bestaat, slaat het script BSM, de mc-pods en de bsm/mc-sitechecks over. → [[Minecraft uit (november 2026)]]

Na elke boot (+120 s), maandag 04:00 en elk uur op :30 (`--quiet`). Log in `/var/log/weekly-update.log`.

1. Services `docker`, `netbird`, `bedrock-server-manager-webui`, `vriendenpaneel-worker` starten als ze niet draaien ([[Systemd-services]]).
2. Per compose-app: draaien er minder containers dan gedefinieerd → `up -d`.
3. Wacht tot `bedrock_server` draait (max 3 min), anders BSM herstarten.
4. Test `SITES`: books, netbird, monitor, n8n, bsm, mc, reismannetje.nl, benjaminhashi.nl — 2xx/3xx/401/403 = goed (403 vanwege [[Geo-blokkade]]).

Zie [[weekly-update.sh]], [[Domeinen]], [[Uptime-alarm]].
