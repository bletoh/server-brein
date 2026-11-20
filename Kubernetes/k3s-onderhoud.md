---
tags: [kubernetes, onderhoud, automatisering]
aliases: [k3s-updates, k8s-images-bijwerken]
---
# k3s-onderhoud

Alles draait automatisch; het meeste hangt aan [[weekly-update.sh]] (maandag 03:00, terwijl Minecraft uit staat).

| Wat | Hoe | Wanneer |
|---|---|---|
| k3s zelf | system-upgrade-controller, Plan `k3s-server`, kanaal **v1.36** (alleen patches), zonder cordon of drain; pods blijven draaien terwijl k3s herstart | ma 04:00–05:00 |
| Flux | `flux-update.sh`: nieuwste 2.x-release van minstens 14 dagen oud, gefilterd, dry-run, commit naar `k8s` | wekelijks |
| externe images | `k8s-images-bijwerken.sh`: alles opnieuw pullen en alleen Deployments met een veranderde image herstarten | wekelijks |
| Minecraft-image | hetzelfde script bouwt `mc-bsm` opnieuw met `--pull`, nieuwe tag via Git/Flux, actief bij de volgende start | wekelijks (server uit) |
| Reismannetje-images | `reismannetje-k8s-deploy.sh --pull` voor prod en test | wekelijks |
| registry | `registry-opruimen.sh`, zie [[Lokale registry]] | wekelijks |
| backups | [[app-backups.sh]] `k3s`: Secrets (yaml), deploy key, k3s-token, `/etc/rancher/k3s`, cluster-database (`state.db`), gitops-werkkopie, testwachtwoord; ook naar de NAS | elke nacht 01:15 |
| controle | [[ensure-apps-up.sh]]: k3s-service, prod-deployment, mc-pods, Flux Ready | elk uur |

Naar een nieuwe minor-versie van k3s (bijvoorbeeld 1.37) gaat met de hand: het kanaal aanpassen in `infra/system-upgrade/plan-k3s.yaml`.

## Logs
Het Traefik-access-log wordt dagelijks geroteerd (14 dagen, copytruncate). Tot 2026-10-31 gebeurde dat nooit: SELinux liet logrotate de map niet lezen. Nu heeft de map het label `var_log_t`. Zie [[Traefik]].

## Opruimen
Het terugvalmateriaal van de migratie zit in één archief: `/srv/backups/archief-voor-k3s-20261031.tar.gz`. Zie [[srv-backups]].
