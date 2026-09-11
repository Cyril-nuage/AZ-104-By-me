Lab 07 — Gestion du stockage Azure

AZ-104 — Microsoft Azure Administrator

Objectif

Mettre en place et sécuriser une solution de stockage Azure.

L'objectif est de créer un compte de stockage, de gérer des données Blob et Azure Files, puis de configurer différents mécanismes de sécurité et d'accès.

Compétences mises en pratique
Création d'un compte de stockage Azure
Configuration de la redondance
Gestion du stockage Blob
Gestion du cycle de vie des données
Configuration des accès RBAC et SAS
Création d'un partage Azure Files
Utilisation de Storage Browser
Configuration de l'accès réseau
Utilisation des points de terminaison de service
Realisation
Création du compte de stockage

Création d'un compte de stockage Azure destiné à héberger les données utilisées pendant le lab.

Le groupe de ressources utilisé est :

Nom : AZ-104-LAB07

☀️ Chemin :

Portail Azure → Comptes de stockage → Créer

Configuration principale :

Nom : nom unique du compte de stockage
Performance : Standard
Redondance : GRS

📸 Capture à mettre :

Configuration principale du compte de stockage
Nom
Région
Performance Standard
Redondance GRS
Configuration de la sécurité et du réseau

Configuration de l'accès réseau du compte de stockage afin de limiter son exposition et contrôler les connexions autorisées.

☀️ Chemin :

Portail Azure → Comptes de stockage → Compte de stockage → Mise en réseau

Configuration de l'accès public et des règles réseau selon les besoins du lab.

📸 Capture à mettre :

Page « Mise en réseau »
Configuration de l'accès réseau
Règles réseau configurées
Gestion du cycle de vie

Création d'une règle permettant de déplacer automatiquement les données peu utilisées vers un niveau de stockage moins coûteux.

☀️ Chemin :

Portail Azure → Comptes de stockage → Compte de stockage → Gestion des données → Gestion du cycle de vie

Configuration :

Nom : Movetocool
Condition : blobs non modifiés depuis 30 jours
Action : déplacer vers le niveau Cool

📸 Capture à mettre :

Règle de cycle de vie
Condition des 30 jours
Passage vers le niveau Cool
Création et gestion d'un conteneur Blob

Création d'un conteneur Blob privé puis téléversement d'un fichier afin de tester la gestion des données.

☀️ Chemin :

Portail Azure → Comptes de stockage → Compte de stockage → Stockage de données → Conteneurs → Ajouter

Configuration :

Nom : data
Niveau d'accès public : Privé

Téléversement d'un fichier dans le conteneur.

📸 Capture à mettre :

Conteneur data
Niveau d'accès privé
Fichier présent dans le conteneur
Sécurisation et accès au Blob

Mise en place d'une stratégie de rétention afin d'empêcher la modification ou la suppression des données pendant une période définie.

Une URL SAS est ensuite générée afin de fournir un accès temporaire au fichier Blob.

☀️ Chemin :

Portail Azure → Comptes de stockage → Compte de stockage → Conteneurs → data

Puis :

Fichier Blob → Générer un SAS

📸 Capture à mettre :

Stratégie de rétention configurée
Génération du SAS
Permission de lecture
Date d'expiration
Configuration des autorisations RBAC

Attribution des rôles permettant de contrôler les droits d'accès aux données du compte de stockage.

☀️ Chemin :

Portail Azure → Comptes de stockage → Compte de stockage → Contrôle d'accès (IAM) → Ajouter une attribution de rôle

Rôles utilisés :

Storage Blob Data Contributor
Storage File Data Privileged Contributor

📸 Capture à mettre :

Attribution des rôles RBAC
Utilisateur concerné
Rôles attribués
Création d'un partage Azure Files

Création d'un partage de fichiers Azure permettant de stocker et gérer des fichiers de manière similaire à un partage réseau traditionnel.

☀️ Chemin :

Portail Azure → Comptes de stockage → Compte de stockage → Stockage de données → Partages de fichiers → Ajouter

Configuration :

Nom : share1
Niveau d'accès : Transaction optimisée

📸 Capture à mettre :

Partage share1
Niveau d'accès configuré
Partage créé
Utilisation de Storage Browser

Utilisation de Storage Browser pour consulter et gérer les données du compte de stockage directement depuis le portail Azure.

☀️ Chemin :

Portail Azure → Comptes de stockage → Compte de stockage → Explorateur de stockage

📸 Capture à mettre :

Storage Browser
Partage share1
Fichier présent dans le partage
Restriction de l'accès avec un réseau virtuel

Création d'un réseau virtuel et configuration d'un point de terminaison de service afin de limiter l'accès au compte de stockage.

Le réseau virtuel est ensuite autorisé dans les règles réseau du compte de stockage.

☀️ Chemin :

Portail Azure → Réseaux virtuels → Créer

Puis :

Réseau virtuel → Sous-réseaux → Points de terminaison de service → Microsoft.Storage

Puis :

Portail Azure → Comptes de stockage → Compte de stockage → Mise en réseau

📸 Capture à mettre :

Réseau virtuel créé
Point de terminaison Microsoft.Storage
Réseau virtuel autorisé dans le compte de stockage
Comparaison des éléments
Élément | Utilisation
Storage Account | Centraliser les services de stockage Azure
Blob Storage | Stocker des données non structurées
Container | Organiser les données Blob
Lifecycle Management | Automatiser la gestion du stockage
RBAC | Contrôler les autorisations
SAS | Fournir un accès temporaire aux données
Azure Files | Fournir un stockage de fichiers partagé
Storage Browser | Gérer les données depuis Azure
Service Endpoint | Sécuriser l'accès au stockage depuis un réseau virtuel
Résultat

Ce lab m'a permis de mettre en pratique plusieurs éléments de la gestion du stockage Azure :

création d'un compte de stockage ;
configuration de la redondance ;
gestion des données Blob ;
mise en place d'une règle de cycle de vie ;
configuration des accès RBAC et SAS ;
création d'un partage Azure Files ;
utilisation de Storage Browser ;
configuration de la sécurité réseau.
Ce que j'ai appris

J'ai compris comment Azure Storage permet de gérer différents types de données et de choisir une configuration adaptée aux besoins de l'infrastructure.

J'ai également compris l'intérêt de la gestion du cycle de vie pour optimiser les coûts ainsi que l'utilisation de RBAC et des SAS pour contrôler l'accès aux données.

Enfin, j'ai découvert comment sécuriser l'accès au stockage en utilisant un réseau virtuel et un point de terminaison de service.

Approche professionnelle

Dans un environnement professionnel, Azure Storage permet de centraliser les données tout en assurant leur disponibilité et leur sécurité.

Les règles de cycle de vie permettent d'optimiser les coûts, tandis que RBAC, les SAS et les règles réseau permettent de contrôler précisément l'accès aux données.

Azure Files peut également être utilisé pour fournir des partages de fichiers accessibles depuis différents environnements.

Source

Lab basé sur les exercices pratiques Microsoft Learning — AZ-104 Microsoft Azure Administrator.

Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
