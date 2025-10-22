# Core-AD — Promotion du contrôleur de domaine (SRV-ADDS)

## Objectif

Promotion du serveur SRV-ADDS en contrôleur de domaine pour le domaine **dexter.lab**  
(équivalent du lab corp.lab dans le guide).

---

## Étapes réalisées

1. Installation du rôle **Active Directory Domain Services (AD DS)** via le Server Manager.  
   → DNS installé automatiquement.

2. Promotion du serveur :

   - **Add a new forest**
   - **Root domain name :** dexter.lab
   - **NetBIOS name :** DEXTER
   - **DSRM password :** défini et noté en coffre (non stocké dans Git)
   - **Domain/Forest functional level :** Windows Server 2016 (par défaut)
   - DNS intégré, options par défaut, redémarrage automatique.

3. Après redémarrage :
   - Domaine opérationnel : `dexter.lab`
   - Contrôleur : `SRV-ADDS.dexter.lab`
   - DNS et AD DS en état OK (`dcdiag` et `nslookup` testés).

---

## Validation

- `hostname` → SRV-ADDS
- `echo %USERDOMAIN%` → DEXTER
- `Get-WindowsFeature AD-Domain-Services` → Installed = True

---

## Notes

- Niveaux fonctionnels 2016 conservés pour compatibilité.
- Aucun second DC pour le moment.
