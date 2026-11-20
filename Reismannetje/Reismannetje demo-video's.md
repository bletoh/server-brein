---
tags: [reismannetje, media]
map: ~/reismannetje-demo
---
# Reismannetje demo-video's

Werkmap `~/reismannetje-demo`.
| Video | Bestand | Methode |
|---|---|---|
| Desktop (76 s, 60 fps) | `reismannetje-demo.mp4` | CDP screencast in slow motion, daarna versneld (`demo.js`, `maak.py`) |
| Mobiel (87 s, 1080x1920, met eigen muziek) | `reismannetje-demo-mobiel.mp4` | deterministische opname met `HeadlessExperimental.beginFrame` (`motor.js`), montage met telefoonframe (PIL), muziek gemaakt met numpy |
| Planavond (v3, 46 s) | `reismannetje-demo-planavond.mp4` | drie `motor.js`-instanties tegelijk (tv + 2 telefoons), om de beurt actief |

Altijd met een verse testserver en nepdata (vrienden via de API), nooit productie. Artifacts op claude.ai met hoofdstukknoppen. Tijdens opnames gevonden bugs zijn in de app opgelost.

Zie [[Playwright-testen]], [[Planavond]].
