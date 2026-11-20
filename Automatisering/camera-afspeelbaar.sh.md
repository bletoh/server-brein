---
tags: [automatisering, script, nas]
bestand: /srv/nas-check/camera-afspeelbaar.sh (NAS: ~/scripts/camera-afspeelbaar.sh)
---
# camera-afspeelbaar.sh

Sinds 2026-11-13. Draait op de [[backupnas (Synology)]], de VPS-kopie staat in `/srv/nas-check/`.

**Probleem:** Surveillance Station (3 Reolink-camera's als Generic ONVIF, 2304x1296) neemt op in HEVC met tag `hev1`, ook al toont SS "H.264". iPhone en DS file spelen alleen `hvc1` af, en de ffmpeg van DSM (4.1.9) heeft geen HEVC-decoder.

**Oplossing:** remux zonder hercoderen (`-c copy -tag:v hvc1 -movflags +faststart`):
`/volume1/surveillance/<cam>/<dag>/*.mp4` → `/volume1/surveillance/Afspeelbaar/<cam>/<dag>/`

- Houdt de laatste 7 dagen (`BEWAAR_DAGEN=7`), ouder wordt opgeruimd.
- `nice 19` (DSM heeft geen ionice), lock `/tmp/camera-afspeelbaar.lock`, log `~/scripts/.camera-afspeelbaar.log`.
- De find op de bron slaat `@*` en `Afspeelbaar` over.
- DSM-taak "camera" (id 5), elk uur van 00 tot 23.
- Eerste run (1 dag): 807 clips, 9,7 GB, 15 min, IO-load ~5.

Valkuil: `nohup … &` via ssh zonder `</dev/null` houdt de ssh-sessie open.

Zie [[NAS app-check]], [[backupnas (Synology)]].
