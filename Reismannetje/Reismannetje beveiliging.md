---
tags: [reismannetje, beveiliging]
---
# Reismannetje beveiliging

Na een audit opgelost op 2026-10-23 (commit `cc4f28f`, test `test/beveiliging.test.js`):
- **SSRF** in link-info: IPv4-in-IPv6 omzeilde de check → `net.BlockList` + undici-Agent die het adres opnieuw controleert bij verbinden (tegen DNS-rebinding).
- **Stored XSS** in kaart-tooltips op deelpagina's → `deelkaart.js` escapet.
- **CSP** `script-src 'self'`: geen inline scripts of `on*=`-handlers meer.
- Tijdelijk wachtwoord via beheerder alleen voor leden in geen andere groep (+ chatmelding).
- Sessies: alleen sha256 van het token in de DB.
- Inlogrem per kwartier: 10 per naam+IP, 30 per IP, 100 per naam. Max `REGISTER_PER_HOUR` (10) nieuwe accounts per IP.
- Container draait als `node` (`docker-entrypoint.sh` met `setpriv`, chown van `/app/data`).
- Verder: scrypt-wachtwoorden, cookie HttpOnly/SameSite=Lax/Secure, upload-sniffing, beveiligingsheaders, `trust proxy` alleen loopback/uniquelocal.

Nog niet gedaan: HSTS includeSubDomains/preload, globale JSON-limiet (15 MB) verlagen.

Rand-beveiliging: [[Traefik]] met [[CrowdSec]]. Zie [[Reismannetje backend]].
