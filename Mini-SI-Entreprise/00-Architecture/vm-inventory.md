# Inventaire des VMs (Mini-SI-Entreprise)

> Rôle, segment, IP prévue et ISO à utiliser pour chaque VM.  
> Les IP `.1` sur chaque segment correspondent aux interfaces LAN de **pfSense** (gateway).  
> Les ISO seront montés au moment de l’installation des **clones** (pas sur les gabarits).

| VM               | Rôle                       | Segment(s)             | IP prévue                              | ISO à utiliser                |
| ---------------- | -------------------------- | ---------------------- | -------------------------------------- | ----------------------------- |
| **FW**           | Pare-feu / routeur pfSense | Users / Servers / MGMT | `.1` sur chaque segment (GW)           | `pfSense-CE-amd64.iso`        |
| **SRV-ADDS**     | AD DS / DNS / DHCP         | Servers                | `192.168.20.10/24` (GW `192.168.20.1`) | `Windows-Server-2022.iso`     |
| **SRV-LNX**      | GLPI (LAMP)                | Servers                | `192.168.20.20/24` (GW `192.168.20.1`) | `debian-12-amd64-netinst.iso` |
| **MON** _(opt.)_ | Centreon / Monitoring      | MGMT                   | `192.168.99.50/24` (GW `192.168.99.1`) | `debian-12-amd64-netinst.iso` |

## Notes

- **DNS chaîne** : Clients → `192.168.20.10` (SRV-ADDS) → redirecteurs (1.1.1.1 / 9.9.9.9).
- **DHCP** : scope Users `192.168.10.100–199` servi par SRV-ADDS (relay via pfSense).
- **Hôte VirtualBox (.254)** : `192.168.10.254` / `192.168.20.254` / `192.168.99.254`.
