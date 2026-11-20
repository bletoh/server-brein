---
tags: [kubernetes, registry]
aliases: [registry, 127.0.0.1:5000]
---
# Lokale registry

Een `registry:2.8.3` in [[Kubernetes (k3s)]] (namespace `registry`) voor de eigen images: `reismannetje` en `mc-bsm`.

- Luistert **alleen op `127.0.0.1:5000`** van de host (hostNetwork). Docker mag daar zonder extra config naar pushen, want 127.0.0.0/8 is voor Docker standaard "insecure". Pods en internet kunnen er niet bij.
- k3s/containerd haalt eruit via `/etc/rancher/k3s/registries.yaml`.
- Data: `/srv/k8s/registry/data`.

## Twee valkuilen (zie ook [[Valkuilen en lessen]])
1. **Altijd bouwen met `--provenance=false --sbom=false`.** Anders pusht Docker een OCI-index (image plus attestation), en `garbage-collect` van registry 2.8 begrijpt die niet: hij gooit dan de layers van alle tags weg.
2. **Na garbage-collect de registry herstarten.** De registry houdt in zijn geheugen bij welke blobs er zijn. Na een GC klopt dat niet meer, en dan slaat `docker push` het uploaden van verwijderde layers over.

## Opruimen
`/usr/local/sbin/registry-opruimen.sh` (wekelijks in [[weekly-update.sh]]): houdt per image de nieuwste 6 tags plus alles wat in Git in gebruik is (`newTag` en `image:`-regels), doet daarna garbage-collect en herstart de registry. Zie [[k3s-onderhoud]].
