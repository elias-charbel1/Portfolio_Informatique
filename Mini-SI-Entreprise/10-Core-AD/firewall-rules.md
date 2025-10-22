# Règles de pare-feu — SRV-ADDS

## 1. Contexte

Windows Server 2022 bloque par défaut :

- Les pings entrants (ICMP)
- Les connexions RDP (3389) jusqu’à activation

Pour faciliter la supervision et l’administration à distance, les règles suivantes ont été configurées.

---

## 2. Règles créées

### 🔹 ICMPv4-In (ping)

```powershell
New-NetFirewallRule -DisplayName "Allow ICMPv4-In" -Protocol ICMPv4 -IcmpType 8 -Direction Inbound -Action Allow
```

Permet les requêtes ping (type 8)

Utilisé pour les tests de connectivité depuis pfSense et les postes d’administration

RDP (Bureau à distance)

Activé via Paramètres → Système → Bureau à distance
Autorise la gestion distante via RDP (port TCP 3389)

Vérifié avec : Test-NetConnection 192.168.20.10 -Port 3389

✅ Validation finale :

Ping du serveur depuis pfSense et depuis l’hôte fonctionne

Connexion RDP établie depuis poste d’administration
