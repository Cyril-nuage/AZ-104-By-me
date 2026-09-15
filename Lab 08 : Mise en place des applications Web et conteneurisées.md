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

Portail Azure → App Services → Créer → Application Web

Configuration principale :

Groupe de ressources : AZ-104-LAB8
Nom : nom unique au niveau mondial
Publication : Code
Pile d'exécution : PHP 8.2
Système d'exploitation : Linux
Région : région Azure disponible
Plan tarifaire : Premium V3 P1V3

Valider la configuration puis créer la Web App.

📷 Capture d'écran : configuration principale de l'Azure Web App avant sa création.

## 2. Vérification de la Web App

Une fois le déploiement terminé, ouvrir la ressource créée.

Chemin :

Portail Azure → App Services → Nom de la Web App → Vue d'ensemble

Ouvrir le lien du domaine par défaut afin de vérifier que l'application est accessible.

📷 Capture d'écran : page Vue d'ensemble de la Web App avec le domaine par défaut.

📷 Capture d'écran : page Web affichée après l'ouverture du domaine par défaut.

## 3. Création du slot Staging

Création d'un environnement de préproduction permettant de tester une nouvelle version de l'application avant son passage en production.

Chemin :

Web App → Déploiement → Emplacements de déploiement → Ajouter

Configuration :

Nom : staging
Cloner les paramètres : Ne pas cloner

Créer le slot puis ouvrir celui-ci.

📷 Capture d'écran : liste des emplacements avec Production et Staging.

## 4. Vérification du slot Staging

Vérification de la présence du nouvel environnement et de son domaine spécifique.

Chemin :

Web App → Déploiement → Emplacements de déploiement → staging

Le slot Staging possède une URL différente de celle de la production.

📷 Capture d'écran : Vue d'ensemble du slot staging avec son domaine.

## 5. Configuration du déploiement depuis GitHub

Activation des paramètres nécessaires afin de permettre le déploiement de l'application depuis un dépôt GitHub externe.

Chemin :

Slot staging → Configuration → Paramètres généraux

Activer l'authentification de base SCM si elle est désactivée puis appliquer les modifications.

Ensuite :

Slot staging → Centre de déploiement → Paramètres

Configurer :

Source : External Git
Dépôt : https://github.com/Azure-Samples/php-docs-hello-world
Branche : master

Enregistrer la configuration.

📷 Capture d'écran : configuration du Centre de déploiement avec le dépôt GitHub.

## 6. Vérification du déploiement Staging

Attendre la fin du déploiement puis ouvrir le domaine du slot staging.

Chemin :

Slot staging → Vue d'ensemble → Domaine par défaut

Vérifier que la page Hello World est affichée.

📷 Capture d'écran : application Hello World affichée sur le slot staging.

## 7. Passage de Staging vers Production

Une fois l'application validée dans l'environnement Staging, effectuer l'échange entre les deux environnements.

Chemin :

Web App → Déploiement → Emplacements de déploiement → Swap

Vérifier les paramètres puis sélectionner Start Swap.

Attendre la fin de l'opération.

📷 Capture d'écran : fenêtre de configuration du Swap avant son lancement.

## 8. Vérification de la Production

Ouvrir la Web App en production et vérifier que l'application précédemment testée dans Staging est maintenant disponible en Production.

Chemin :

App Services → Web App → Vue d'ensemble → Domaine par défaut

📷 Capture d'écran : application Hello World accessible depuis le domaine de production.

## 9. Configuration de la mise à l'échelle automatique

Configuration de l'autoscaling afin que la Web App puisse adapter automatiquement ses ressources en fonction de la charge.

Chemin :

Web App → Mise à l'échelle

Sélectionner le mode :

Automatic

Configuration principale :

Nombre minimal d'instances : 1
Maximum burst : 2

Enregistrer les modifications.

📷 Capture d'écran : configuration de la mise à l'échelle automatique.

## 10. Test de charge de la Web App

Création d'un test de charge permettant de générer des requêtes vers l'application.

Chemin :

Web App → Diagnostiquer et résoudre les problèmes → Tester la charge de votre application → Créer un test de charge

Créer le test puis ajouter une requête HTTP.

