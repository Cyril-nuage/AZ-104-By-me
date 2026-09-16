# Lab 08 — Mise en place des applications Web et conteneurisées

AZ-104 — Microsoft Azure Administrator

## Objectif

Mettre en pratique plusieurs solutions Azure de calcul PaaS permettant d'héberger des applications Web et conteneurisées.

Le lab regroupe la mise en place d'une Azure Web App, la gestion d'un slot de déploiement, le déploiement d'une application depuis GitHub, la mise à l'échelle automatique ainsi que le déploiement d'Azure Container Instances et d'Azure Container Apps.

## Compétences mises en pratique

Création et configuration d'une Azure Web App
Gestion d'un App Service Plan
Création et gestion de Deployment Slots
Déploiement d'une application depuis GitHub
Échange entre environnements Staging et Production
Mise à l'échelle automatique d'une Web App
Déploiement d'Azure Container Instances
Utilisation d'images Docker
Déploiement d'Azure Container Apps
Gestion d'un environnement Container Apps
Vérification d'applications conteneurisées

## Environnement

Microsoft Azure
Azure App Service
Azure Web Apps
Azure Container Instances
Azure Container Apps
GitHub
Azure Load Testing
Resource Group : AZ-104-LAB8

## Réalisation

# Partie 1 — Azure Web Apps

## 1. Création de l'Azure Web App

Création d'une application Web Azure permettant d'héberger une application PHP.

Chemin :

**Portail Azure → App Services → Créer → Application Web**

Configuration principale :

Groupe de ressources : AZ-104-LAB8
Nom : nom unique au niveau mondial
Publication : Code
Pile d'exécution : PHP 8.3
Système d'exploitation : Linux
Région : région Azure disponible
Plan tarifaire : Gratuit F1 (1 Go de mémoire)

Valider la configuration puis créer la Web App.

<img width="957" height="983" alt="image" src="https://github.com/user-attachments/assets/89c36949-3607-4bde-b787-c57b9f8b75c1" />

## 2. Vérification de la Web App

Une fois le déploiement terminé, ouvrir la ressource créée.

Chemin :

**Portail Azure → App Services → Nom de la Web App → Vue d'ensemble**

Ouvrir le lien du domaine par défaut afin de vérifier que l'application est accessible.

<img width="1639" height="799" alt="image" src="https://github.com/user-attachments/assets/e935cbc0-2c1d-436f-ab8c-9a205649f656" />

## 3. Création du slot Staging

Création d'un environnement de préproduction permettant de tester une nouvelle version de l'application avant son passage en production.

Chemin :

**Web App → Déploiement → Emplacements de déploiement → Ajouter**

Configuration :

Nom : staging
Cloner les paramètres : Ne pas cloner

Créer le slot puis ouvrir celui-ci.

<img width="1140" height="775" alt="image" src="https://github.com/user-attachments/assets/d9ccd2b9-1555-4aa6-9388-1edb7bbac883" />
<img width="1137" height="411" alt="image" src="https://github.com/user-attachments/assets/8872f651-be6a-45a3-a618-2ab2d12d5235" />

## 4. Vérification du slot Staging

Vérification de la présence du nouvel environnement et de son domaine spécifique.

Chemin :

**Web App → Déploiement → Emplacements de déploiement → staging**

Le slot Staging possède une URL différente de celle de la production.

<img width="1141" height="983" alt="image" src="https://github.com/user-attachments/assets/8c413541-8d3f-401c-8619-5bd0620dd925" />

## 5. Configuration du déploiement depuis GitHub

Activation des paramètres nécessaires afin de permettre le déploiement de l'application depuis un dépôt GitHub externe.

Chemin :

**Slot staging → Configuration → Paramètres généraux**

Activer l'authentification de base SCM si elle est désactivée puis appliquer les modifications.

Ensuite :

**Slot staging → Centre de déploiement → Paramètres**

Configurer :

Source : External Git
Dépôt : https://github.com/Azure-Samples/php-docs-hello-world
Branche : master

Enregistrer la configuration.
<img width="813" height="628" alt="image" src="https://github.com/user-attachments/assets/ced9888b-a917-4855-bd92-29e74b9098ad" />

## 6. Vérification du déploiement Staging

Attendre la fin du déploiement puis ouvrir le domaine du slot staging.

Chemin :

**Slot staging → Vue d'ensemble → Domaine par défaut**

Vérifier que la page Hello World est affichée.

<img width="1919" height="1014" alt="image" src="https://github.com/user-attachments/assets/60402f38-f88e-46b5-a96d-0d41e71b7f17" />

