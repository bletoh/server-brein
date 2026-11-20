---
tags: [reismannetje, werkwijze, git]
---
# Reismannetje ontwikkelworkflow

> [!note] Sinds 2026-10-31
> Testen kan op de testomgeving: `git push --force origin <branch>:test` (binnen 2 min live). Productie: merge naar `main` → autodeploy via `reismannetje-k8s-deploy.sh` → Flux. `docker exec reismannetje` werkt niet meer: gebruik `sudo /usr/local/bin/k3s kubectl -n reismannetje exec deploy/reismannetje -- …`. → [[Reismannetje op k3s]]

1. Repo kopiëren naar de scratchpad van de Claude-sessie, `npm ci`.
2. Testserver met een **verse** lege `DATA_DIR` (of kopie) op een eigen poort (4100–4171), PID in een bestand bewaren. **Nooit** `pkill` op patroon: dat raakt ook de productie-node.
3. Browsertests met Playwright in Docker (`--network host`) → [[Playwright-testen]], plus `npm test` → [[Reismannetje tests]].
4. Commit op een feature-branch (`-c user.name=bletoh`), fetch naar `/srv/docker/reismannetje` (`sudo git -c safe.directory=*`), push (root's SSH-sleutel).
5. Deployen: `sudo docker compose -f /srv/docker/reismannetje/docker-compose.yml up -d --build`.
6. Eigenaar merget de PR op GitHub (geen `gh` CLI op de server).

## Afspraken
- Sinds 2026-10-23: **één PR-branch naar main per ronde** (huidige: `naar-main`), geen gestapelde branches meer. Na merge nieuw werk vanaf `origin/main`.
- Vóór deployen `git status`/`git check-ignore` voor nieuwe bestanden (een genegeerd databestand liet de container eens 3 min crashen).
- DB-backup maken vóór migraties (`/srv/backups/reismannetje-voor-*.db`).
- Pushen en deployen mag zonder te vragen (toestemming eigenaar).
- Repo-naam op GitHub: `bletoh/vakantieapp` (hernoemen naar reismannetje staat nog open).

Zie [[Claude Code sessies]], [[Valkuilen en lessen]].
