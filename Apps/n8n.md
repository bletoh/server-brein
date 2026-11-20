---
tags: [app, docker, automatisering]
map: /srv/docker/n8n
domein: n8n.benjaminhashi.nl
---
# n8n

Workflow-automatisering (v2.43), op [[n8n.benjaminhashi.nl]].

| | |
|---|---|
| Containers | `n8n-n8n-1` (n8nio/n8n) + `n8n-postgres-1` (eigen build: postgres:16 + Percona pg_stat_monitor, sinds 2026-11-20, zie [[Grafana]]) |
| Netwerken | `books-net` + `web` (om apps direct te checken, [[Geo-blokkade]]) |
| Poort | `127.0.0.1:5678` (alleen lokaal; webhook voor [[n8n-daily-stats.sh]]) |
| Data | `./data` (config met encryption key!), `./postgres-data` |
| Onderhoud | dode rijen opruimen: `VACUUM (ANALYZE)` als user n8n (laatst 2026-11-20), zie [[Grafana]] → Databasemonitoring |
| Speciaal | `NODE_FUNCTION_ALLOW_BUILTIN=dgram,crypto` (RakNet-ping + Discord-handtekening) |

## Flows
Bron in `/srv/n8n-flows` → [[n8n-flows]]:
- [[Uptime-alarm]] — elke minuut alle sites
- [[Dagelijks serverrapport]] — 07:00
- [[Minecraft-alarm (Discord)]] — Bedrock ≥2 min offline
- [[Discord status-commando]] — `/status` in Discord

Meldingen gaan als push via **ntfy.sh** (Gmail-SMTP lukte niet: geen app-wachtwoorden).

## Tips
- Testen via CLI: `n8n execute` werkt alleen met een Execute Workflow Trigger en andere poorten (`N8N_RUNNERS_BROKER_PORT=5690 N8N_PORT=5699`).
- `docker cp` laat root-bestanden achter → opruimen met `docker exec -u root`.

Backup: [[app-backups.sh]] (pg_dump + data + flows).
