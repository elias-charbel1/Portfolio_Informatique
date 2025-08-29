# Lab Administration : Installation GLPI – Agence Rue25

## 🎯 Objectifs
- Créer une machine virtuelle Debian 11.6 pour héberger GLPI
- Installer et configurer les dépendances nécessaires (Apache, PHP, MariaDB)
- Installer GLPI et sécuriser l’accès via l’interface web
- Documenter l’installation et la configuration

## 🛠️ Environnement
- Machine virtuelle : VirtualBox / VMware
- OS : Debian 11.6 (sans interface graphique)
- Configuration VM :
  - CPU : 1
  - RAM : 2 Go
  - Stockage : 20 Go
- Accès SSH pour administration

## 🔄 Mise en œuvre

### 1️⃣ Création de la machine virtuelle
- Installation de Debian 11.6 sans interface graphique
- Création d’un utilisateur avec droits sudo pour administration sécurisée

### 2️⃣ Installation et configuration de SSH
```bash
sudo apt install openssh-server -y
sudo systemctl status ssh
ssh user@adresseIPmachine  # test de connexion depuis l’hôte
```

### 3️⃣ Installation des dépendances
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2 -y
sudo systemctl status apache2
sudo apt install php libapache2-mod-php -y
sudo apt install mariadb-server -y
sudo systemctl status mariadb
sudo systemctl restart apache2
```

### 4️⃣ Sécurisation et création de la base de données
```bash
sudo mysql_secure_installation
sudo mysql -u root
# Dans MariaDB
create database glpi;
create user 'glpi'@'localhost' identified by 'glpi';
grant all privileges on glpi.* to 'glpi'@'localhost' with grant option;
flush privileges;
quit;
```

### 5️⃣ Installation de GLPI
```bash
wget https://github.com/glpi-project/glpi/releases/download/10.0.17/glpi-10.0.17.tgz
tar -xvzf glpi-10.0.17.tgz
sudo mv glpi /var/www/html/glpi
cd /var/www/html
sudo apt install -y php-curl php-gd php-mbstring php-zip php-xml php-ldap php-intl php-mysql php-dom php-simplexml php-json php-phar php-pdo php-cgi
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi
systemctl restart apache2
```

### 6️⃣ Configuration via l’interface web

Accès à l’interface : http://adresseIPmachine/glpi

Connexion à la base de données :

Serveur : localhost

Utilisateur : glpi

Mot de passe : glpi

Base de données : glpi

Suivi des étapes d’installation de GLPI

### 7️⃣ Sécurisation

Changement du mot de passe administrateur GLPI

Déplacement des répertoires sensibles hors du répertoire web

✅ Résultats

Interface GLPI opérationnelle et accessible via le web

Base de données correctement configurée et sécurisée

Déploiement sur VM Debian fonctionnel

Documentation complète disponible pour référence interne
