---
tags: [reismannetje, functie]
---
# Groepen en chat

Sinds 2026-10-05. Accounts (naam + wachtwoord), groepen ("teams") met uitnodigingslink `/join/<code>` of QR-code, chat met gebeurtenisberichten.

- Alles is per groep gescheiden (`team_id`, header `X-Team`). De eerste die een lege groep binnenkomt wordt beheerder.
- Chat werkt als een WhatsApp-groep: stemrondes, roulette, datumprikker en "toevoegen" via de ＋-knop in de chat; vastgezette balk met de open stemronde.
- Desktop: chat als kolom links naast de kaart (dock); telefoon: chatknop rechtsonder op de kaart.
- Gebeurtenisberichten (pin toegevoegd, reis gepland, "gaat mee", uitgave, match) met kaartjes; verlopen verwijzingen worden na 1 minuut opgeruimd.
- **Alleen in een groep** (2026-10-23): ben je de enige, dan verdwijnen alle groepselementen (chat, datumprikker, stemmen, wie betaalt wat, rsvp). Uitnodigen blijft.

Code: `routes/social.js`, `11-accounts-chat.js`. Push bij nieuwe berichten: [[PWA en push]]. Live bijwerken: [[Planavond]]. Zie [[Reismannetje]].
