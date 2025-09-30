# VirtualBox - Design réseaux

## Choix de modes

> Objectif : séparer WAN, Users, Servers, Management. DHCP désactivé sur tous les Host-Only (géré par pfSense).

| Mode réseau VirtualBox | Usage                       | VM concernée    | Nom VirtualBox (Adapter)         |
| ---------------------- | --------------------------- | --------------- | -------------------------------- |
| NAT                    | Accès Internet (WAN)        | pfSense (WAN)   |
| Host-Only              | Réseau interne Utilisateurs | VM Users        | VirtualBox Host-Only Ethernet #2 |
| Host-Only              | Réseau interne Serveurs     | VM Servers      | VirtualBox Host-Only Ethernet #3 |
| Host-Only              | Réseau interne Management   | VM Admin / MGMT | VirtualBox Host-Only Ethernet #4 |

## Segments et adresses

> Passerelles = interfaces LAN de **pfSense (.1)**. IP hôte = **adaptateur Host-Only** de l'hôte (.254).

| Segment    | Plage IP        | Gateway (pfSense) | IP hôte (VirtualBox) |
| ---------- | --------------- | ----------------- | -------------------- |
| Users      | 192.168.10.0/24 | 192.168.10.1      | 192.168.10.254       |
| Servers    | 192.168.20.0/24 | 192.168.20.1      | 192.168.20.254       |
| Management | 192.168.99.0/24 | 192.168.99.1      | 192.168.99.254       |

## Paramètres VirtualBox (rappel)

- **Adapter pfSense WAN** : NAT
- **Adapters pfSense LAN** : Host-only (un par segment Users / Servers / MGMT)
- **DHCP Host-Only** : **Off** sur tous les segments (pfSense fait DHCP si besoin)
