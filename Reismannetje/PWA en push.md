---
tags: [reismannetje, functie]
---
# PWA en push

- **PWA** (2026-10-14): manifest + iconen (`scripts/iconen.js`), service worker `src/service-worker.js` op `/sw.js` (versie = hash van bundel/css/index). App-schil network-first, `/vendor` `/img` `/uploads` cache-first, nooit `/api` of deellinks. Offline-scherm. Installeren via knop of iPhone-uitleg.
- **Push** (`src/push.js`, `web-push`): bij chatberichten en gebeurtenissen naar andere leden. VAPID-sleutels in `vapid.json` (zit in de backup). Alleen bekende pushdiensten (Google, Apple, Mozilla, Microsoft) toegestaan.
- Ook gebruikt door het prijsalarm ([[Tickets en prijsalarm]]).
- App-stores: later misschien (Play Store €25, App Store $99/jaar).

Headless Chromium kan zich niet op push abonneren → server-kant getest met een stub ([[Reismannetje tests]]).
