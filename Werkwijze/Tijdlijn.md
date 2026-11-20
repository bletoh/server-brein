---
tags: [werkwijze, tijdlijn]
---
# Tijdlijn

| Datum (2026) | Gebeurtenis |
|---|---|
| jun–sep | VPS draait met Caddy, NetBird, Calibre-web, n8n, GitLab, pm2-apps |
| 03-10 | Alles naar `/srv/docker` ([[Mappenstructuur]]); [[weekly-update.sh]] + [[ensure-apps-up.sh]]; Pro Clubs-site en Discord-bot verwijderd; addon [[Addon Homes & Teleport]] |
| 05-10 | [[Addon Handige Extra's]]; [[Groepen en chat]] in de vakantieplanner |
| 06-10 | Vakantieplanner productie-klaar: tests, healthz, backups ([[reismannetje-backup.sh]]), echte prijzen |
| 11-10 | DNS-fix ([[DNS-resolver]]); [[Claude Code sessies]] per onderwerp |
| 12-10 | Caddy → [[Traefik]]; [[CrowdSec]]; [[NetBird reverse proxy]]; [[NetBird ACL en groepen]]; [[n8n-flows]] met ntfy en Discord |
| 13-10 | [[Bedrock-kaart]] + stats; geo-filter; casino, kliniek, arena, atoombom en herstel |
| 14-10 | Hernoemd naar [[Reismannetje]] op [[reismannetje.nl]]; PWA; bestemmingsgids; [[Vriendenpaneel]]; alles Minecraft onder [[mc.benjaminhashi.nl]]; [[Demodorp]] |
| 17-10 | [[Blog (Ghost)]] op [[benjaminhashi.nl]]; [[app-backups.sh]] voor alle apps; boomhut; chaos-middag + herstel; tick-distance 12; mc-fix voor NetBird-peers |
| 19-10 | Economie, centrale winkel, dynamische prijzen; kaartlagen; Minecraft-thema; Reismannetje nieuwe stijl |
| 20-10 | [[Mijnhoogte en ertsscan]]; CrowdSec-whitelist Ghost |
| 21-10 | Reismannetje Airbnb-stijl + OpenFreeMap-vectorkaart |
| 22-10 | Reisvenster/reisstand, wie betaalt wat, centrale pagina, demo-video's |
| 23-10 | Solo-groepen, budget weg, rondreis, tickets + prijsalarm, swipen, beveiligingsaudit, planavond; deze vault |
| 26-10 | Tickets koppelen aan programma; blog verwijderd; [[Geheugen]]: limieten per container, loadmon per app, logs bewaard; Node2Shell (CVE-2026-111497): Reismannetje en nb-monit naar Node 24 |
| 27-10 | Bedrock 1.26.60 met auto-update (mc-autoupdate, poortcheck, xboxcheck, hersteltest, terugdraai); MCXboxBroadcast (PS5 via Xbox-vriendenlijst, NetherNet); 30% XP-verlies bij dood; gevelborden Bibliotheek en Grasshopper |
| 28-10 | Naam Glanerbrugcraft; griefinglog (/wiedeed, /terugdraaien); hele [[mc.benjaminhashi.nl]] achter het gedeelde wachtwoord met tabbladen Kaart/Ranglijst/Borden/Beheer; eigen borden van vrienden |
| 29-10 | glanerbrugcraft-repo met `deploy.py` en auto-deploy; Reismannetje "Voor thuis" (ouderfunctie) |
| 30-10 | Reismannetje-mail via ImprovMX (Instagram) |
| 31-10 | [[Kubernetes (k3s)]]: Reismannetje en daarna alles rond Minecraft naar k3s; [[Flux en GitOps]], [[Lokale registry]], testomgeving en zero-downtime deploys ([[Reismannetje op k3s]]); hardening en NetworkPolicies, NetBird-mark-valkuil ([[k3s-beveiliging]]); [[Minecraft op k3s]]; [[Monitoring en meldingen]] met eigen Discord-kanaal en NAS-check van buitenaf; [[k3s-onderhoud]]; Reismannetje-image 961 → 492 MB; Traefik-logrotate gerepareerd |
| 01-11 | SELinux-valkuil in `deploy.py` (copy2 nam `user_home_t` mee) ([[Valkuilen en lessen]]) |
| 02-11 | [[dagelijkse-opruiming.sh]] (18:00); Bedrock lag-optimalisatie (tick-distance 10, lagmeter); Discord-meldingen worden na 12 uur gewist; `deploy.py` draait lokale commits terug, dus eerst pushen |
| 04–09-11 | Reismannetje: nieuwe Voor thuis, instapkaart, automatisch prijsalarm ([[Reismannetje wijzigingen november 2026]]) |
| 10/11-11 | [[Home-incident 2026-11-10]]: home per ongeluk verplaatst en hersteld |
| 11/12-11 | Reismannetje: echte vluchtroutes, Ontdekken-lijst, lanceerplan, nieuwe tabs |
| 12-11 | Home opgeruimd naar `~/archief` ([[Mappenstructuur]]); CPU-voorrang Reismannetje prod > MC > test, MC-jobs minder vaak, kaart alleen renderen na spelen ([[Geheugen]]) |
| 13-11 | Camera-opnames afspeelbaar via [[camera-afspeelbaar.sh]]; Reismannetje [[Gebruiksanalyse]], evenementen weg |
| 14–17-11 | Reismannetje: Uit het raam, samen boeken, [[Kladblok]] |
| 19-11 | [[Minecraft uit (november 2026)]]: alles rond Minecraft tijdelijk uit |
| 20-11 | Vault in git; [[Grafana]] (Prometheus, node-exporter, cAdvisor) vervangt de loadmon-pagina op [[load.benjaminhashi.nl]]; firewallregel 015; databasemonitoring met Percona pg_stat_monitor (dashboard Databases); n8n-database gevacuumd (dode rijen opgeruimd); [[Agents]]: Grafana-alerts naar ntfy, dagelijkse onderhoudsagent en wekelijkse Reismannetje-agent; eerste punten van [[Openstaand]] opgepakt: Flux v2.10.0 + flux-update gerepareerd, Minecraft-pauze in Git, Reismannetje-fix Airbnb-502 + npm audit 0 live (00eb0f9); Reismannetje: Airbnb-502-fix + npm audit 0 (`00eb0f9`) en Wereldkaart met plekken als strook, paneel zonder dubbelingen, Groep gecentreerd op laptop (`2a37a42`), beide live; zie [[Kaart (MapLibre)]] |
