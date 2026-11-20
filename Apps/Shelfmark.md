---
tags: [app, docker, uit]
map: /srv/docker/shelfmark
domein: books-download.benjaminhashi.nl
---
# Shelfmark (staat uit)

Boeken zoeken en downloaden naar de [[Calibre-web]]-bibliotheek. Compose-project `downloader`, image `ghcr.io/calibrain/shelfmark`, poort 8084, netwerk `downloader_default`. Bewust niet in `APPS=` van [[weekly-update.sh]]/[[ensure-apps-up.sh]]. Router [[books-download.benjaminhashi.nl]] bestaat nog in [[Traefik]].

Starten: `cd /srv/docker/shelfmark && sudo docker compose up -d`.
