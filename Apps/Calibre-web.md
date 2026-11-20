---
tags: [app, docker]
map: /srv/docker/calibre-web
domein: books.benjaminhashi.nl
---
# Calibre-web

E-boekenbibliotheek op [[books.benjaminhashi.nl]]. Image `lscr.io/linuxserver/calibre-web` (+ mod `universal-calibre`), compose-project `ebooks`, netwerk `books-net`, poort 8083 intern.
- Data: `./config` (`app.db` = gebruikers/instellingen), `./books` (bibliotheek met `metadata.db`).
- Boeken toevoegen kan via [[Shelfmark]] (staat uit), die naar `../calibre-web/books` schrijft.
- Publiek via de [[NetBird reverse proxy]] (geo).
- Backup: [[app-backups.sh]] (calibre-web, incl. boeken).
