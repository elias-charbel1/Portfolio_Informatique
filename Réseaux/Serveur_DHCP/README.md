# Lab Réseaux : Serveur DHCP multi-sous-réseaux

## 🎯 Objectifs
- Mettre en place un serveur DHCP pour attribuer automatiquement des adresses IP
- Configurer deux pools d’adresses pour deux sous-réseaux distincts
- Tester l’attribution automatique d’adresses IP sur tous les terminaux
- Configurer le “IP Helper” pour permettre le routage DHCP entre les sous-réseaux
- Vérifier la connectivité et documenter les résultats

## 🛠️ Environnement
- Cisco Packet Tracer (ou équivalent)
- Routeur, switchs, serveur DHCP et terminaux configurés
- Adressage IP dynamique via DHCP

## 📡 Topologie
- Fichier Packet Tracer : [Topologie_DHCP.pkt](./Topologie_DHCP.pkt)  
- Schéma visuel :  

![Topologie DHCP](./Topologie_DHCP.png)

## 🔄 Mise en œuvre
1. Création de deux sous-réseaux distincts dans le LAN
2. Configuration du serveur DHCP avec deux pools d’adresses IP
3. Configuration de l’“IP Helper” sur le routeur pour relayer les requêtes DHCP
4. Test de l’attribution automatique des adresses IP sur tous les terminaux
5. Vérification de la connectivité et de la communication entre les machines

## ✅ Résultats
- Attribution automatique des IP fonctionnelle sur les deux sous-réseaux
- Communication validée entre tous les terminaux
- Compréhension de la configuration DHCP multi-sous-réseaux et du relai DHCP
