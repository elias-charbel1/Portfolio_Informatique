# VirtualBox – Gabarits VM (Templates)

Ces gabarits servent de base aux clones des VMs du lab Mini-SI-Entreprise.

## Tableau récapitulatif

| Nom              | OS / Type VirtualBox            | vCPU | RAM  | Disque (VDI) | Contrôleur | Boot (ordre)     | NICs (mode → segment)                                                                                               | Remarques                  |
| ---------------- | ------------------------------- | ---- | ---- | ------------ | ---------- | ---------------- | ------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| **TPL-pfSense**  | BSD / FreeBSD 64-bit            | 2    | 2 Go | 20 Go (dyn.) | SATA       | Optique → Disque | NIC1: NAT (WAN Internet)<br>NIC2: Host-Only #2 (Users)<br>NIC3: Host-Only #3 (Servers)<br>NIC4: Host-Only #4 (MGMT) | Firewall / Routeur central |
| **TPL-WS2022**   | Windows Server 2019/2022 64-bit | 2    | 4 Go | 60 Go (dyn.) | SATA       | Optique → Disque | NIC1: Host-Only #3 (Servers)                                                                                        | AD/DNS/DHCP                |
| **TPL-Debian12** | Linux / Debian 64-bit           | 2    | 2 Go | 20 Go (dyn.) | SATA       | Optique → Disque | NIC1: Host-Only #3 (Servers)                                                                                        | GLPI / Serveur Linux       |

## Mapping Host-Only Adapters

| Adapter VirtualBox               | IP hôte (.254) | Segment logique |
| -------------------------------- | -------------- | --------------- |
| VirtualBox Host-Only Ethernet #2 | 192.168.10.254 | Users           |
| VirtualBox Host-Only Ethernet #3 | 192.168.20.254 | Servers         |
| VirtualBox Host-Only Ethernet #4 | 192.168.99.254 | Management      |

> Les disques sont créés en VDI dynamique.  
> Les ISO seront montés au moment de l’installation des clones.
