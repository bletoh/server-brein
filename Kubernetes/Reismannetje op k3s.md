---
tags: [kubernetes, reismannetje]
aliases: [Reismannetje k8s, Testomgeving Reismannetje, reismannetje-test]
---
# Reismannetje op k3s

[[Reismannetje]] draait sinds 2026-10-31 in [[Kubernetes (k3s)]] in plaats van Docker Compose. De overstap kostte ongeveer 20 seconden downtime.

## Productie en test
| | productie | test |
|---|---|---|
| URL | [[reismannetje.nl]] | reismannetje-test.benjaminhashi.nl (basic auth, `noindex`) |
| namespace | `reismannetje` | `reismannetje-test` |
| ClusterIP | 10.43.100.40:4000 | 10.43.100.41:4000 |
| data | `/srv/k8s/reismannetje/data` | `/srv/k8s/reismannetje-test/data` (eigen, lege database) |
| bron | `/srv/docker/reismannetje` (live branch; autodeploy van `main`) | GitHub-branch `test` (autodeploy elke 2 min) |

- Wachtwoord van de testomgeving: `/srv/k8s/reismannetje-test/wachtwoord` (zie [[Geheimen]]).
- Iets op test zetten: `git push --force origin <branch>:test`. Testomgeving leegmaken: `reismannetje-test-reset.sh`.
- Browsertests tegen test: zie [[Playwright-testen]] (`E2E_BASE=http://10.43.100.41:4000`, eerst een reset).

## Deploy
`/usr/local/sbin/reismannetje-k8s-deploy.sh [--env prod|test] [--src MAP] [--pull]`:
1. image bouwen (zonder attestations) en pushen naar de [[Lokale registry]]
2. `newTag` in Git zetten, committen, pushen (branch `k8s`)
3. Flux laten toepassen, of zelf `apply -k`
4. wachten op een gezonde pod; mislukt het, dan `git revert` en terug naar de vorige versie

Aangeroepen door `reismannetje-autodeploy.sh` (prod, cron elke 2 min), `reismannetje-test-autodeploy.sh` (test) en [[weekly-update.sh]] (`--pull`).

## Geen downtime bij deploys
De Deployment gebruikt `Recreate` (SQLite: nooit twee schrijvers). In [[Traefik]] vangen een **retry-middleware** (`k8s-deploy-retry`, 6 pogingen, backoff vanaf 0,5 s) en een **dial-timeout van 2 s** (`serversTransport k8s-snel`) de paar seconden zonder pod op. Getest: 189 van 189 requests OK tijdens een deploy, maximaal 3,6 s.

## Image
Sinds de merge van PR #64 een image in twee fasen: de build-tools komen niet in de eindimage (961 MB → 492 MB).

## Gehard
Draait als uid 1000 met een read-only rootfs, zonder capabilities, onder Pod Security `restricted` en met een NetworkPolicy. Zie [[k3s-beveiliging]].

## Backups
[[reismannetje-backup.sh]] leest nu uit `/srv/k8s/reismannetje/data`. Bij een restore: `chown -R 1000:1000` op de datamap.
