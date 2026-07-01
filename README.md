# AD-File-Share-Lab

> Laboratoire pratique mettant en œuvre le modèle **AGDLP** dans un environnement **Active Directory** afin de sécuriser un partage **SMB** à l'aide des permissions **NTFS** et des groupes de sécurité.

---

# 📖 Présentation

Ce projet a pour objectif de démontrer la mise en œuvre du modèle **AGDLP (Accounts → Global Groups → Domain Local Groups → Permissions)** dans un environnement **Active Directory** sous **Windows Server 2019**.

Le laboratoire simule un service **Comptabilité** où les utilisateurs disposent de différents niveaux d'accès à un partage réseau SMB. Les autorisations sont attribuées aux **groupes de sécurité** plutôt qu'aux utilisateurs, conformément aux bonnes pratiques Microsoft et au modèle AGDLP.

Dans une seconde partie, le laboratoire sera analysé du point de vue d'un **Pentester** puis d'un **Analyste SOC**, afin d'illustrer les techniques d'énumération d'un domaine Active Directory et la validation des permissions.

---

# 🎯 Objectifs

- Déployer un environnement Active Directory.
- Créer une structure d'**Unités d'Organisation (Organizational Units - OU)**.
- Implémenter le modèle AGDLP.
- Configurer un partage SMB.
- Configurer les permissions de partage et les permissions NTFS.
- Vérifier les permissions effectives des utilisateurs.
- Réaliser une phase d'énumération Active Directory.
- Analyser l'infrastructure dans une approche Pentest et SOC.

---

# 📁 Structure du projet

Le projet est organisé en plusieurs étapes afin de suivre chronologiquement la mise en œuvre d'un partage SMB sécurisé dans un environnement Active Directory. Chaque dossier contient une documentation détaillée ainsi que les captures d'écran correspondantes.

```text
AD-File-Share-Lab/
│
├── 01-Users-Creation/
│   ├── Images/
│   └── README.md
│
├── 02-Group-Creation/
│   ├── Images/
│   └── README.md
│
├── 03-AGDLP-Implementation/
│   ├── Images/
│   └── README.md
│
├── 04-SMB-Share-Creation/
│   ├── Images/
│   └── README.md
│
├── 05-Share-and-NTFS-Permissions/
│   ├── Images/
│   └── README.md
│
├── 06-Permission-Validation/
│   ├── Images/
│   └── README.md
│
├── 07-Pentest/
│   ├── Images/
│   └── README.md
│
└── README.md
```

### Description des différentes étapes

| Étape | Description |
|--------|-------------|
| **01 - Users Creation** | Création de l'OU **Compta** et des comptes utilisateurs. |
| **02 - Group Creation** | Création des groupes de sécurité (**Global Groups** et **Domain Local Groups**). |
| **03 - AGDLP Implementation** | Ajout des utilisateurs dans les Global Groups puis intégration des Global Groups dans les Domain Local Groups. |
| **04 - SMB Share Creation** | Création du dossier partagé et publication du partage SMB. |
| **05 - Share and NTFS Permissions** | Configuration des permissions de partage et des permissions NTFS selon le principe du moindre privilège. |
| **06 - Permission Validation** | Vérification des droits effectifs avec différents comptes utilisateurs. |
| **07 - Pentest** | Énumération Active Directory, analyse des partages SMB, validation des permissions et analyse SOC. |

---

# 🖥️ Environnement du laboratoire

| Élément | Valeur |
|---------|--------|
| Système | Windows Server 2019 |
| Domaine | evilcorp.local |
| Contrôleur de domaine | 192.168.32.142 |
| Machine d'attaque | Debian Linux |
| Service étudié | SMB |
| Authentification | Active Directory |

---

# 🏗️ Architecture

> 📸 **Schéma de l'architecture du laboratoire**

```text
OU : Compta
│
├── compta_manager
├── compta_user
└── compta_extern_user

        │

Global Groups
│
├── GG_Comptables
└── GG_Users_Externe

        │

Domain Local Groups
│
├── GDL_Partages_RW
└── GDL_Partages_RO

        │

\\WIN-SERV2019\Compta
```

---

# 🔐 Implémentation du modèle AGDLP

Le laboratoire applique le modèle recommandé par Microsoft :

```text
Account
      ↓
Global Group
      ↓
Domain Local Group
      ↓
Permissions
```

### Accès Lecture / Écriture

```text
compta_manager
        ↓
GG_Comptables
        ↓
GDL_Partages_RW
        ↓
Lecture / Écriture
```

### Accès Lecture seule

```text
compta_extern_user
        ↓
GG_Users_Externe
        ↓
GDL_Partages_RO
        ↓
Lecture seule
```

---

# 📂 Configuration du partage SMB

Cette étape comprend :

- Création du dossier partagé.
- Publication du partage SMB.
- Configuration des permissions de partage.
- Attribution des groupes de sécurité.

> 📸 Ajouter les captures d'écran correspondantes.

---

# 🔒 Configuration des permissions NTFS

Les permissions sont configurées selon le **principe du moindre privilège**.

| Groupe | Permission |
|---------|------------|
| Administrators | Contrôle total |
| SYSTEM | Contrôle total |
| GDL_Partages_RW | Modification |
| GDL_Partages_RO | Lecture |

> 📸 Ajouter les captures d'écran correspondantes.

---

# ✅ Vérification des permissions

Les autorisations ont été testées avec plusieurs comptes utilisateurs.

| Utilisateur | Lecture | Écriture | Suppression |
|-------------|:-------:|:--------:|:-----------:|
| compta_manager | ✅ | ✅ | ✅ |
| compta_user | ✅ | ✅ | ✅ |
| compta_extern_user | ✅ | ❌ | ❌ |

Les tests confirment que les permissions sont correctement héritées via les groupes de sécurité et respectent le modèle AGDLP.

---

# 🛡️ Partie Pentest *(À venir)*

La seconde partie du projet sera consacrée à l'évaluation de la sécurité de l'infrastructure depuis une machine **Debian**, afin de reproduire les techniques d'énumération qu'un attaquant pourrait utiliser sur un domaine **Active Directory**.

Elle comprendra notamment :

- Reconnaissance SMB.
- Énumération Active Directory.
- Identification des utilisateurs.
- Identification des groupes.
- Analyse des partages SMB.
- Validation des permissions.
- Vérification de l'implémentation AGDLP.
- Analyse des résultats dans une démarche SOC.

---

# 💡 Compétences mises en œuvre

- Administration Active Directory
- Gestion des Unités d'Organisation (OU)
- Gestion des utilisateurs et des groupes de sécurité
- Implémentation du modèle AGDLP
- Configuration des partages SMB
- Gestion des permissions NTFS
- Contrôle d'accès
- Windows Server 2019
- Administration Linux
- Énumération Active Directory
- Pentest
- Analyse SOC

---

# 🚀 Améliorations futures

- Analyse avec BloodHound.
- Énumération LDAP.
- Analyse de l'authentification Kerberos.
- Capture du trafic SMB avec Wireshark.
- Analyse des journaux Windows.
- Mapping MITRE ATT&CK.
- Détection et corrélation dans un SOC.

---

# 📜 Licence

Ce projet est réalisé à des fins d'apprentissage et de démonstration des bonnes pratiques en administration système, Active Directory et cybersécurité.