## 7. Passage de Staging vers Production

Une fois l'application validée dans l'environnement Staging, effectuer l'échange entre les deux environnements.

Chemin :

**Web App → Déploiement → Emplacements de déploiement → Swap**

Vérifier les paramètres puis sélectionner Start Swap.

Attendre la fin de l'opération.

<img width="1141" height="983" alt="image" src="https://github.com/user-attachments/assets/47563c8f-c966-4433-89e4-46cb35da8fee" />

## 8. Vérification de la Production

Ouvrir la Web App en production et vérifier que l'application précédemment testée dans Staging est maintenant disponible en Production.

Chemin :

**App Services → Web App → Vue d'ensemble → Domaine par défaut**

<img width="1913" height="1013" alt="image" src="https://github.com/user-attachments/assets/dcb6e459-c8a7-4441-b8ec-792cfa4c3b7c" />

## 9. Configuration de la mise à l'échelle automatique

Configuration de l'autoscaling afin que la Web App puisse adapter automatiquement le nombre d'instances en fonction de la charge.

Chemin :

**Web App → Mise à l'échelle**

Dans la section **Mise à l'échelle**, sélectionner :

**Basé sur des règles**

Configuration principale :

Nombre minimal d'instances : 1
Nombre maximal d'instances : 3
Nombre d'instances par défaut : 1

Ajouter une règle de scale-out :

Métrique : Pourcentage du processeur
Condition : Supérieur à 70 %
Durée : 10 minutes
Action : Augmenter le nombre d'instances de 1

Ajouter une règle de scale-in :

Métrique : Pourcentage du processeur
Condition : Inférieur à 20 %
Durée : 10 minutes
Action : Diminuer le nombre d'instances de 1

Enregistrer les modifications.

<img width="1141" height="983" alt="image" src="https://github.com/user-attachments/assets/49b06315-428b-4f46-9064-aadfece84cd9" />
<img width="1139" height="982" alt="image" src="https://github.com/user-attachments/assets/e2acf216-669c-470b-a353-cc183dcc8174" />

## 10. Test de charge de la Web App

Création d'un test de charge permettant de générer des requêtes vers l'application.

Chemin :

**Web App → Diagnostiquer et résoudre les problèmes → Tester la charge de votre application → Créer un test de charge**

Sélectionner **+ Créer** puis donner un nom unique au test.

Sélectionner **Vérifier + créer**, puis **Créer**.

Attendre la création du test puis sélectionner **Accéder à la ressource**.

Depuis la page **Vue d'ensemble**, dans **Créer en ajoutant des requêtes HTTP**, sélectionner **Créer**.

Dans l'onglet **Plan de test**, sélectionner **Ajouter une requête**.

Dans le champ **URL**, saisir le **Domaine par défaut** de la Web App.

L'URL doit commencer par :

`https://`

Sélectionner **Ajouter** pour enregistrer la requête.

Sélectionner **Vérifier + créer**, puis **Créer**.

Une fois le test créé, l'ouvrir puis lancer le test.

Actualiser les données et vérifier notamment :

Utilisateurs virtuels
Temps de réponse
Requêtes par seconde

<img width="1142" height="1013" alt="image" src="https://github.com/user-attachments/assets/73507c56-6971-4862-95ab-84cb99a806d8" />

<img width="1141" height="997" alt="image" src="https://github.com/user-attachments/assets/a65ea870-d774-4c09-b594-fc74a80cc30d" />

Une fois les métriques observées, sélectionner **Arrêter**, puis confirmer avec **Arrêter**.

---

# Partie 2 — Azure Container Instances

## 11. Création d'une Azure Container Instance

Déploiement d'une application Web conteneurisée à partir d'une image Docker.

Chemin :

**Portail Azure → Instances de conteneurs → Créer**

Configuration principale :

Groupe de ressources : AZ-104-LAB8
Nom du conteneur : az104-c1
Région : région Azure disponible
Source de l'image : Images de démarrage rapide
Image : mcr.microsoft.com/azuredocs/aci-helloworld:latest
Système d'exploitation : Linux

<img width="922" height="974" alt="image" src="https://github.com/user-attachments/assets/e9afa631-627e-4862-81e9-bd81c11fdb3a" />

Dans **Mise en réseau**, configurer une **étiquette de nom DNS** unique afin de rendre l'application accessible depuis Internet.

Valider puis créer l'instance.

## 12. Vérification et test de l'Azure Container Instance

Attendre la fin du déploiement puis ouvrir la ressource.

