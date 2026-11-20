---
tags: [reismannetje, test]
---
# Reismannetje tests

> [!note] Sinds 2026-10-31
> e2e kan tegen de testomgeving (`E2E_BASE=http://10.43.100.41:4000`, eerst `reismannetje-test-reset.sh`). Let op: 6 van de 8 e2e-tests lopen achter op de UI (ook lokaal). → [[Reismannetje op k3s]]

`npm test` = `scripts/check-app.js` (syntaxcheck van de bundel) + `node --test test/*.test.js`. Elke test start de server op een lege tijdelijke `DATA_DIR`. Ook in GitHub Actions bij elke push/PR.

Testbestanden: `api`, `beveiliging`, `e2e`, `gids`, `hernoemen`, `inpaklijst`, `linkinfo`, `partnerlinks`, `planavond`, `prijsalarm`, `pwa`, `reset`, `rondreis`, `swipen`, `tickets` (+ `helpers.js`).

**E2E** (`test/e2e.test.js`, `E2E=1`): Chromium klikt door inloggen, kaart, planpaneel, reizen, ideeën, chat, snel toevoegen, planavond. Lokaal met `E2E_BASE=http://…` tegen een testserver op de host, omdat de Playwright-image Node 24 heeft en better-sqlite3 voor Node 20 gebouwd is. Zie [[Playwright-testen]].

Zie [[Reismannetje ontwikkelworkflow]].
