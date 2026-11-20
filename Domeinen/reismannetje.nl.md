---
tags: [domein]
---
# reismannetje.nl

> [!note] Sinds 2026-10-31
> Geserveerd door k3s (`reismannetje/reismannetje`, 10.43.100.40). Testomgeving: reismannetje-test.benjaminhashi.nl. → [[Reismannetje op k3s]]

Eigen domein van [[Reismannetje]] sinds 2026-10-14 (geregistreerd bij OVH).
- Route: [[Traefik]] direct (geen NetBird-proxy: de app is publiek met eigen accounts), routers `reismannetje`, `reismannetje-www` (301), `vakantieplanner-oud` (301), service `http://reismannetje:4000`.
- `PUBLIC_URL=https://reismannetje.nl` in compose.
- Publieke pagina's: `/bestemmingen`, `/bestemming/<slug>`, `/reis/<slug>`, `/reizen/<slug>`, `/stem/<slug>`, `/privacy`, `sitemap.xml` — zie [[Deelpagina's en bestemmingsgids]].
- Health: `/healthz` en `/healthz?backup=1` (gecheckt door [[NAS app-check]]).
- Google Search Console: sitemap nog niet ingediend (account eigenaar).

Oud adres: [[vakantieplanner.benjaminhashi.nl]].
