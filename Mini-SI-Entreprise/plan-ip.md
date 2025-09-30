## Gateways & IP hôte

| Segment    | Gateway (pfSense) | IP hôte (Host-Only) |
| ---------- | ----------------- | ------------------- |
| Users      | 192.168.10.1      | 192.168.10.254      |
| Servers    | 192.168.20.1      | 192.168.20.254      |
| Management | 192.168.99.1      | 192.168.99.254      |

Domaine: dexter.lab (NETBIOS: DEXTER)
DNS primaire: 192.168.20.10 (SRV-ADDS) → Redirecteurs: 1.1.1.1, 9.9.9.9
Gateways (pfSense): Users 192.168.10.1 | Servers 192.168.20.1 | MGMT 192.168.99.1
IP hôte (VirtualBox Host-Only): 192.168.10.254 / 192.168.20.254 / 192.168.99.254
DHCP: serveur 192.168.20.10 (scope Users 192.168.10.100–192.168.10.199), relay via pfSense
IPs fixes: SRV-ADDS 192.168.20.10 | SRV-LNX 192.168.20.20 | MON 192.168.99.50 (optionnel)
