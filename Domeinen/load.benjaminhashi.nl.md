---
tags: [domein]
---
# load.benjaminhashi.nl

[[Grafana]] (sinds 2026-11-20; daarvoor de eigen loadmon-pagina). Via [[NetBird reverse proxy]] met **SSO** (groep `beheerders`) en CrowdSec. Doel `loadmon:8080` = alias van de grafana-container. Traefik geeft de SNI door (passthrough in `dynamic/netbird.yml`). Verwacht 302 → NetBird-oauth2 ([[NAS app-check]], [[ensure-apps-up.sh]]).
