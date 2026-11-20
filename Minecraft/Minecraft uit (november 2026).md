---
tags: [minecraft, status]
aliases: [Minecraft uit, minecraft-weer-aan]
bijgewerkt: 2026-11-19
---
# Minecraft uit (sinds 2026-11-19)

Op verzoek van de eigenaar staat **alles rond Minecraft tijdelijk uit**, tot hij zegt dat het weer aan mag. Zet niets Minecraft-achtigs zelf terug aan.

## Wat er uit staat
| Onderdeel | Hoe uitgezet |
|---|---|
| Vlagbestand | `/etc/minecraft-uit`: zolang dit bestaat slaat [[ensure-apps-up.sh]] BSM, de mc-pods en de bsm/mc-sitechecks over (backup: `/srv/backups/ensure-apps-up.voor-mc-uit-*.sh`) |
| Flux | kustomizations `mc` en `mc-server` op suspend ([[Flux en GitOps]]) |
| Server | `bedrock-server-manager-webui` gestopt en disabled; deployment `mc-server/bedrock` op 0 ([[Bedrock Server Manager]]) |
| Namespace `mc` | `bedrock-map`, `bedrock-map-api`, `vriendenpaneel`, `mcxboxbroadcast` op 0, dus [[mc.benjaminhashi.nl]] is offline |
| k3s CronJobs | `borden-bouw`, `kaart-collect`, `kaart-render`, `mijlpalen`, `weer` op suspend ([[Cron-planning]]) |
| Host-cron | `/etc/cron.d/mc-{autoupdate,hersteltest,poortcheck,xboxcheck}` hernoemd naar `*.uit` |
| User-crontab | `deploy.py`-regels beginnen met `#MCUIT# ` (backup `~/archief/crontab.voor-mc-uit-*`) |
| n8n | flow `MinecraftStatus1` niet gepubliceerd ([[n8n-flows]]) |

Blijft wel draaien: [[app-backups.sh]] (wereldbackup), [[weekly-update.sh]] (bouwt het `mc-bsm`-image opnieuw, kan geen kwaad) en de Discord-flow `/status` ([[Discord status-commando]]).

## Weer aanzetten
```bash
~/minecraft-weer-aan.sh            # draait alles hierboven terug
sudo ss -lnptu | grep bedrock_server   # verwacht *:19132
```
Bindt 19132 niet: één keer `systemctl restart` van BSM, zie [[Minecraft op k3s]].

Zie [[Bedrock-server]], [[Minecraft op k3s]], [[Tijdlijn]].