Utiliser l'URL du domaine de production de la Web App.

Vérifier notamment :

Utilisateurs virtuels
Temps de réponse
Requêtes par seconde

📷 Capture d'écran : configuration de la requête HTTP du test de charge.

📷 Capture d'écran : métriques du test de charge en cours.

---

# Partie 2 — Azure Container Instances

## 11. Création d'une Azure Container Instance

Déploiement d'une application Web conteneurisée à partir d'une image Docker.

Chemin :

Portail Azure → Instances de conteneurs → Créer

Configuration principale :

Groupe de ressources : AZ-104-LAB8
Nom du conteneur : az104-c1
Région : région Azure disponible
Source de l'image : Images de démarrage rapide
Image : mcr.microsoft.com/azuredocs/aci-helloworld:latest
Système d'exploitation : Linux

📷 Capture d'écran : configuration principale de l'Azure Container Instance.

## 12. Configuration de l'accès réseau

Configurer un nom DNS public permettant d'accéder directement au conteneur depuis Internet.

Chemin :

Créer une instance de conteneur → Mise en réseau

Configuration :

Étiquette de nom DNS : nom unique

L'application sera accessible via un nom DNS Azure associé à la région sélectionnée.

📷 Capture d'écran : configuration du nom DNS de l'instance.

Valider puis créer l'instance.

## 13. Vérification de l'Azure Container Instance

Attendre la fin du déploiement puis ouvrir la ressource.

Chemin :

Instance de conteneur → az104-c1 → Vue d'ensemble

Vérifier que l'état de l'instance est :

Running

📷 Capture d'écran : Vue d'ensemble de l'instance avec l'état Running.

## 14. Test de l'application conteneurisée

Récupérer le nom de domaine complet de l'instance puis l'ouvrir dans un navigateur.

Chemin :

Instance de conteneur → Vue d'ensemble → FQDN

Ouvrir l'adresse dans un nouvel onglet.

Vérifier que la page :

Welcome to Azure Container Instance

est affichée.

📷 Capture d'écran : page Web de l'Azure Container Instance.

## 15. Vérification des journaux

Effectuer plusieurs actualisations de la page afin de générer des requêtes HTTP.

Puis consulter les journaux du conteneur.

Chemin :

Instance de conteneur → Conteneurs → Journaux

Vérifier la présence des requêtes HTTP générées lors de l'accès à l'application.

📷 Capture d'écran : journaux du conteneur contenant les requêtes HTTP.

---

# Partie 3 — Azure Container Apps

## 16. Création d'une Azure Container App

Déploiement d'une application conteneurisée avec Azure Container Apps afin d'utiliser une solution PaaS sans gérer directement l'infrastructure sous-jacente.

Chemin :

Portail Azure → Container Apps → Créer → Container App

Configuration principale :

Groupe de ressources : AZ-104-LAB8
Nom de l'application : my-app
Région : région Azure disponible

Créer également un environnement Container Apps.

Nom de l'environnement :

my-environment

📷 Capture d'écran : configuration principale de la Container App.

## 17. Configuration de l'image du conteneur

Configurer l'image de démonstration fournie par Azure.

Chemin :

Container App → Conteneur

Activer :

Utiliser une image de démarrage rapide

Sélectionner :

Simple hello world container

Vérifier les paramètres d'accès à l'application puis poursuivre la création.

📷 Capture d'écran : configuration du conteneur avec l'image Simple hello world container.

## 18. Création et déploiement de la Container App

Vérifier la configuration puis lancer le déploiement.

Chemin :

Container App → Vérifier + créer → Créer

Attendre la fin du déploiement.

📷 Capture d'écran : validation finale de la Container App avant création.

## 19. Vérification de l'Azure Container App

Une fois le déploiement terminé, ouvrir la ressource.

Chemin :

Container Apps → my-app → Vue d'ensemble

Récupérer l'URL de l'application.

📷 Capture d'écran : Vue d'ensemble de la Container App avec l'Application URL.

## 20. Test de l'application

Ouvrir l'Application URL dans un navigateur.

Vérifier que la page de démonstration confirme que la Container App fonctionne.

📷 Capture d'écran : page Hello World de l'Azure Container App.

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
