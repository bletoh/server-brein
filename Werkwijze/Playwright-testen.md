---
tags: [werkwijze, test]
---
# Playwright-testen

> [!note] Sinds 2026-10-31
> Bij voorkeur tegen de testomgeving: `docker run --network host … -e E2E_BASE=http://10.43.100.41:4000`, eerst `reismannetje-test-reset.sh`. → [[Reismannetje op k3s]]

De host heeft geen Chromium-bibliotheken, dus browsertests draaien in Docker:
```bash
sudo docker run --rm --network host mcr.microsoft.com/playwright:v1.63.0-noble …
```
- Scripts (`pw/*.js`) staan in de scratchpad van de sessie, met `playwright-core@1.63.0`.
- WebGL (MapLibre) headless: `--enable-unsafe-swiftshader --use-angle=swiftshader`.
- Touch-swipes: CDP `Input.dispatchTouchEvent` (Playwright heeft geen touch-drag).
- iPhone: WebKit met `devices['iPhone 15']`.
- Kaartsite testen via het container-IP van `bedrock-map` met nep-JSON via `page.route`.
- Altijd een verse testserver; check of er geen oude op dezelfde poort draait (`ss -ltnp`).

Gebruikt voor [[Reismannetje tests]], [[Reismannetje demo-video's]] en de [[Bedrock-kaart]].
