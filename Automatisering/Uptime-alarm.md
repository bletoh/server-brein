---
tags: [automatisering, n8n, monitoring]
---
# Uptime-alarm

> [!note] Sinds 2026-10-31
> De checks voor Reismannetje gebruiken de k3s-ClusterIP `10.43.100.40:4000`. Alle meldingen komen ook in het Discord-serverkanaal. → [[Monitoring en meldingen]]

n8n-flow, elke minuut. Checkt de apps **direct** op het Docker-netwerk of NetBird-IP (calibre-web:8083, n8n, nb-monit:3001, reismannetje:4000, bsm/nas via NetBird-IP) plus één `proxy`-check die 302/403 accepteert — vanwege de [[Geo-blokkade]]. Pusht via ntfy na 3 keer falen (≥ 2 min down) en één keer bij herstel. Status in workflow static data; geslaagde runs worden niet opgeslagen.

Onderdeel van [[n8n-flows]]. Verwant: [[ensure-apps-up.sh]], [[NAS app-check]].
