# pfSense – Baseline de configuration & durcissement léger

**Objectif :** Mise en place du pare-feu pfSense avec réglages de base, durcissement léger et interopérabilité AD future.

---

### Objectifs techniques

- Sécuriser l’accès administrateur.
- Avoir des logs datés fiables (NTP/TZ).
- Ne pas exposer de service inutile (DNS pfSense désactivé vers clients).
- Structurer les règles par **alias** (lisibilité / audit).
- Séparer les droits entre **MGMT** (tout accès) et **USERS** (limités).
- Préparer la future intégration AD/DHCP relay.

---

## 1. Étapes de configuration

### 1.1 Compte administrateur

- **Chemin :** `System → User Manager → Users → admin`
- Changement du mot de passe `admin` par un mot de passe fort.
- Sauvegarde dans le coffre sécurisé (Bitwarden / KeePass).

**But :** éviter tout accès non autorisé.

---

### 1.2 Timezone & NTP

- **Timezone :** `System → General Setup → Timezone = Europe/Paris`
- **NTP :** `Services → NTP → Enable`
  - Interfaces : `LAN (MGMT)` uniquement
  - Upstream : serveurs NTP par défaut

**But :** cohérence temporelle (logs, corrélation SIEM).

---

### 1.3 WAN

- **Chemin :** `Interfaces → WAN`
  - Type : DHCP (NAT VBox)
  - **Block private networks and loopback : décoché**

**But :** autoriser le trafic NATé de VirtualBox (sinon Internet bloqué).

---

### 1.4 DNS Resolver (Unbound)

- **Chemin :** `Services → DNS Resolver`
  - **Network Interfaces :** _Localhost uniquement_
  - **Outgoing Network Interfaces :** _WAN_
  - **Enable DNSSEC Support :** activé (par défaut)
- **DNS Forwarder (dnsmasq) :** désactivé

**But :** pfSense ne répond pas aux clients en DNS, seuls les serveurs AD feront résolution interne.

---

### 1.5 Aliases

- **Chemin :** `Firewall → Aliases → IP`

| Nom           | Type    | Valeur          | Commentaire         |
| ------------- | ------- | --------------- | ------------------- |
| `NET_USERS`   | Network | 192.168.10.0/24 | VLAN Utilisateurs   |
| `NET_SERVERS` | Network | 192.168.20.0/24 | VLAN Serveurs       |
| `NET_MGMT`    | Network | 192.168.99.0/24 | VLAN Administration |
| `SRV_DNS`     | Host(s) | 192.168.20.10   | Serveur DNS/AD      |

**But :** rendre les règles lisibles et auditables.

---

### 1.6 Règles LAN (MGMT)

- **Chemin :** `Firewall → Rules → LAN`

| Action | Source   | Destination   | Protocole | Port(s) | Commentaire         |
| ------ | -------- | ------------- | --------- | ------- | ------------------- |
| Pass   | NET_MGMT | This Firewall | TCP       | 443     | Accès GUI pfSense   |
| Pass   | NET_MGMT | This Firewall | ICMP      | -       | Ping pfSense        |
| Pass   | NET_MGMT | any           | any       | any     | Accès complet admin |

**Remarque :** “Default allow LAN to any” désactivée.  
**But :** réseau d’administration totalement libre pour maintenance et supervision.

---

### 1.7 Règles USERS (OPT1)

- **Chemin :** `Firewall → Rules → USERS`

| Action            | Source    | Destination   | Protocole | Port(s) | Commentaire                 |
| ----------------- | --------- | ------------- | --------- | ------- | --------------------------- |
| Pass              | NET_USERS | SRV_DNS       | TCP/UDP   | 53      | DNS vers AD                 |
| Pass              | NET_USERS | This Firewall | UDP       | 67-68   | DHCP Relay vers AD          |
| Pass (temporaire) | NET_USERS | any           | TCP       | 80,443  | Accès web temporaire (test) |

**Remarque :** “Default allow Users to any” désactivée.  
**But :** limiter les postes utilisateurs à DNS/DHCP + navigation temporaire.

---

### 1.8 DHCP Relay

- **Chemin :** `Services → DHCP Relay`
  - Interface : USERS
  - Serveur : 192.168.20.10
  - Enable : décoché (en attente d’AD/DHCP)

**But :** préparer le relais DHCP sans perturber le réseau.

---

## 2. Vérifications & tests de validation

### 2.1 Depuis Windows (PowerShell)

### 2.2 Depuis la console pfSense (Shell)
