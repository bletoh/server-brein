---
tags: [beveiliging]
---
# Geheimen — wáár ze staan (niet wát)

> [!danger] Deze vault bevat bewust geen wachtwoorden of tokens.

| Geheim | Locatie | Gebruikt door |
|---|---|---|
| App-secrets per app | `/srv/docker/<app>/.env` (root 600) | [[Docker]] |
| NetBird API-token | `/srv/docker/netbird/api-token` (PAT, vernieuwd 2026-11-20; verlopen token geeft 401 → nieuwe maken in het dashboard) | [[nb-api]], [[nb-monit]] |
| Grafana-admin | `/srv/docker/grafana/.env` (`GF_SECURITY_ADMIN_PASSWORD`) | [[Grafana]] |
| Postgres-rol `monitoring` | `/srv/docker/grafana/.env` (`PG_MONITOR_PASSWORD`) | [[Grafana]] (exporter + datasource) |
| NetBird proxy-token | `/srv/docker/netbird/proxy.env` | [[NetBird reverse proxy]] |
| CrowdSec bouncer-keys | `/srv/docker/crowdsec/.env`, `traefik/dynamic/middlewares.yml` | [[CrowdSec]] |
| n8n encryption key + DB | `/srv/docker/n8n/.env` | [[n8n]] |
| Discord webhook / public key | `/srv/n8n-flows/.discord-webhook` (600), `.discord-public-key` | [[n8n-flows]] |
| ntfy-topic | in de flows/README (`/srv/n8n-flows`) — de topicnaam is het geheim | [[n8n-flows]] |
| Vriendenpaneel-wachtwoord | `/srv/docker/vriendenpaneel/wachtwoord.txt` (600), hash in `.env` en Secret `mc/vriendenpaneel-env` | [[Vriendenpaneel]] |
| Reismannetje SMTP/partnercodes/Travelpayouts | `/srv/docker/reismannetje/.env`, in k3s als Secret `reismannetje-env` (prod en test) | [[Reismannetje op k3s]] |
| VAPID-sleutels (push) | `/srv/k8s/reismannetje/data/vapid.json` | [[PWA en push]] |
| NAS SSH-sleutel | `~/.config/nas-check/id_ed25519` | [[Backup-strategie]] |
| BSM-config | `~/.config/bedrock-server-manager/` | [[Bedrock Server Manager]] |
| Let's Encrypt-sleutels | `acme.json` in `traefik_traefik_certs` | [[Certificaten (Let's Encrypt)]] |
| Flux deploy key (read-only, branch k8s) | `/srv/k8s/flux/deploykey`, Secret `flux-system/github-k8s` | [[Flux en GitOps]] |
| Wachtwoord testomgeving Reismannetje | `/srv/k8s/reismannetje-test/wachtwoord` (root 600) | [[Reismannetje op k3s]] |
| Discord-webhook serverkanaal | `/srv/k8s/server-discord-webhook`, Secret `monitoring/ntfy-discord`, NAS `~/scripts/.discord-webhook` | [[Monitoring en meldingen]] |
| k3s-token en kubeconfig | `/var/lib/rancher/k3s/server/token`, `/etc/rancher/k3s/k3s.yaml` | [[Kubernetes (k3s)]] |

Alle k3s-Secrets gaan elke nacht als yaml mee in de backup `k3s` van [[app-backups.sh]].
