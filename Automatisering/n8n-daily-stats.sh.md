---
tags: [automatisering, script, monitoring]
bestand: /usr/local/sbin/n8n-daily-stats.sh
---
# n8n-daily-stats.sh

Dagelijks 07:00 (`/etc/cron.d/n8n-daily-stats`). Verzamelt als JSON: hostnaam, uptime, load, schijf, geheugen, alle containers, **certificaat-dagen** per domein (DOMAINS), mislukte n8n-runs van 24 uur (psql in de n8n-db), staart van de update-log. Stuurt het naar de lokale webhook `http://127.0.0.1:5678/webhook/…` van de flow [[Dagelijks serverrapport]].

Testen: `sudo n8n-daily-stats.sh --print`. Zie [[n8n]], [[Certificaten (Let's Encrypt)]].
