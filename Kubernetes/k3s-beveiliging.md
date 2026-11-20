---
tags: [kubernetes, beveiliging]
aliases: [NetworkPolicy, Pod Security]
---
# k3s-beveiliging

## Pods
- [[Reismannetje op k3s]], de `mc`-namespace en monitoring draaien onder Pod Security **restricted**:
  - non-root (uid 1000 of 101/65534);
  - read-only rootfs met alleen een `emptyDir` voor `/tmp`;
  - `capabilities: drop ALL`, seccomp `RuntimeDefault`;
  - geen ServiceAccount-token.
- Data via vaste PersistentVolumes in plaats van hostPath, want hostPath is onder `restricted` niet toegestaan.
- Uitzonderingen, bewust privileged:
  - `registry`: hostNetwork op loopback;
  - `mc-server`: de Minecraft-server, zie [[Minecraft op k3s]];
  - `system-upgrade`: de upgrade-controller draait met SELinux `spc_t`, anders mag hij de CA-bundel van de host niet lezen.

## NetworkPolicies
- **Erin:** alleen vanaf de Docker-netwerken (172.16.0.0/12: Traefik, n8n, NetBird-proxy) en de host zelf. Andere pods worden geweigerd.
  - Docker-containers komen binnen met hun eigen adres, via hun standaardroute: `books-net` (172.19/16), niet `web`. De masquerade gebeurt pas na het filteren.
- **Eruit (Reismannetje):** alleen publieke DNS (1.1.1.1, 9.9.9.9) en TCP 80/443/465/587 naar internet. Niets intern: geen Docker-netwerken, geen NetBird (100.64/10), geen LAN, geen 169.254 (OVH-metadata) en niet het eigen publieke IP. Daarmee is de app dicht tegen SSRF.

> [!danger] NetBird-mark botst met kube-router
> NetBird zet in mangle PREROUTING op elk nieuw pakket de mark `0x1bd22`. Bit `0x10000` daarin betekent voor kube-router "goedgekeurd door NetworkPolicy". Zonder ingreep werkten **alle** NetworkPolicies dus niet.
> Oplossing: regels in mangle INPUT en FORWARD die voor pod-verkeer (10.42.0.0/16) de bits `0x30000` wissen. Ze staan ook in `/etc/sysconfig/iptables`. Zie [[Firewall (iptables)]].

## Firewall
- filter INPUT-regel **014**: 10.42.0.0/16 (pods) mag naar de host, voor de API-server en DNS.
- NodePorts luisteren alleen op 127.0.0.1. De API-server (6443) is van buiten dicht via de regel "999 deny all".
- `systemctl restart iptables` wist de k3s-ketens; doe daarna `systemctl restart k3s`.

## SELinux
- Host-mappen voor pods krijgen het label `container_file_t` via `semanage fcontext` (`/srv/k8s`, `/srv/docker/bedrock-map`, `vriendenpaneel`, `mcxboxbroadcast`).
- `k3s-selinux` is geïnstalleerd.
