---
tags: [app, docker, vpn]
map: /srv/docker/nb-monit
domein: monitor.benjaminhashi.nl
---
# nb-monit (NetBird-monitor)

Kleine Express-app die de status van alle [[NetBird]]-peers toont (online/offline, IP, last seen, OS, groep). Op [[monitor.benjaminhashi.nl]] achter SSO.
- Eigen build (`node:20-alpine`, `server.js` + `public/`), netwerk `web`, poort 3001.
- Login met eigen gebruiker + bcrypt-hash (`AUTH_PASS_HASH` in `.env` — **tussen enkele quotes** vanwege `$`, zie [[Valkuilen en lessen]]).
- Leest de NetBird-API met het token van de automation-user ([[Geheimen]]).
- Was eerst een pm2-proces; origineel in `/srv/archive/nb-monit-origineel`.
- Backup: [[app-backups.sh]] (kleine-apps).
