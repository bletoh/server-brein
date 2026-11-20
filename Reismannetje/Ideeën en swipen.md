---
tags: [reismannetje, functie]
---
# Ideeën en swipen

**Ideeën**: rangschikt 145 bestemmingen vanaf Schiphol op wensen van de groep (feesten, strand, zon, stedentrip, goedkoop, wintersport, …) en het weer per maand. Elk pakket toont vlucht + verblijfsschatting per persoon. Categoriebalk met iconen, filters achter een knop, zoeken op land/plaats.
- Data: `public/data/bestemmingen.json` (foto's handmatig gekozen van Wikimedia Commons, nooit raden op paginatitel).
- Wensen van de eigenaar: geen Oost-Europa behalve Kroatië, Griekenland en Sunny Beach; geen Caribisch gebied; wel dure verre bestemmingen.
- Budgetfunctie is verwijderd (2026-10-23).

**Swipen** (2026-10-23, `09-swipen.js`): Tinder-achtig door de ideeën (desktop en telefoon), pijltjestoetsen/slepen, ongedaan maken. Swipes staan in `dest_reactions`; als alle leden (minstens 2) rechts swipen ontstaat een **match** (`dest_matches`) met één chatbericht. Swipes vervingen de duimpjes.

Echte prijzen: [[Externe diensten (Reismannetje)]]. Getoond op de [[Planavond]].
