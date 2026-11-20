---
tags: [werkwijze, valkuil]
---
# Valkuilen en lessen

## Server en netwerk
- **`$` in `.env`** wordt door Compose geïnterpoleerd → enkele quotes. nb-monit-login was hierdoor een week stuk. → [[nb-monit]]
- **Containers kunnen geen host-poorten bereiken** (alleen docker0 mag) → firewallregel nodig (013 voor BSM). → [[Firewall (iptables)]]
- **Geen HTTP/3** op Traefik: breekt NetBird-relay. → [[Traefik]]
- **Hairpin-NAT + geo** → 403 voor interne checks en NetBird-peers. → [[Geo-blokkade]]
- **`allowed_cidrs` is AND**, geen uitzondering. → [[NetBird reverse proxy]]
- **Host() vs HostRegexp()**: een HTTP-router met Host() claimt de SNI en wint van TCP-passthrough. → [[mc.benjaminhashi.nl]]
- **ACME probeert niet opnieuw** tot de config echt verandert. → [[Certificaten (Let's Encrypt)]]
- **NetBird-DNS op de host** maakte elke lookup 2,5–5 s. → [[DNS-resolver]]
- **Ghost-admin-login** triggerde een CrowdSec-ban (blog inmiddels weg). → [[CrowdSec]]
- **Compress-middleware** houdt SSE-events vast → `Content-Encoding: identity`. → [[Planavond]]

- **NetBird-mark 0x1bd22 botst met kube-router**: bit 0x10000 = "door NetworkPolicy goedgekeurd", dus policies werkten niet. Bits wissen in mangle voor 10.42/16. → [[k3s-beveiliging]]
- **Docker-containers bereiken ClusterIP's met hun eigen adres** via hun standaardroute (books-net), niet via `web`. → [[k3s-beveiliging]]
- **`kubectl create secret --from-env-file` laat quotes staan** (Compose haalt ze weg): `'abc'` wordt letterlijk. → [[Minecraft op k3s]]
- **Registry 2.8 GC + OCI-index = layers weg**; bouw met `--provenance=false --sbom=false` en herstart de registry na GC. → [[Lokale registry]]
- **SELinux (enforcing)**: host-mappen voor pods `container_file_t`; logrotate kon `var_t` niet lezen (Traefik-log groeide tot 825 MB); de upgrade-controller kon de CA-bundel niet lezen (`spc_t`). → [[k3s-onderhoud]]
- **Een `kubectl patch ... suspend: true` op een Flux-Kustomization is tijdelijk**: zodra `flux-system` een nieuwe commit toepast (Flux-update, deploy), zet hij de spec uit Git terug en is de pauze weg. Pauzes die moeten blijven horen in Git (`clusters/server/apps.yaml`). Gebeurd op 2026-11-20 met mc/mc-server. → [[Minecraft uit (november 2026)]]
- **`kubectl apply --dry-run=server --server-side` tegen Flux-objecten** botst met velden van `kustomize-controller`; gebruik `--field-manager=kustomize-controller`. → [[k3s-onderhoud]]
- **Van RollingUpdate naar Recreate** kan Flux niet alleen: het `rollingUpdate`-blok moet eenmalig met de hand weg. → [[Monitoring en meldingen]]
- **Verbinding naar een pod die net stopt hangt** (geen refused): Traefik-retry helpt pas met een korte dial-timeout. → [[Reismannetje op k3s]]
- **Een check die altijd faalt valt niet op**: de NAS-check van mc stond sinds 28-10 op rood, maar de DSM-taak bestond niet eens. Controleer of een monitor echt draait. → [[NAS app-check]]
- **Geen blinde `restorecon -RF` op home**: de mc-server-pods gebruiken hostPaths daar. Laat sessies nooit `mv` naar of van een hostPath doen met variabelen die niet gecontroleerd zijn. → [[Home-incident 2026-11-10]]
- **`shutil.copy2` kopieert het SELinux-label** (`user_home_t`), waarna een pod het bestand niet mag lezen. Gebruik copyfile+copymode of `cat repo > live`; bij "pagina kapot na deploy" eerst `ls -Z`. → [[Minecraft op k3s]]
- **Foute-inlogtest via Traefik** liet CrowdSec het eigen server-IP 4 uur bannen (http-generic-401-bf). Zulke tests direct op de ClusterIP doen. → [[CrowdSec]]
- **`nohup … &` via ssh** zonder `</dev/null` houdt de sessie open. → [[camera-afspeelbaar.sh]]

## Minecraft
- **glanerbrugcraft `deploy.py` importeert eerst live → repo**: een lokale commit wordt dan overschreven. Werkwijze: commit, `git push origin HEAD:main`, `git reset --hard HEAD~1`, dan `./deploy.py`. → [[Minecraft op k3s]]
- Na een pod-herstart bindt 19132 soms niet; één keer `systemctl restart` helpt. → [[Minecraft op k3s]]
- Console = stdin van `bedrock_server`, niet van BSM. `stop` op stdin telt als crash (max 3). → [[Bedrock Server Manager]]
- `reload` laadt gewijzigde scripts, maar geen nieuwe bestanden of commando's. → [[Bedrock-server]]
- Bouwscripts zijn niet idempotent; na grote kraters laadt de server geen nieuwe chunks. → [[Chaos-events]]
- Bedrock-bloknamen wijken af (`hardened_clay`, `grass_path`, `stone_stairs` = cobblestone stairs). → [[Boomhut bletoh1]]
- `serverlog` wordt bij elke start leeggemaakt → collector houdt offset/inode bij. → [[Kaart-collector]]
- `getComponent("minecraft:food")` werkt niet op API 2.10 → vaste lijst. → [[Addon Handige Extra's]]

- **Nooit een tweede `bedrock_server` naast de echte**: scripts nemen de eerste PID van `pgrep`. → [[Minecraft op k3s]]
- **BSM herschrijft `server_output.txt` bij elke start** (collectors volgen inode + offset). Stop BSM met SIGTERM, niet met "stop" naar de console: dan start BSM de server meteen opnieuw. → [[Minecraft op k3s]]

## Reismannetje
- Nooit `pkill` op patroon (raakt productie). Testserver-PID bijhouden. → [[Reismannetje ontwikkelworkflow]]
- Nieuw bestand kan stil gitignored zijn → container crasht. Check `git status`.
- Express 4 vangt async-fouten niet → handlers wrappen.
- Overpass is vaak overbelast; foto's nooit raden op Wikipedia-titel. → [[Externe diensten (Reismannetje)]]
- CSP verbiedt inline scripts en `onclick`. → [[Reismannetje beveiliging]]
- **Traefik-502 zegt niet waar de fout zit**: `OriginStatus` is 0, ook als de app zelf 502 gaf (retry-middleware). Vergelijk met de app-log en kijk per dag (13-11 was een overbelastingsincident). → [[Agents]]
- **Airbnb zonder woningen is geen fout**: China en afgelegen plekken geven een geldige pagina zonder resultaten (sinds 20-11 een lege lijst, voorheen een 502).
- Velden kleiner dan 16 px laten iOS inzoomen en zijwaarts schuiven; date/time-inputs hebben op iOS een eigen min-breedte. → [[Reismannetje wijzigingen november 2026]]
- Een push-melding kan de oude app-versie uit de SW-cache openen; de service worker haalt nu eerst de nieuwste versie. → [[PWA en push]]