Chemin :

**Instance de conteneur → az104-c1 → Vue d'ensemble**

Vérifier que l'état de l'instance est :

**Running**

Récupérer ensuite le **FQDN** et l'ouvrir dans un navigateur.

Vérifier que la page :

**Welcome to Azure Container Instance**

est affichée.

<img width="1919" height="772" alt="image" src="https://github.com/user-attachments/assets/2a4eb60e-6493-4116-92a5-d56b7e5da893" />

## 13. Vérification des journaux

Actualiser plusieurs fois la page Web afin de générer des requêtes HTTP.

Puis consulter :

**Instance de conteneur → Conteneurs → Journaux**

Vérifier la présence des requêtes générées.

<img width="1136" height="798" alt="image" src="https://github.com/user-attachments/assets/edc6f10c-18a0-4c2b-a49f-c36563064fa3" />

---

# Partie 3 — Azure Container Apps

## 14. Création et configuration d'une Azure Container App

Déploiement d'une application conteneurisée avec Azure Container Apps afin d'utiliser une solution PaaS sans gérer directement l'infrastructure sous-jacente.

Chemin :

**Portail Azure → Container Apps → Créer → Container App**

Configuration principale :

Groupe de ressources : AZ-104-LAB8
Nom de l'application : my-app
Région : région Azure disponible

Créer également un environnement Container Apps.

Nom de l'environnement :

my-environment

Configurer l'image de démonstration fournie par Azure.

Chemin :

**Container App → Conteneur**

Activer :

Utiliser une image de démarrage rapide

Sélectionner :

Simple hello world container

Vérifier les paramètres d'accès à l'application puis poursuivre la création.

Vérifier la configuration puis lancer le déploiement.

Chemin :

**Container App → Vérifier + créer → Créer**

Attendre la fin du déploiement.

<img width="773" height="985" alt="image" src="https://github.com/user-attachments/assets/1c696d58-3585-42f8-b0ff-2a91d2b54a20" />

## 15. Vérification de l'Azure Container App

Une fois le déploiement terminé, ouvrir la ressource.

Chemin :

**Container Apps → my-app → Vue d'ensemble**

Récupérer l'URL de l'application.

<img width="1129" height="316" alt="image" src="https://github.com/user-attachments/assets/6b5f72cd-5265-4733-9dfe-430a36564b49" />

## 16. Test de l'application

Ouvrir l'Application URL dans un navigateur.

Vérifier que la page de démonstration confirme que la Container App fonctionne.

<img width="819" height="619" alt="image" src="https://github.com/user-attachments/assets/86244dc5-5638-441b-91f8-4dee208c3547" />

## Résultat

Plusieurs solutions Azure permettant d'héberger des applications Web et conteneurisées ont été mises en œuvre.

Une Azure Web App a été créée et configurée avec un environnement Staging, un déploiement depuis GitHub et une mise à l'échelle automatique.

Une Azure Container Instance a ensuite été déployée à partir d'une image Docker avec un accès public via DNS.

Enfin, une Azure Container App a été créée avec son environnement dédié et une image de démonstration.

Ces trois approches permettent de comparer différents modèles PaaS pour l'hébergement d'applications.

## Ce que j'ai appris

Ce lab m'a permis de comprendre les différentes possibilités offertes par Azure pour héberger des applications sans avoir à gérer directement l'ensemble de l'infrastructure.

J'ai notamment appris à utiliser Azure App Service pour héberger une application Web, les Deployment Slots pour séparer les environnements et l'autoscaling pour adapter automatiquement les ressources.

J'ai également découvert la différence entre Azure Container Instances et Azure Container Apps pour exécuter des applications conteneurisées.

## Approche professionnelle

Dans un environnement d'entreprise, le choix du service d'hébergement dépend du niveau de contrôle souhaité, du type d'application et des besoins en matière de disponibilité et de mise à l'échelle.

Azure App Service permet notamment d'héberger rapidement des applications Web avec des mécanismes de déploiement et de scaling intégrés.

Azure Container Instances convient davantage à l'exécution simple et rapide de conteneurs sans gestion de serveurs.

Azure Container Apps permet quant à lui d'héberger des applications conteneurisées et des architectures modernes tout en réduisant la gestion de l'infrastructure.

La comparaison de ces solutions permet ainsi de choisir une architecture adaptée aux contraintes techniques et opérationnelles d'une entreprise.

## Source

Lab basé sur le parcours pratique Microsoft Learning — AZ-104 Microsoft Azure Administrator.

Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
