# Lab 06 — Gestion du stockage Azure

AZ-104 — Microsoft Azure Administrator

## Objectif

Mettre en place et sécuriser une solution de stockage Azure.

L'objectif est de créer un compte de stockage, de gérer des données Blob et Azure Files, puis de configurer différents mécanismes de sécurité et d'accès.

## Compétences mises en pratique
Création d'un compte de stockage Azure
Configuration de la redondance
Gestion du stockage Blob
Gestion du cycle de vie des données
Configuration des accès RBAC et SAS
Création d'un partage Azure Files
Utilisation de Storage Browser
Configuration de l'accès réseau
Utilisation des points de terminaison de service
## Realisation
  1. Création du compte de stockage

Création d'un compte de stockage Azure destiné à héberger les données utilisées pendant le lab.

Le groupe de ressources utilisé est :

Nom : AZ-104-LAB06

Chemin :

**Portail Azure → Comptes de stockage → Créer**

Configuration principale :

Nom : nom unique du compte de stockage
Performance : Standard
Redondance : GRS

<img width="1007" height="979" alt="image" src="https://github.com/user-attachments/assets/75bcbe53-b094-464e-89b7-410e824e0ef2" />

  2. Configuration de l'accès réseau du compte de stockage afin de limiter son exposition et contrôler les connexions autorisées.

Chemin :

**Portail Azure → Comptes de stockage → Compte de stockage → Mise en réseau**

Configuration de l'accès public et des règles réseau selon les besoins du lab.

<img width="998" height="982" alt="image" src="https://github.com/user-attachments/assets/414e9245-e3fa-4070-811a-3c4ecaad9cb1" />

  3. Création d'une règle permettant de déplacer automatiquement les données peu utilisées vers un niveau de stockage moins coûteux.

Chemin :

**Portail Azure → Comptes de stockage → Compte de stockage → Gestion des données → Gestion du cycle de vie**

Configuration :

Nom : Movetocool
Condition : blobs non modifiés depuis 30 jours
Action : déplacer vers le niveau Cool

<img width="680" height="722" alt="image" src="https://github.com/user-attachments/assets/102bae59-6166-4e31-8f92-dece10de9da3" />
<img width="1273" height="1747" alt="image" src="https://github.com/user-attachments/assets/f071e393-d4a2-46eb-b3e4-c04277a149ca" />

  4. Création d'un conteneur Blob privé puis téléversement d'un fichier afin de tester la gestion des données.

Chemin :

**Portail Azure → Comptes de stockage → Compte de stockage → Stockage de données → Conteneurs → Ajouter**

Configuration :

Nom : data
Niveau d'accès public : Privé

Téléversement d'un fichier dans le conteneur.

<img width="2328" height="1969" alt="image" src="https://github.com/user-attachments/assets/f62503dc-1abb-406a-adc3-2a8275a3dd77" />

  5. Mise en place d'une stratégie de rétention afin d'empêcher la modification ou la suppression des données pendant une période définie.

Une URL SAS est ensuite générée afin de fournir un accès temporaire au fichier Blob.

Chemin :

**Portail Azure → Comptes de stockage → Compte de stockage → Conteneurs → data**

Puis :

Fichier Blob → Générer un SAS

<img width="2142" height="1957" alt="image" src="https://github.com/user-attachments/assets/b6d49a6c-caa4-4e44-8154-885d2066270e" />

  6. Attribution des rôles permettant de contrôler les droits d'accès aux données du compte de stockage.

Chemin :

**Portail Azure → Comptes de stockage → Compte de stockage → Contrôle d'accès (IAM) → Ajouter une attribution de rôle**

Rôles utilisés :

Storage Blob Data Contributor
Storage File Data Privileged Contributor

<img width="1166" height="986" alt="image" src="https://github.com/user-attachments/assets/eb56fa13-3d05-422a-a5e0-7bdf3338bee2" />

  7. Création d'un partage de fichiers Azure permettant de stocker et gérer des fichiers de manière similaire à un partage réseau traditionnel.

Chemin :

**Portail Azure → Comptes de stockage → Compte de stockage → Stockage de données → Partages de fichiers → Ajouter**

Configuration :

Nom : share1
Niveau d'accès : Transaction optimisée

<img width="883" height="885" alt="image" src="https://github.com/user-attachments/assets/9f1c4192-43c5-4888-9ce3-4da7ce138185" />

## Ce que j'ai appris

Ce lab m'a permis de mettre en pratique plusieurs éléments de la gestion du stockage Azure :

- création d'un compte de stockage ;
- configuration de la redondance ;
- gestion des données Blob ;
- mise en place d'une règle de cycle de vie ;
- configuration des accès RBAC et SAS ;
- création d'un partage Azure Files ;
- utilisation de Storage Browser ;
- configuration de la sécurité réseau.

J'ai compris comment Azure Storage permet de gérer différents types de données et de choisir une configuration adaptée aux besoins de l'infrastructure.

J'ai également compris l'intérêt de la gestion du cycle de vie pour optimiser les coûts ainsi que l'utilisation de RBAC et des SAS pour contrôler l'accès aux données.

Enfin, j'ai découvert comment sécuriser l'accès au stockage en utilisant un réseau virtuel et un point de terminaison de service.

## Approche professionnelle

Dans un environnement professionnel, Azure Storage permet de centraliser les données tout en assurant leur disponibilité et leur sécurité.

Les règles de cycle de vie permettent d'optimiser les coûts, tandis que RBAC, les SAS et les règles réseau permettent de contrôler précisément l'accès aux données.

Azure Files peut également être utilisé pour fournir des partages de fichiers accessibles depuis différents environnements.

## Source

Lab basé sur les exercices pratiques Microsoft Learning — AZ-104 Microsoft Azure Administrator.

Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
