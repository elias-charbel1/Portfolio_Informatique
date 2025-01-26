## Table des Matières
1. [Objectifs](#objectifs)
2. [Configuration de la Machine Virtuelle](#1-configuration-de-la-machine-virtuelle)
   1. [Outil Utilisé](#outil-utilisé)
   2. [Configuration de la VM](#configuration-de-la-vm)
3. [Installation et Configuration](#2-installation-et-configuration)
   1. [Configuration SSH](#21-configuration-ssh)
   2. [Installation des Dépendances](#22-installation-des-dépendances)
      1. [Apache2](#apache2)
      2. [PHP](#php)
      3. [MariaDB](#mariadb)
      4. [Modules PHP supplémentaires](#modules-php-supplémentaires)
   3. [Sécurisation et création de la base de données MariaDB](#23-sécurisation-et-création-de-la-base-de-données-mariadb)
   4. [Installation de GLPI](#24-installation-de-glpi)
   5. [Configuration via l'interface web](#25-configuration-via-linterface-web)
4. [Sécurisation](#3-sécurisation)
5. [Conclusion](#4-conclusion)


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

#### Apache2
- Installer Apache2, le serveur web utilisé pour héberger GLPI.
```bash
sudo apt install apache2 -y
```
- Vérifier que le service Apache2 fonctionne correctement.
```bash
systemctl status apache2
```

#### PHP
- Installer PHP, nécessaire pour exécuter les scripts de GLPI.
```bash
sudo apt install php -y
```

- Vérifier que PHP est installé et connaître la version installée.
```bash
php -v
```
#### MariaDB
- Installer MariaDB, la base de données utilisée par GLPI.
```bash
sudo apt install mariadb-server -y
```
- Vérifier que le service MariaDB fonctionne correctement.
```bash
systemctl status mariadb
```
#### Modules PHP supplémentaires
- Installer les modules PHP nécessaires pour qu'Apache2 prenne en charge les scripts de GLPI.
```bash
sudo apt install php libapache2-mod-php -y
```
- Redémarrer Apache2 pour appliquer les modifications.
```bash
sudo systemctl restart apache2
```
### 2.3 Sécurisation et création de la base de données MariaDB  
Lancez la configuration sécurisée de MariaDB.  
```bash
sudo mysql_secure_installation
```
---  

Connectez-vous en tant que root dans MariaDB.  
```bash
sudo mysql -u root
```
---  

Créez la base de données et configurez les utilisateurs.  
```sql
CREATE DATABASE glpi;
CREATE USER 'glpi'@'localhost' IDENTIFIED BY 'glpi';
GRANT ALL PRIVILEGES ON glpi.* TO 'glpi'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
QUIT;
```
---  

3. Installation de GLPI  
Téléchargez GLPI depuis le dépôt officiel GitHub.  
```bash
wget https://github.com/glpi-project/glpi/releases/download/10.0.17/glpi-10.0.17.tgz
```
Extrayez les fichiers et déplacez-les vers le répertoire web d’Apache.  
```bash
tar -xvzf glpi-10.0.17.tgz
sudo mv glpi /var/www/html/glpi
```
Installez les modules PHP nécessaires pour GLPI.  
```bash
cd /var/www/html
sudo apt install -y php-curl php-gd php-mbstring php-zip php-xml php-ldap php-intl php-mysql php-dom php-simplexml php-json php-phar php-pdo php-cgi
```
Donnez les permissions nécessaires aux fichiers GLPI.  
```bash
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi
```
Redémarrez Apache pour appliquer les modifications.  
```bash
systemctl restart apache2
```
4. Configuration via l'interface web  
Accédez à l'interface web en ouvrant l’URL suivante dans votre navigateur :  
http://adresseIPmachine/glpi  

Configurez la connexion à la base de données :  
- Serveur : localhost  
- Utilisateur : glpi  
- Mot de passe : glpi  
- Base de données : glpi  

Suivez les étapes d'installation guidée dans l'interface web.  

5. Sécurisation  
Changez le mot de passe de l'administrateur GLPI pour renforcer la sécurité.  

Déplacez les répertoires sensibles (comme les logs et les fichiers de configuration) hors du répertoire web pour éviter qu’ils ne soient accessibles depuis l’extérieur.  


6. Conclusion  
L’interface GLPI est maintenant installée et opérationnelle. Vous pouvez commencer à l’utiliser pour gérer votre parc informatique. Pour plus de détails, consultez la documentation officielle de GLPI.
