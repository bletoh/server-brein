---
tags: [domein, vpn]
---
# netbird.benjaminhashi.nl

Management, signal, relay en dashboard van [[NetBird]]. [[Traefik]] termineert TLS:
- gRPC (`Content-Type: application/grpc`) → `h2c://netbird-server:80`
- `/relay`, `/ws-proxy/`, `/api/`, `/oauth2/` → `netbird-server:80`
- rest → `netbird-dashboard:80` (met `site-default`)

Ook de SSO-loginpagina (`/oauth2`) voor alle proxy-services met SSO.
