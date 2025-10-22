# Windows Server 2022 — Installation de base (SRV-ADDS)

## 1. Détails de l’installation

- Édition : **Windows Server 2022 Standard (Desktop Experience)**
- ISO utilisée : image officielle Microsoft (eval)
- Type d’installation : **installation propre**, partition automatique
- Nom de machine : **SRV-ADDS**
- Mot de passe administrateur : **non écrit ici (sécurisé localement)**
- Interface réseau utilisée : **Host-Only (VirtualBox Host-Only Adapter #3)**
- Timezone : **(UTC+01:00) Bruxelles, Paris**
- Langue/clavier : **Français (France)**
- Pilotes : détectés automatiquement par VirtualBox Guest Additions

## 2. Objectif

Préparer le serveur pour devenir **contrôleur de domaine Active Directory (AD DS)**.  
La machine doit être stable, administrable à distance (RDP) et joignable en ping.

## 3. Vérifications après installation

- `hostname` → **SRV-ADDS**
- `systeminfo | findstr "OS Name"` → confirme l’édition Windows
- RDP activé et testé depuis l’hôte (port 3389)
- Ping autorisé (ICMPv4-In) depuis pfSense ou machine de gestion
