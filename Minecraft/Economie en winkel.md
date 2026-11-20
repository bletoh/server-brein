---
tags: [minecraft, functie]
---
# Economie en winkel

(2026-10-19) Lichte economie met emeralds in [[Addon Homes & Teleport]].
- **Bank** per speler (world prop `eco:b:<naam>`): storten, opnemen, betalen, geschiedenis. Alleen via NPC "Bankier".
- **Loon**: +1 emerald per uur actief spelen. **Startkapitaal** naar speeltijd, **weekbonus** elke maandag voor de top 3 (speeltijd, kills, afstand, bouwen), uitbetaald door de [[Kaart-collector]].
- **Centrale winkel** via NPC "Winkelier" in het winkelgebouw (x 452-466, z 196-206, warp `winkel`). Spelerswinkels staan uit.
- **Dynamische prijzen**: schaarste (hoeveel ertsen/kills de server heeft) × basisprijs, minimaal 2; items op slot tot de bron gevonden is (bijv. diamant, enderman, Nether); vraagtoeslag +1 per 10 aankopen per 2 uur. Berekend door de collector en via `eco:prijzen` doorgestuurd.
- Casinowinst gaat naar de bank, inzet terug als items.
- Op de site: sectie Economie (saldo's, prijslijst, laatste handel) → [[Stats en ranglijst]]. Aankondiging in Discord (bericht-id in `/srv/n8n-flows/.discord-eco-message-id`).
