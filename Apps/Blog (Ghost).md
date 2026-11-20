---
tags: [app, docker]
map: /srv/docker/blog
domein: benjaminhashi.nl
---
> **Verwijderd op 2026-10-26** op verzoek van de eigenaar (geheugen besparen). Laatste stand: `/srv/archive/blog-20261026` (ghost.sql + blog-map.tar.gz). Hieronder de oude situatie, ter naslag.

# Blog (Ghost)

Persoonlijke blog op [[benjaminhashi.nl]] (sinds 2026-10-17). Nog leeg: de eigenaar schrijft zelf.

| | |
|---|---|
| Containers | `blog` (ghost:6-alpine, v6.71) + `blog-db` (mysql:8.4, healthcheck) |
| Netwerken | `books-net` (voor Traefik) + `blog-intern` (alleen DB) — [[Docker-netwerken]] |
| Data | `./content` (foto's, thema's), volume `blog_db` |
| Instellingen | locale nl, aanmelden leden uit, `staffDeviceVerification` uit (geen SMTP) |
| Eigenaar-account | aangemaakt via setup-API; startwachtwoord in `~/.config/blog-ghost-wachtwoord` → wijzigen! |
| Route | [[Traefik]] direct, router `blog` / `blog-www` |

## Beheer-API vanaf de host
`curl -k --resolve benjaminhashi.nl:443:127.0.0.1` met Origin-header + sessiecookie (cookie is Secure-only, dus niet via http naar de container). `curl -g` voor `filter=[..]`.

## Backup
[[blog-backup.sh]] om 01:45 (mysqldump + content) → [[srv-backups]] en [[backupnas (Synology)]].

## Valkuil
Inloggen in `/ghost/` leek voor [[CrowdSec]] op admin-probing → ban op alle sites. Opgelost met een whitelist.

## Ideeën (nog niet gebouwd)
Sport- en reisfuncties: tags `sport`/`reizen` met collections in `routes.yaml`, Strava-koppeling, kaart met reizen. Link met [[Reismannetje]] ligt voor de hand.
