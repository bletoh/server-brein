---
tags: [server]
---
# Mappenstructuur

> [!note] Sinds 2026-10-31
> Nieuw: `/srv/k8s` (gitops-werkkopie, data van Reismannetje prod/test, registry, Flux-sleutel, README) en `/etc/rancher/k3s`. → [[Kubernetes (k3s)]]

Sinds 2026-10-03 staat alles op één vaste plek (verhuisd uit `/var/ebooks`, `/root/n8n`, `/opt/...`). Overzicht in `/srv/README.md`.

```
/srv/
├── README.md              ← overzicht van de server (bron van waarheid op de server zelf)
├── docker/<app>/          ← één map per Docker-app: compose.yml, .env (root 600), data
│   ├── traefik/           → [[Traefik]]
│   ├── crowdsec/          → [[CrowdSec]]
│   ├── netbird/           → [[NetBird]]
│   ├── n8n/               → [[n8n]]
│   ├── calibre-web/       → [[Calibre-web]]
│   ├── shelfmark/         → [[Shelfmark]] (uit)
│   ├── nb-monit/          → [[nb-monit]]
│   ├── reismannetje/      → [[Reismannetje]] (git-repo)
│   ├── bedrock-map/       → [[Bedrock-kaart]]
│   └── vriendenpaneel/    → [[Vriendenpaneel]]
├── backups/               → [[srv-backups]]
├── archive/               ← oude Caddy, GitLab, origineel nb-monit
├── n8n-flows/             → [[n8n-flows]] (bron van de flows)
└── nas-check/app-check.sh → [[NAS app-check]]

/usr/local/sbin/           ← root-scripts: [[weekly-update.sh]], [[ensure-apps-up.sh]], [[app-backups.sh]],
                             [[reismannetje-backup.sh]], [[n8n-daily-stats.sh]], [[dagelijkse-opruiming.sh]]
/etc/cron.d/               → [[Cron-planning]]
/opt/bsm-venv, /opt/bsm-data → [[Bedrock Server Manager]]

/home/almalinux/
├── bin/                   → [[Scripts in ~-bin]] (kaart, collector, paneel-worker, ertsscan, nb-api)
├── apps/unmined → unmined-cli_0.20.11-dev   → [[uNmINeD]]
├── apps/map-work/         ← werkmap kaart: wereldkopie, JSON-state, voor-*.js/html backups, chunk-merge
├── .config/bedrock-server-manager/   → [[Bedrock-server]] (servers, backups, addons)
├── .config/nas-check/     ← SSH-sleutel naar de NAS, zie [[backupnas (Synology)]]
└── archief/               ← opgeruimd uit ~ op 2026-11-12 (LEESMIJ.md): oude sessielogs, media (incl. demo-video's),
                             downloads, wegwerp-klonen, herstel-20261111 ([[Home-incident 2026-11-10]]). Niets gebruikt, mag weg.
```

Regel: een nieuwe app krijgt een eigen map onder `/srv/docker`, een vaste `name:` in compose, en komt in `APPS=` van [[weekly-update.sh]] en [[ensure-apps-up.sh]] en in [[app-backups.sh]].
