---
tags: [agent, moc, werkwijze]
aliases: [Claude-agents, Onderhoudsagent, Reismannetje-agent]
---
# Agents

Sinds 2026-11-20 werken er drie dingen proactief op de server zonder dat de eigenaar online hoeft te zijn. Ontwerpregel: **agents analyseren en stellen voor, ze veranderen niets aan de server**. Uitvoeren gebeurt in een interactieve sessie ("pak punt X van [[Openstaand]] op", "voer voorstel 2 van week 2026-W47 uit").

| Wat | Wanneer | Doet | Uitvoer |
|---|---|---|---|
| Grafana-alerts | continu (elke minuut) | 10 regels: schijf, schijf-voorspelling, geheugen, load, systemd-failed, meetbron weg, Postgres weg, OOM, SQLite-WAL, SQLite-meting stil | push via ntfy (en zo in Discord) bij alarm en bij herstel, zie [[Grafana]] |
| Onderhoudsagent | dagelijks 07:30 | analyseert de dagsnapshot: resources, alerts, journal-fouten, containers, k3s, Postgres, back-ups, updates, certificaten, CrowdSec | `Agents/Onderhoud/JJJJ-MM-DD.md` + sectie Server in [[Openstaand]] + push |
| Reismannetje-agent | zondag 10:00 | 5xx/trage routes met oorzaak in de code, npm audit, werkt `Reismannetje/ideen.md` uit tot plannen, top-3 voorstellen | `Agents/Reismannetje/JJJJ-Www.md` + sectie Reismannetje in [[Openstaand]] + push |

## Hoe het werkt
1. **Feiten verzamelen (root, alleen lezen):** `/usr/local/sbin/agent-snapshot.py onderhoud|reismannetje` → `/var/lib/claude-agent/<modus>.md`. Bronnen: Prometheus, Grafana-API, journal, docker, kubectl, Postgres (pg_stat_monitor), Traefik-accesslog, app-log, git, npm audit (in een node-container), SQLite-tellingen (via een `.backup`-kopie).
2. **Analyseren (almalinux, headless Claude):** `~/bin/claude-agent.sh <modus>` draait `claude -p` met `--permission-mode dontAsk`. Mag alleen: Read/Glob/Grep (vault, snapshot, en voor Reismannetje de code in `/srv/docker/reismannetje`) en bewerken binnen `~/server-brein/Agents/`. Geen Bash, geen web, geen `.env`/sleutels. Model: Sonnet voor onderhoud, Opus voor Reismannetje. Max. 45 minuten, lock per modus.
3. **Afronden:** commit + push van `Agents/` (vault), push-melding met de samenvatting naar ntfy. Log: `~/.local/state/claude-agent/<modus>.log`.

Cron: `/etc/cron.d/claude-agents` (zie [[Cron-planning]]).

## Aanpassen
- De opdrachten staan in de vault en worden elke run opnieuw gelezen: [[Opdracht onderhoud]] en [[Opdracht reismannetje]]. Zo kun je vanuit Obsidian sturen wat de agents doen.
- Nieuwe ideeën voor Reismannetje: zet ze in `Reismannetje/ideen.md`; de agent werkt ze zondag uit.
- Handmatig draaien: `sudo /usr/local/sbin/agent-snapshot.py onderhoud && ~/bin/claude-agent.sh onderhoud`.
- Een nieuwe agent (bv. voor n8n): sectie toevoegen in `agent-snapshot.py`, een `Opdracht <modus>.md` maken en een cronregel.

## Waarom zo
- Een agent met shell en sudo op productie zonder toezicht is te riskant (zie [[Home-incident 2026-11-10]]). Daarom verzamelt een vast script de feiten en kan de agent alleen lezen en schrijven in zijn eigen map.
- Alles wat de agent schrijft komt in git, dus elke wijziging is terug te zien en terug te draaien.
