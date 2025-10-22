# Configuration réseau — SRV-ADDS

## 1. Paramètres IPv4

| Élément     | Valeur                      |
| ----------- | --------------------------- |
| Adresse IP  | `192.168.20.10`             |
| Masque      | `255.255.255.0` (/24)       |
| Passerelle  | `192.168.20.1`              |
| DNS préféré | `127.0.0.1` (boucle locale) |

📍 **Important :**
Le DNS pointe vers **lui-même**, car ce serveur hébergera plus tard le service DNS pour le domaine `corp.lab`.

## 2. Validation avec `ipconfig /all`

## 3. Tests de connectivité

Depuis SRV-ADDS :
ping 192.168.20.1 # OK - répond (pfSense)
Test-NetConnection 192.168.20.1 -CommonTCPPort HTTP

Depuis la machine hôte :
ping 192.168.20.10 # OK
Test-NetConnection 192.168.20.10 -Port 3389 # RDP ouvert

✅ **Résultat attendu :**

- Réponses ICMP correctes
- Connexion RDP possible depuis le poste de gestion
