---
tags: [automatisering, n8n, minecraft]
---
# Discord status-commando

> [!note] Sinds 2026-10-31
> Statistieken komen van `http://10.43.100.50/live/...` (k3s-kaart). → [[Minecraft op k3s]]

Interactions-endpoint `https://n8n.benjaminhashi.nl/webhook/discord-minecraft` voor de slash-command `/status` van de Discord-app. Controleert de Ed25519-handtekening (public key in `.discord-public-key`) en antwoordt meteen met het ping-resultaat van de [[Bedrock-server]].

Dezelfde Discord-webhook wordt gebruikt voor de economie-aankondiging ([[Economie en winkel]]). Onderdeel van [[n8n-flows]].
