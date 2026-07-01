# 01 - Users Creation

## 📖 Objectif

Cette première étape consiste à préparer l'environnement Active Directory en créant l'Unité d'Organisation (OU) dédiée au service **Comptabilité** ainsi que les comptes utilisateurs qui seront utilisés tout au long du laboratoire.

L'objectif est de mettre en place une structure claire et évolutive avant la configuration des groupes de sécurité et des permissions.

---

## 🎯 Objectifs de cette étape

- Créer l'OU **Compta**.
- Créer les comptes utilisateurs du service Comptabilité.
- Organiser les utilisateurs dans une unité d'organisation dédiée.
- Préparer l'implémentation du modèle **AGDLP**.

---

## 🏗️ Structure de l'OU

```text
evilcorp.local
│
└── Compta
    │
    ├── compta_manager
    ├── compta_user
    └── compta_extern_user
```

---

## 👥 Comptes utilisateurs

| Utilisateur | Description |
|-------------|-------------|
| **compta_manager** | Responsable du service Comptabilité disposant d'un accès en lecture/écriture. |
| **compta_user** | Employé du service Comptabilité disposant d'un accès en lecture/écriture. |
| **compta_extern_user** | Utilisateur externe disposant uniquement d'un accès en lecture. |

---

## 📸 Captures d'écran

### Création de l'OU Compta

> Ajouter la capture d'écran.

---

### Création des comptes utilisateurs

> Ajouter la capture d'écran.

---

### Vérification dans Active Directory Users and Computers

> Ajouter la capture d'écran.

---

## ✅ Résultat

À l'issue de cette étape :

- Une OU **Compta** a été créée.
- Les trois comptes utilisateurs ont été créés avec succès.
- Les utilisateurs sont correctement organisés dans leur unité d'organisation.
- L'environnement est prêt pour la création des groupes de sécurité et l'implémentation du modèle **AGDLP**.

---

## ➡️ Étape suivante

La prochaine étape consiste à créer les **Global Groups (GG)** et les **Domain Local Groups (GDL)** qui serviront à implémenter le modèle **AGDLP**.

→ **02-Group-Creation**
