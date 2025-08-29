# Lab Administration : AD & DHCP – Agence Rue25

## 🎯 Objectifs
- Installer un serveur Windows Server 2019 pour l’agence Rue25
- Configurer un serveur DHCP pour l’attribution automatique des adresses IP
- Installer Active Directory (AD DS) et créer le domaine `rue25.com`
- Créer les utilisateurs, unités organisationnelles (OU) et groupes de sécurité
- Optionnel : créer des dossiers partagés par service avec permissions adaptées

## 🛠️ Environnement
- Machine virtuelle : VirtualBox / VMware
- Système : Windows Server 2019
- Configuration VM :
  - RAM : 4 Go
  - CPU : 2 cœurs
  - Disque dur : 50 Go
  - Réseau : Mode NAT
- Captures écran disponibles dans `Screenshots/` (optionnel)
- Scripts PowerShell pour automatisation des utilisateurs et groupes (optionnel)

## 🔄 Mise en œuvre

### 1️⃣ Configuration de la machine virtuelle
- Nom de la VM : `Windows2019`
- Adresse IP statique :
  - IP : 10.0.2.20
  - Masque : 255.255.255.0
  - Passerelle : 10.0.2.2
  - DNS : 10.0.2.2

### 2️⃣ Configuration du rôle DHCP
- Installation via le Gestionnaire de serveur → Ajouter rôles et fonctionnalités
- Plage d’adresses DHCP :
  - Nom : Rue25DHCP
  - Plage : 10.0.2.100 – 10.0.2.150
  - Passerelle : 10.0.2.2
  - DNS : 10.0.2.2
- Tests : IP attribuée automatiquement sur un poste client, vérification des baux

### 3️⃣ Configuration de l’Active Directory (AD DS)
- Installation du rôle AD DS via le Gestionnaire de serveur
- Promotion du serveur comme contrôleur de domaine :
  - Nom du domaine : `rue25.com`
- Création des OU :
  - Direction, Consultants, Commerciaux, Comptables
- Ajout des utilisateurs :
  - Direction : Sylvie Bien, Lisa Razou, Samira Bien
  - Consultants : Alain Firmerie, Mehdi Tez
  - Commerciaux : Jonathan Longtemps, Paul Dunor
  - Comptables : Vincent Tyme, Cyrène Demer
- Création des groupes de sécurité :
  - Service Direction, Service Consultants, Service Commerciaux, Service Comptables

### 4️⃣ Configuration des dossiers partagés
- Emplacement : `C:\Partages`
- Sous-dossiers par service :
  - Direction, Consultants, Commerciaux, Comptables
- Permissions réseau et NTFS alignées sur les groupes :
  - Exemple : Dossier Consultants → Services Consultants lecture/écriture, Samira Bien lecture

### 5️⃣ Tests finaux
- DHCP : vérification qu’un poste client reçoit une IP automatiquement dans la plage définie
- Connexions utilisateurs : chaque utilisateur peut se connecter au domaine
- Permissions dossiers : accès validé selon les autorisations configurées

## ✅ Résultats
- DHCP opérationnel et IP attribuées automatiquement
- AD fonctionnel avec utilisateurs, groupes et OU créés
- Partages réseau configurés avec permissions adaptées
- Documentation complète disponible pour référence interne

