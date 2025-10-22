# Core-AD — Configuration DNS (SRV-ADDS)

## Objectif

Mettre en place le service DNS interne pour le domaine **dexter.lab**, avec zones directes et inverses.

---

## 1. Zones configurées

### Zones directes

- **dexter.lab**
  - A → `srv-adds.dexter.lab` = `192.168.20.10`
  - SOA → `srv-adds.dexter.lab`
  - NS → `srv-adds.dexter.lab`

### Zones inverses

- **20.168.192.in-addr.arpa**
- **10.168.192.in-addr.arpa**

Les deux zones sont :

- **Primary**
- **Active Directory-integrated**
- **Replication scope :** To all DNS servers in this domain
- **Dynamic updates :** Secure only

---

## 2. Redirecteurs

Ajoutés dans DNS Manager → Propriétés du serveur → onglet _Redirecteurs_ :

- 1.1.1.1
- 9.9.9.9

_(non valides depuis le lab isolé, mais préconfigurés pour usage futur Internet)_

---

## 3. Tests de résolution

### Depuis SRV-ADDS

```powershell
nslookup srv-adds
# Nom : srv-adds.dexter.lab
# Adresse : 192.168.20.10

nslookup 192.168.20.10
# Nom : srv-adds.dexter.lab
# Adresse : 127.0.0.1


```

✅ Résolution directe et inverse OK
✅ DNS interne fonctionnel
✅ Serveur se résout lui-même (localhost → 127.0.0.1)
