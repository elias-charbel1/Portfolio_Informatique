Les réseaux sont souvent la cible d'attaques visant à perturber leur fonctionnement. Voici deux exemples courants et les solutions associées :

## Ping of Death
Le *Ping of Death* exploite une vulnérabilité en envoyant des paquets ICMP (Internet Control Message Protocol) trop volumineux, dépassant la limite maximale autorisée par le protocole IP (65 535 octets). Lorsque la cible tente de reconstituer ces paquets, cela peut provoquer des plantages ou des interruptions de service.

**Solutions** :
- Configurer des pare-feu pour filtrer les paquets ICMP malveillants.
- Limiter la taille maximale des paquets ICMP autorisés.

---

## SYN Flood
Le *SYN Flood* est une attaque qui surcharge la phase d'initialisation des connexions TCP (*TCP three-way handshake*). L'attaquant envoie un grand nombre de requêtes SYN sans jamais compléter la connexion, ce qui sature la file d'attente du serveur et peut rendre le système indisponible.

**Solutions** :
- Mettre en place des pare-feu pour détecter et bloquer les paquets SYN suspects.
- Activer des mécanismes comme les SYN Cookies pour gérer efficacement les connexions incomplètes.
- Réduire le délai d'attente des connexions non confirmées.
