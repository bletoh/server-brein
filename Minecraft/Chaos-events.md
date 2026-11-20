---
tags: [minecraft, functie]
---
# Chaos-events

Console-events op verzoek van de eigenaar (meestal stil, zonder chatmelding):
| Event | Commando | Opmerking |
|---|---|---|
| Aardbeving | `aardbeving:start [sec]` | camerashake, vallend grind/zand dat weer verdwijnt |
| Dansende dieren | `dans:start [sec]` | stil |
| Razend vuur | `vuur:haard x z` / aansteken als `vuur:aan` | realistische verspreiding via brandstof en wind; staat standaard **uit**; noodstop `vuur:blus` |
| Meteoriet | `meteoor:inslag x z` | krater r6, ancient debris in de kern |
| Atoombom | `atoom:start [demo \| x z y]` | luchtalarm, kijkplatform, krater, paddenstoelwolk |
| Mega-atoombom | `atoom:mega` | 5 bommen, spelers onsterfelijk; vooraf alles laden |

Alle grote events zijn na afloop teruggedraaid met de [[Chunk-merge hersteltool]] uit [[Wereldbackups]]. Vrienden kunnen meteoor en atoombom alleen op het [[Demodorp]] afvuren via het [[Vriendenpaneel]].

Les: na een enorme krater laadt de server minutenlang geen nieuwe chunks → eerst alles voorladen. Zie [[Valkuilen en lessen]].
