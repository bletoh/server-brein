---
tags: [kubernetes, minecraft]
aliases: [Minecraft k8s, mc-server, namespace mc]
---
# Minecraft op k3s

> [!warning] Sinds 2026-11-19 staat alles uit
> Flux gesuspend, deployments op 0, CronJobs gesuspend. Terug met `~/minecraft-weer-aan.sh`. → [[Minecraft uit (november 2026)]]

> [!note] deploy.py (november)
> Deploy kopieert met copyfile+copymode, zodat het SELinux-label niet wordt meegenomen (zie [[Valkuilen en lessen]]). `deploy.py` importeert eerst live → repo, dus: commit, push naar main, `git reset --hard HEAD~1`, dan `./deploy.py`. Een lokale wijziging live zetten zonder deploy: `cat repo-bestand > live-bestand`.

Sinds 2026-10-31 draait alles rond de [[Bedrock-server]] in [[Kubernetes (k3s)]], verdeeld over twee namespaces. De code blijft in de `glanerbrugcraft`-repo; `deploy.py` zet bestanden zoals altijd op de host-paden en herstart daarna de juiste pod of sidecar. De pods lezen die host-mappen rechtstreeks.

## Namespace `mc` (gehard)
| Deployment | Wat | Notitie |
|---|---|---|
| `bedrock-map` | kaartsite (nginx-unprivileged, poort 8080), ClusterIP **10.43.100.50:80** | [[Bedrock-kaart]], [[mc.benjaminhashi.nl]] |
| `bedrock-map-api` | warps beheren → `/srv/docker/bedrock-map/queue` | [[bedrock-map-queue.py]] |
| `vriendenpaneel` | API van het Beheer-tabblad + login van de hele site | [[Vriendenpaneel]] |
| `mcxboxbroadcast` | PS5/Xbox joinen via de vriendenlijst | [[Bedrock-server]] |

- Pod Security `restricted`, non-root, read-only. API en paneel mogen geen verbindingen naar buiten maken.
- nginx gebruikt cluster-DNS (`vriendenpaneel.mc.svc.cluster.local`, resolver 10.43.0.10).
- De NetBird-proxy (`mc`), Traefik (`mc-netbird`) en n8n (`mcping.js`) wijzen naar 10.43.100.50.
- Paneel-Secret `mc/vriendenpaneel-env` komt uit `.env`, maar dan **zonder** aanhalingstekens (kubectl haalt die niet weg).

## Namespace `mc-server` (bewust privileged)
**Deployment `bedrock`** bevat:
- container `bsm`: [[Bedrock Server Manager]] 3.10.6 en de server, image `mc-bsm` (Python 3.11, dezelfde pakketten als `/opt/bsm-venv`);
- sidecars `kaart-live`, `kaart-queue`, `discord` en `paneel-worker`: de scripts uit [[Scripts in ~-bin]].

De pod heeft `hostNetwork` (19132 TCP/UDP en BSM-web 11325 zoals altijd), een gedeelde procesruimte en SELinux `spc_t`. Alle mappen zijn **op hetzelfde pad** gemount als op de host. Daardoor werken `pgrep -x bedrock_server`, `/proc/<pid>/fd/0`, `cmd.sh` en `server_output.txt` vanaf de host precies zoals vroeger.

> [!tip] Aan, uit en herstarten
> Gewoon `sudo systemctl start|stop|restart bedrock-server-manager-webui`. Die unit heet nog hetzelfde, maar `/usr/local/sbin/mc-k8s-dienst` zet de deployment op 1 of 0. In Git staat bewust geen `replicas`.
> BSM stopt de server netjes bij SIGTERM ("Server stop requested ... Quit correctly"). Het paneel herstart via `bsm-herstart` (env `BSM_HERSTART`). Daardoor werken [[weekly-update.sh]], [[ensure-apps-up.sh]], mc-autoupdate, poortcheck en terugdraai ongewijzigd.

**CronJobs** (hostPID, zelfde schema en logbestanden als de oude crontab):

| CronJob | Schema | Notitie |
|---|---|---|
| `kaart-render` | elke 5 min | [[bedrock-map.sh]], [[uNmINeD]] |
| `kaart-collect` | elke minuut | [[Kaart-collector]] |
| `mijlpalen` | elke 2 min | [[Stats en ranglijst]] |
| `weer` | elke 10 min | [[Scripts in ~-bin]] |
| `borden-bouw` | :07, :22, :37, :52 | [[Bedrock-kaart]] |

## Blijft op de host
- `deploy.py` (cron, met git- en ssh-sleutels)
- de rootscripts `mc-autoupdate`, `mc-poortcheck`, `mc-xboxcheck` (leest nu podlogs via kubectl), `mc-hersteltest` en `mc-terugdraai`
- de backups

> [!warning] Nooit een tweede Bedrock-server tegelijk
> Scripts zoeken de server met `pgrep` en nemen de eerste PID. Een proefserver ernaast stuurt commando's naar de verkeerde server.

Terugvalmateriaal (oude units, crontab, compose-files): `/srv/backups/archief-voor-k3s-20261031.tar.gz`.
