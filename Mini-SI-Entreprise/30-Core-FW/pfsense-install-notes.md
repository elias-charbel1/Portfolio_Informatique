# pfSense – Installation & Interfaces

## Version

pfSense CE 2.7.x (ISO amd64)

## Mapping VirtualBox ↔ pfSense

| VirtualBox NIC | Mode réseau  | pfSense interface    | Segment         | IP assignée                      |
| -------------- | ------------ | -------------------- | --------------- | -------------------------------- |
| NIC1           | NAT          | em0 (WAN)            | Internet (NAT)  | DHCP (attribuée automatiquement) |
| NIC2           | Host-Only #2 | em1 (OPT1 - USERS)   | 192.168.10.0/24 | 192.168.10.1                     |
| NIC3           | Host-Only #3 | em2 (OPT2 - SERVERS) | 192.168.20.0/24 | 192.168.20.1                     |
| NIC4           | Host-Only #4 | em3 (LAN - MGMT)     | 192.168.99.0/24 | 192.168.99.1                     |

## Choix clés

- **LAN = MGMT** pour profiter de la règle anti-lockout.
- **WAN en DHCP (NAT VirtualBox)** pour accès Internet.
- **DHCP désactivé** sur LAN/OPT1/OPT2 (relay via AD plus tard).
- Test ping OK sur .99.1 / .10.1 / .20.1 depuis l’hôte.
- Accès GUI : https://192.168.99.1 (admin / pfsense)

## Captures

- Console : assignation des interfaces
- Interface Web : page de login pfSense (certificat autosigné)
