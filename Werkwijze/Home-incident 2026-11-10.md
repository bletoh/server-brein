---
tags: [werkwijze, incident]
---
# Home-incident 2026-11-10

Op 2026-11-10 om 19:59 verplaatste een Claude-sessie bij het terugzetten van testdata de hele `/home/almalinux` naar `/srv/k8s/reismannetje-test/data` (`mv` met een verkeerde doelmap). Op 2026-11-11 hersteld met `/root/herstel-home.sh`. Conflictkopieën (`*.nieuw-20261111`, alleen een verse Claude-installatie) staan in `~/archief/herstel-20261111/`.

## Nasleep: SELinux-labels
Na het herstel heeft bijna alles in home nog het label `container_file_t:s0:c346,c412`; `restorecon` slaat dat type zonder `-F` over. `.ssh` is wel gerepareerd (`ssh_home_t`, 700/600).

**Draai geen blinde `restorecon -RF /home/almalinux`.** De mc-server-pods gebruiken hostPaths in home (`.config/bedrock-server-manager`, `.config/mc-discord`, `bin`, `apps`). Krijgen die `user_home_t`, dan kan de pod er niet meer bij.

## Les
Laat een sessie nooit `mv` naar of van een hostPath doen met variabelen die niet gecontroleerd zijn.

Zie [[Valkuilen en lessen]], [[Minecraft op k3s]], [[Reismannetje op k3s]].
