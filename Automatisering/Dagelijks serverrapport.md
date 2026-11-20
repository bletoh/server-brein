---
tags: [automatisering, n8n, monitoring]
---
# Dagelijks serverrapport

n8n-flow met webhook, gevoed om 07:00 door [[n8n-daily-stats.sh]]. Maakt er een leesbaar rapport van (schijf, geheugen, containers, certificaten, mislukte runs, sites, update-log) en pusht het via ntfy.

Onderdeel van [[n8n-flows]].
