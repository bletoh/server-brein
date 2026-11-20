---
tags: [kubernetes, gitops, flux]
aliases: [Flux, GitOps, branch k8s]
---
# Flux en GitOps

Alles wat in [[Kubernetes (k3s)]] draait, staat als manifest in Git: de losse branch **`k8s`** van `bletoh/vakantieapp` (los van de app-branches). Werkkopie op de server: `/srv/k8s/gitops`.

## Indeling van de branch
| Map | Inhoud |
|---|---|
| `apps/reismannetje/base`, `prod`, `test` | [[Reismannetje op k3s]] (kustomize: base + overlays) |
| `apps/mc`, `apps/mc-server` | [[Minecraft op k3s]] |
| `apps/monitoring` | [[Monitoring en meldingen]] (scripts als ConfigMap) |
| `infra/registry`, `infra/system-upgrade` | [[Lokale registry]], [[k3s-onderhoud]] |
| `images/mc-bsm` | Dockerfile van de Minecraft-image |
| `clusters/server` | Flux zelf + een Kustomization per onderdeel |

## Flux
- Flux v2.9.6, alleen **source-controller** en **kustomize-controller** (geen helm/notification/image-automation; zonder `--events-addr`).
- Leest de branch via een **read-only deploy key** (`/srv/k8s/flux/deploykey`, Secret `flux-system/github-k8s`; de gebruiker heeft hem op GitHub toegevoegd).
- Elke minuut kijken naar Git, elke 10 minuten alles opnieuw toepassen. Een handmatige wijziging in het cluster zet Flux terug (getest: replicas met de hand op 0 werd weer 1).
- Status: `sudo /usr/local/bin/k3s kubectl -n flux-system get gitrepository,kustomization`. [[ensure-apps-up.sh]] meldt elk uur als iets niet Ready is.

## Deploys = commits
`reismannetje-k8s-deploy.sh` zet de nieuwe image-tag (`newTag`) in Git, commit, pusht, laat Flux het toepassen en wacht op een gezonde pod. Mislukt het, dan volgt een `git revert`. Zonder werkende Flux past het script de map zelf toe (`kubectl apply -k`). Zie [[Reismannetje op k3s]].

## Uitzonderingen
- **Secrets** staan niet in Git (bijv. `reismannetje-env`, `vriendenpaneel-env`, `ntfy-discord`). Ze zitten wel in de nachtelijke backup, zie [[k3s-onderhoud]].
- De Minecraft-Deployment heeft bewust **geen `replicas`**: aan/uit gaat via systemd, zie [[Minecraft op k3s]].
- Namespaces en PersistentVolumes hebben `kustomize.toolkit.fluxcd.io/prune: disabled`: weghalen uit Git gooit nooit data weg.

## Bijwerken
Flux werkt zichzelf wekelijks bij via `flux-update.sh` (alleen releases van minstens 14 dagen oud), zie [[k3s-onderhoud]].
