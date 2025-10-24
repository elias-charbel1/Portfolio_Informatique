# Seed AD demo users & groups (GLPI test)

## 🎯 Objectif

Création d’un petit jeu de données dans l’AD pour préparer l’intégration GLPI (auth LDAP et profils de base).  
On crée une OU dédiée **GLPI-Users**, deux groupes (`IT-Helpdesk`, `Employees`) et trois utilisateurs (`User1..3`).

---

## ⚙️ Script exécuté sur SRV-ADDS

```powershell
Import-Module ActiveDirectory

# 1️⃣ Crée l’OU "GLPI-Users" à la racine du domaine
New-ADOrganizationalUnit -Name "GLPI-Users" -Path "DC=dexter,DC=lab" -ProtectedFromAccidentalDeletion $true

# 2️⃣ Crée les deux groupes
New-ADGroup "IT-Helpdesk" -GroupScope Global -Path "OU=GLPI-Users,DC=dexter,DC=lab"
New-ADGroup "Employees"  -GroupScope Global -Path "OU=GLPI-Users,DC=dexter,DC=lab"

# 3️⃣ Crée trois utilisateurs simples
1..3 | % {
  New-ADUser -Name "User$($_)" -SamAccountName "user$($_)" -GivenName "User" -Surname "$($_)" -EmailAddress "user$($_)@dexter.lab" `
    -AccountPassword (ConvertTo-SecureString "P@ssw0rd$($_)!" -AsPlainText -Force) -Enabled $true -Path "OU=GLPI-Users,DC=dexter,DC=lab"
}

# 4️⃣ Ajoute les utilisateurs aux groupes
Add-ADGroupMember "IT-Helpdesk" user1
Add-ADGroupMember "Employees" user1,user2,user3

# 5️⃣ (Bonus) crée un enregistrement DNS pour le futur serveur GLPI
Add-DnsServerResourceRecordA -Name "glpi" -ZoneName "dexter.lab" -IPv4Address 192.168.20.20
```

✅ Vérifications effectuées

OU GLPI-Users visible dans ADUC avec groupes et utilisateurs.

Groupes correctement remplis :

```powershell
Get-ADGroupMember "IT-Helpdesk"
Get-ADGroupMember "Employees"

```
