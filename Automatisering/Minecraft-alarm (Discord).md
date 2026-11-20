---
tags: [automatisering, n8n, minecraft]
---
# Minecraft-alarm (Discord)

> [!note] Sinds 2026-10-31
> `mcping.js` leest de live-kaart via `http://10.43.100.50/live` (k3s). → [[Minecraft op k3s]]

n8n-flow: elke minuut een RakNet-ping (UDP, `mcping.js`) naar [[minecraft.benjaminhashi.nl]]:19132. Post in Discord **alleen** als de [[Bedrock-server]] ≥ 2 min offline is (op verzoek geen live-status en geen herstelbericht). Webhook-URL in `.discord-webhook`.

Onderdeel van [[n8n-flows]]. Zie ook [[Discord status-commando]].
