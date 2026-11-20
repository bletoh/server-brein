---
tags: [minecraft, tool]
---
# uNmINeD

> [!note] Sinds 2026-10-31
> Renderen gebeurt in de k3s-CronJob `kaart-render` (image `mc-bsm`). → [[Minecraft op k3s]]

Kaartrenderer voor Minecraft-werelden. CLI 0.20.11-dev in `~/apps/unmined` (symlink).
- Nodig: `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1` (geen libicu op de host).
- Gebruikt door [[bedrock-map.sh]]: `web render` overworld, webp, 3D-schaduwen, zoomin 2, incrementeel (±6 s).
- The End wordt overgeslagen (nog nooit bezocht → crash).
- Licentie: gratis, niet-commercieel, niet herverdelen.
- Zwarte vlakken op de kaart = chunks die Bedrock nooit heeft opgeslagen.

Zie [[Bedrock-kaart]].
