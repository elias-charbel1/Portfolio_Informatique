## Table des Matières

- [Introduction](#introduction)
- [Objectifs](#objectifs)
- [1. Configuration de la Machine Virtuelle](#1-configuration-de-la-machine-virtuelle)
  - [Outil Utilisé](#outil-utilisé)
  - [Configuration de la VM](#configuration-de-la-vm)
- [2. Installation et Configuration](#2-installation-et-configuration)
  - [2.1 Configuration SSH](#21-configuration-ssh)
  - [2.2 Installation des Dépendances](#22-installation-des-dépendances)
  - [2.3 Configuration de MariaDB](#23-configuration-de-mariadb)


# Installation et Configuration de GLPI sur Debian

## Introduction
Ce projet documente l'installation et la configuration de GLPI (Gestion Libre de Parc Informatique) sur une machine virtuelle Debian 11.6 dans le cadre de l'agence Rue25.

### Objectifs
- Créer une machine virtuelle pour héberger GLPI.
- Installer et configurer les dépendances nécessaires.
- Installer et sécuriser GLPI via l'interface web.

---

## 1. Configuration de la Machine Virtuelle

### Outil Utilisé
- **VirtualBox**

### Configuration de la VM
- **CPU** : 1
- **RAM** : 2 Go
- **Stockage** : 20 Go
- Installation de Debian sans interface graphique.

---

## 2. Installation et Configuration

### 2.1 Configuration SSH
- Installation du serveur SSH.
- Vérification de l'installation.
- Test de la connexion SSH depuis l'ordinateur hôte.

```bash
sudo apt install openssh-server -y 
sudo systemctl status ssh
ssh user@adresseIPmachine
```

### 2.2 Installation des Dépendances
- Installation des services suivants :
  - **Apache2**
  - **PHP**
  - **MariaDB**

![Image Dépendances Installation](#)

### 2.3 Configuration de MariaDB
- Sécurisation de MariaDB.
- Création de la base de données pour GLPI :
  - Nom de la base : `glpi`
  - Utilisateur : `glpi`
  - Mot de passe : `glpi`

![Image Configuration MariaDB](#)

---

## 3. Installation de GLPI

### 3.1 Téléchargement et Extraction
- Téléchargement de la dernière version de GLPI depuis [GitHub](https://github.com/glpi-project/glpi/releases).
- Déplacement des fichiers vers le répertoire web d'Apache.

### 3.2 Installation des Modules PHP Nécessaires
- Installation des modules PHP requis par GLPI.
- Attribution des permissions nécessaires aux fichiers.

![Image Installation GLPI](#)

---

## 4. Configuration via l'Interface Web
- Accès à l'interface : `http://adresseIPmachine/glpi`.
- Connexion à la base de données avec les informations suivantes :
  - Serveur : `localhost`
  - Utilisateur : `glpi`
  - Mot de passe : `glpi`
  - Base de données : `glpi`
- Suivi des étapes de configuration.

![Image Interface Web GLPI](#)

---

## 5. Sécurisation
- Changement du mot de passe administrateur GLPI.
- Déplacement des répertoires sensibles hors du répertoire web.

---

## Conclusion
GLPI est désormais installé et opérationnel. Pour plus d'informations, consultez la documentation officielle ou le [répertoire GitHub de GLPI](https://github.com/glpi-project/glpi/releases).
