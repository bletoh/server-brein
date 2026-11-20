---
tags: [beveiliging, tls]
---
# Certificaten (Let's Encrypt)

- **[[Traefik]]**: ACME http-01 (resolver `le`, e-mail eigenaar), opslag `acme.json` in volume `traefik_traefik_certs`. Voor: [[reismannetje.nl]], [[benjaminhashi.nl]], [[netbird.benjaminhashi.nl]], [[books-download.benjaminhashi.nl]], en [[mc.benjaminhashi.nl]] (alleen voor NetBird-peers).
- **[[NetBird reverse proxy]]**: eigen certificaten voor alle proxy-services (volume `netbird_netbird_proxy_certs`).
- Geldigheid wordt dagelijks gerapporteerd door [[n8n-daily-stats.sh]] (dagen tot verlopen).
- Valkuil: Traefik probeert een mislukte ACME-aanvraag niet opnieuw tot de config echt verandert.

Backups: [[app-backups.sh]] (traefik, netbird).
