# VirtualBox – Design réseaux

## Choix de modes

> Objectif : séparer WAN, Users, Servers, Management.  
> DHCP désactivé sur tous les Host-Only (géré par pfSense).

## Segments et adresses

> Passerelles = interfaces LAN de **pfSense (.1)**.  
> IP hôte = **adaptateur Host-Only** de l’hôte (.254).

| Segment    | Type réseau | Nom adaptateur VirtualBox        | Plage IP        | Gateway (pfSense) | IP hôte (.254) |
| ---------- | ----------- | -------------------------------- | --------------- | ----------------- | -------------- |
| WAN        | NAT         | —                                | (Internet)      | —                 | —              |
| Users      | Host-Only   | VirtualBox Host-Only Ethernet #2 | 192.168.10.0/24 | 192.168.10.1      | 192.168.10.254 |
| Servers    | Host-Only   | VirtualBox Host-Only Ethernet #3 | 192.168.20.0/24 | 192.168.20.1      | 192.168.20.254 |
| Management | Host-Only   | VirtualBox Host-Only Ethernet #4 | 192.168.99.0/24 | 192.168.99.1      | 192.168.99.254 |

## Paramètres VirtualBox (rappel)

- **Adapter pfSense WAN** : NAT
- **Adapters pfSense LAN** : Host-Only (un par segment Users / Servers / MGMT)
- **DHCP Host-Only** : **Off** sur tous les segments (pfSense fait DHCP si besoin)
