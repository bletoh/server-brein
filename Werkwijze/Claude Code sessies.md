---
tags: [werkwijze, claude]
---
# Claude Code sessies

Bijna alles op deze server is gebouwd met Claude Code (vanaf ±3 oktober 2026). De eigenaar praat in het Nederlands, vaak vanaf de telefoon.

## Vaste sessies per onderwerp (sinds 2026-10-11)
Minecraft Bedrock, Reismannetje, n8n, NetBird + nb-monit, Caddy/domeinen (nu [[Traefik]]), Calibre-web/Shelfmark, NAS & backups, Server-onderhoud. Ze draaien via [[claude-remote-control]].

## Geheugen
Claude houdt per onderwerp notities bij in `~/.claude/projects/-home-almalinux/memory/` (o.a. server-layout, bedrock-server, reismannetje-app, traefik-proxy). Deze vault is daar grotendeels op gebaseerd.

## Afspraken
- Configwijzigingen en deployen van Reismannetje mogen zonder te vragen; de eigenaar wil dat de server meer CPU gebruikt.
- Vóór elke wijziging een backup (`*.voor-*`).
- De auto-mode-classifier blokkeert sommige acties (NetBird-services aanmaken/verwijderen, geo weghalen, CrowdSec-whitelist, productie-DB kopiëren) → de eigenaar doet die zelf of zet auto mode uit.

Zie [[Valkuilen en lessen]], [[Tijdlijn]], [[Playwright-testen]].
