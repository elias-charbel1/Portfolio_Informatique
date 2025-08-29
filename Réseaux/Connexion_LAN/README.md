# Lab Réseaux : Connexion de deux LAN via un routeur

## 🎯 Objectifs
- Concevoir et configurer un réseau local multi-sites (Site A et Site B) reliés par un routeur
- Attribuer des adresses IP statiques et assurer la communication entre les deux LAN
- Tester la connectivité et documenter les résultats
- Identifier et analyser les menaces réseau liées à ce type d’architecture

## 🛠️ Environnement
- Cisco Packet Tracer (ou équivalent)
- Routeur, switchs et terminaux configurés
- Adressage IP manuel sur toutes les machines

## 📡 Topologie
- Fichier Packet Tracer : [Topologie_LAN.pkt](./Topologie_LAN.pkt)  
- Schéma visuel :  

![Topologie LAN](./Topologie_LAN.png)

## 🔄 Mise en œuvre
1. Création des deux LAN indépendants (Site A et Site B)
2. Configuration des terminaux avec des adresses IP statiques
3. Mise en place d’un routeur pour relier les deux LAN
4. Tests de connectivité (`ping`) entre les machines des deux sites
5. Analyse des menaces possibles et contre-mesures

## 🔐 Sécurité
Deux attaques fréquentes pouvant cibler un réseau local :  
- **Ping of Death** : envoi de paquets ICMP malveillants trop volumineux → risque d’interruption de service  
- **SYN Flood** : saturation de la phase d’initialisation TCP → risque de non-disponibilité  

👉 Voir la documentation détaillée : [Menaces_Réseaux.md](../Menaces_Réseaux.md)

## ✅ Résultats
- Communication validée entre toutes les machines des deux LAN
- Routage opérationnel et adressage IP fonctionnel
- Identification et compréhension des menaces principales et des solutions de mitigation
