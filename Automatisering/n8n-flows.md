---
tags: [automatisering, n8n, moc]
map: /srv/n8n-flows
---
# n8n-flows

> [!note] Sinds 2026-10-31
> Kaart- en Reismannetje-checks wijzen naar k3s-ClusterIP's (10.43.100.40 en 10.43.100.50). Elke ntfy-melding komt ook in het Discord-serverkanaal. → [[Monitoring en meldingen]]

Bron van de flows in `/srv/n8n-flows` (eigenaar almalinux). `python3 -I build.py` maakt de JSON van losse `.js`-bestanden; importeren overschrijft op id, daarna `n8n publish:workflow --id=ID` + n8n herstarten.

| Flow | Id | Wat |
|---|---|---|
| [[Uptime-alarm]] | UptimeAlarmBH01 | elke minuut alle apps |
| [[Dagelijks serverrapport]] | ServerRapportBH1 | 07:00 rapport |
| [[Minecraft-alarm (Discord)]] | MinecraftStatus1 | Bedrock offline → Discord |
| [[Discord status-commando]] | DiscordStatusCmd | `/status` in Discord |

Bestanden: `checks.js`, `uptime.js`, `report.js`, `mcping.js`, `minecraft.js`, `discord-status.js`, plus geheime `.discord-*`-bestanden ([[Geheimen]]). Meldingen via **ntfy.sh** (push-app, topic als geheim).

Zie [[n8n]].
