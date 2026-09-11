Lab 01 — Gestion des identités Microsoft Entra ID

AZ-104 — Microsoft Azure Administrator

 ## Objectif

Mettre en pratique la gestion des identités et des groupes dans Microsoft Entra ID à travers la création d'utilisateurs, l'invitation d'un utilisateur externe et la création d'un groupe de sécurité.

## Compétences mises en pratique
Gestion des utilisateurs Microsoft Entra ID
Gestion des utilisateurs externes (Guest)
Création et gestion de groupes
Gestion des membres et propriétaires
Appartenance de groupe Assigned
Organisation des identités
## Réalisation
**1. Création d'un utilisateur**

Création de l'utilisateur usr-tech01 dans Microsoft Entra ID avec les informations demandées par le scénario.

Chemin :

*Portail Azure → Microsoft Entra ID → Utilisateurs → Nouvel(le) utilisateur(-trice)*

Configuration principale :

Nom : usr-tech01
Job title : IT Lab Administrator
Department : IT
Compte : Activé

<img width="1213" height="1062" alt="Capture d&#39;écran 2026-08-27 151408" src="https://github.com/user-attachments/assets/11384696-5d82-4bdf-bade-f2b5c4a3e2aa" />


**2. Vérification de l'utilisateur**

Vérification de la présence du compte dans la liste des utilisateurs Microsoft Entra ID.

Chemin :

*Microsoft Entra ID → Utilisateurs → Tous les utilisateurs*

<img width="2070" height="703" alt="Capture d&#39;écran 2026-08-27 152217" src="https://github.com/user-attachments/assets/6a728e8e-04cb-41e3-a817-ea3ec3a1671b" />


**3. Invitation d'un utilisateur externe**

Invitation d'un utilisateur externe afin de mettre en pratique la gestion des identités Guest.

Chemin :

*Microsoft Entra ID → Utilisateurs → Nouvel(le) utilisateur(-trice) → Inviter un utilisateur externe*

<img width="922" height="849" alt="Capture d&#39;écran 2026-08-27 153701" src="https://github.com/user-attachments/assets/d7d31948-b5f6-45ef-a906-2ab4602de8e5" />

**4. Création du groupe de sécurité**

Création du groupe IT Lab Administrators afin de regrouper les utilisateurs concernés par l'administration de l'environnement.

Chemin :

*Microsoft Entra ID → Groupes → Nouveau Groupe*

Paramètre	Valeur
Type	Security
Nom	IT Lab Administrators
Membership type	Assigned

<img width="888" height="704" alt="Capture d&#39;écran 2026-08-27 154014" src="https://github.com/user-attachments/assets/f12aa001-8ac6-4cd1-a3ca-84aace54bcea" />


**5. Gestion des propriétaires et des membres**

Définition d'un propriétaire puis ajout des utilisateurs au groupe.

Chemin :

*Microsoft Entra ID → Groupes → IT Lab Administrators → Propriétaires / Membres*

<img width="824" height="578" alt="Capture d&#39;écran 2026-08-27 154040" src="https://github.com/user-attachments/assets/a0a9288a-97df-4415-b5f3-1f7f72709c64" />


## Résultat

Le groupe IT Lab Administrators a été créé avec succès et les utilisateurs prévus par le scénario ont été associés au groupe.

<img width="975" height="666" alt="Capture d&#39;écran 2026-08-27 154139" src="https://github.com/user-attachments/assets/b1ee3b5d-837c-4f66-9573-670d32e50c8f" />


L'environnement dispose désormais d'une première organisation des identités permettant de préparer la gestion des autorisations Azure.

## Ce que j'ai appris

Ce lab m'a permis de comprendre les bases de la gestion des identités dans Microsoft Entra ID et notamment l'intérêt des groupes pour organiser les utilisateurs.

J'ai également découvert la gestion des utilisateurs externes ainsi que la différence entre une appartenance de groupe Assigned et Dynamic.

## Approche professionnelle

Dans un environnement d'entreprise, l'organisation des identités permet de simplifier l'administration et de préparer une gestion structurée des accès.

L'utilisation de groupes permet notamment d'éviter de gérer individuellement chaque utilisateur lorsqu'ils doivent bénéficier de permissions similaires.

Le prochain lab permettra d'aller plus loin avec Azure RBAC, afin de déterminer précisément quelles actions les utilisateurs ou groupes sont autorisés à effectuer.

## Source

Lab basé sur le parcours pratique Microsoft Learning — AZ-104 Microsoft Azure Administrator.

Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
