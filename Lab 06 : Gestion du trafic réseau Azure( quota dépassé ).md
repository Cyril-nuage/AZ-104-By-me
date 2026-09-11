# Lab 06 — Gestion du trafic réseau Azure

AZ-104 — Microsoft Azure Administrator

## Objectif

Mettre en place et tester la gestion du trafic réseau avec Azure.

L'objectif est de déployer plusieurs machines virtuelles, puis de configurer un Azure Load Balancer et une Azure Application Gateway afin de répartir et d'orienter le trafic réseau vers différentes ressources.

## Compétences mises en pratique

* Déploiement de machines virtuelles Azure
* Création et configuration d'un Azure Load Balancer
* Configuration d'un pool principal
* Création d'une sonde d'intégrité
* Configuration d'une règle d'équilibrage de charge
* Test de la répartition du trafic
* Création et configuration d'une Application Gateway
* Configuration du routage HTTP
* Configuration du routage basé sur le chemin URL
* Vérification de l'état des serveurs principaux
* Analyse de la gestion du trafic réseau Azure

## Realisation

1. Déploiement de l'infrastructure

Déploiement de l'infrastructure nécessaire au lab à l'aide d'un modèle ARM.

L'infrastructure comprend un réseau virtuel, plusieurs machines virtuelles et les ressources réseau nécessaires à la mise en place du Load Balancer et de l'Application Gateway.

Le groupe de ressources utilisé pour ce lab est :

Nom : AZ-104-LAB06

☀️ Chemin :

Portail Azure → Groupes de ressources → AZ-104-LAB06

📸 Capture à mettre :

* Vue d'ensemble du groupe de ressources AZ-104-LAB06
* Liste des ressources déployées dans le groupe de ressources
* Machines virtuelles présentes dans l'infrastructure

2. Création de l'Azure Load Balancer

Création d'un Azure Load Balancer afin de répartir le trafic entrant entre plusieurs machines virtuelles.

Le Load Balancer permet d'améliorer la disponibilité d'un service en distribuant les connexions entre plusieurs serveurs.

☀️ Chemin :

Portail Azure → Équilibreurs de charge → Créer

Configuration principale :

Nom : AZ-104-LB06
Référence SKU : Standard
Type : Public
Région : même région que les machines virtuelles

Une adresse IP publique est également associée au Load Balancer afin de permettre l'accès au service depuis Internet.

📸 Capture à mettre :

* Configuration générale du Load Balancer
* Nom AZ-104-LB06
* SKU Standard
* Type Public
* Région sélectionnée
* Adresse IP publique du serveur frontal

3. Configuration du pool principal

Création d'un pool principal contenant les machines virtuelles qui recevront le trafic.

Le pool principal permet au Load Balancer de savoir vers quelles ressources le trafic doit être distribué.

☀️ Chemin :

Portail Azure → Équilibreurs de charge → AZ-104-LB06 → Pools principaux → Ajouter

Configuration :

Nom : AZ-104-BE06

Ajout des interfaces réseau des machines virtuelles utilisées pour le test.

📸 Capture à mettre :

* Pool principal AZ-104-BE06
* Machines virtuelles ou interfaces réseau ajoutées au pool

4. Configuration de la sonde et de la règle d'équilibrage

Création d'une sonde d'intégrité afin de vérifier automatiquement la disponibilité des serveurs.

Configuration de la sonde :

Nom : AZ-104-HP06
Protocole : TCP
Port : 80
Intervalle : 5 secondes

Création ensuite d'une règle d'équilibrage permettant de distribuer le trafic HTTP vers les machines virtuelles disponibles.

Configuration de la règle :

Nom : AZ-104-LB-RULE06
Protocole : TCP
Port frontal : 80
Port principal : 80
Sonde d'intégrité : AZ-104-HP06
Pool principal : AZ-104-BE06

☀️ Chemin :

Portail Azure → Équilibreurs de charge → AZ-104-LB06 → Sondes d'intégrité

Puis :

Portail Azure → Équilibreurs de charge → AZ-104-LB06 → Règles d'équilibrage de charge

📸 Capture à mettre :

* Configuration de la sonde d'intégrité
* Protocole TCP
* Port 80
* Configuration de la règle d'équilibrage
* Pool principal
* Sonde associée
* Ports 80

5. Vérification du Load Balancer

Test de l'accès au service à partir de l'adresse IP publique du Load Balancer.

Le résultat doit afficher la réponse d'un des serveurs backend.

En actualisant la page plusieurs fois, le serveur répondant peut changer en fonction de la répartition du trafic.

Cette vérification permet de confirmer que le Load Balancer distribue correctement les requêtes entre les machines virtuelles.

☀️ Chemin :

Portail Azure → Équilibreurs de charge → AZ-104-LB06 → Vue d'ensemble

📸 Capture à mettre :

* Adresse IP publique du Load Balancer
* Page web affichant la réponse d'une machine virtuelle
* Si possible, une deuxième capture montrant la réponse d'une autre machine virtuelle

6. Création de l'Application Gateway

Création d'une Azure Application Gateway afin de mettre en place un routage du trafic HTTP basé sur les chemins URL.

Contrairement au Load Balancer, l'Application Gateway permet d'effectuer un routage applicatif de niveau 7.

Un sous-réseau dédié est utilisé pour héberger l'Application Gateway.

☀️ Chemin :

Portail Azure → Application Gateway → Créer

Configuration principale :

Nom : AZ-104-APPGW06
Niveau : Standard V2
Réseau virtuel : réseau virtuel du lab
Sous-réseau : subnet-appgw
Adresse IP publique : nouvelle adresse IP publique

Sous-réseau :

Nom : subnet-appgw
Plage d'adresses : 10.60.3.224/27

📸 Capture à mettre :

* Configuration de création de l'Application Gateway
* Nom AZ-104-APPGW06
* Niveau Standard V2
* Réseau virtuel
* Sous-réseau subnet-appgw
* Plage d'adresses du sous-réseau

7. Configuration du pool principal et de l'écouteur HTTP

Configuration des ressources nécessaires pour recevoir les requêtes HTTP et les transmettre aux serveurs backend.

Création d'un pool principal contenant les interfaces réseau des machines virtuelles.

Pool principal :

Nom : AZ-104-APPGWBE06

Création également d'un écouteur HTTP permettant à l'Application Gateway de recevoir les requêtes sur le port 80.

Écouteur :

Nom : AZ-104-LISTENER06
Protocole : HTTP
Port : 80

Des paramètres principaux sont également configurés afin de définir la communication entre l'Application Gateway et les serveurs backend.

Paramètres :

Nom : AZ-104-HTTP06
Protocole : HTTP
Port : 80

☀️ Chemin :

Portail Azure → Application Gateway → AZ-104-APPGW06 → Pools principaux

Puis :

Portail Azure → Application Gateway → AZ-104-APPGW06 → Écouteurs

Puis :

Portail Azure → Application Gateway → AZ-104-APPGW06 → Paramètres principaux

📸 Capture à mettre :

* Pool principal AZ-104-APPGWBE06
* Interfaces réseau ajoutées
* Écouteur HTTP
* Port 80
* Paramètres principaux AZ-104-HTTP06

8. Configuration du routage basé sur le chemin

Création d'une règle de routage permettant d'orienter les requêtes vers différents serveurs en fonction du chemin utilisé dans l'URL.

La règle principale associe l'écouteur HTTP au pool principal et aux paramètres de communication.

Configuration :

Nom : AZ-104-GWRULE06
Priorité : 10
Écouteur : AZ-104-LISTENER06
Paramètres principaux : AZ-104-HTTP06

Des règles de chemin sont ensuite configurées :

/image/* → serveur d'images

/video/* → serveur vidéo

Cette fonctionnalité permet de répartir le trafic applicatif en fonction du contenu demandé.

☀️ Chemin :

Portail Azure → Application Gateway → AZ-104-APPGW06 → Règles → Ajouter

Puis :

Règle de routage → Règles de chemin

📸 Capture à mettre :

* Configuration de la règle AZ-104-GWRULE06
* Priorité 10
* Écouteur HTTP
* Paramètres principaux
* Règle `/image/*`
* Règle `/video/*`
* Pools principaux associés aux différents chemins

9. Vérification de l'intégrité et test du routage

Vérification de l'état des serveurs backend afin de confirmer que l'Application Gateway peut communiquer correctement avec eux.

Les serveurs doivent apparaître comme étant en bonne santé.

☀️ Chemin :

Portail Azure → Application Gateway → AZ-104-APPGW06 → Intégrité du backend

📸 Capture à mettre :

* Page « Intégrité du backend »
* Serveurs affichés avec l'état « Sain »

Un test du routage est ensuite effectué à partir de l'adresse IP publique de l'Application Gateway.

L'accès au chemin `/image/` doit être envoyé vers le serveur d'images.

L'accès au chemin `/video/` doit être envoyé vers le serveur vidéo.

📸 Capture à mettre :

* Navigateur avec l'URL `http://<adresse-ip>/image/`
* Résultat affichant le serveur d'images
* Navigateur avec l'URL `http://<adresse-ip>/video/`
* Résultat affichant le serveur vidéo

## Comparaison des éléments

* Élément | Utilisation
* Virtual Network | Fournir le réseau Azure aux ressources
* Virtual Machine | Héberger les serveurs utilisés pour les tests
* Load Balancer | Répartir le trafic réseau entre plusieurs serveurs
* Pool principal | Définir les ressources recevant le trafic
* Sonde d'intégrité | Vérifier la disponibilité des serveurs
* Règle d'équilibrage | Définir comment le trafic est distribué
* Application Gateway | Gérer le trafic applicatif HTTP
* Écouteur | Recevoir les requêtes HTTP
* Paramètres principaux | Définir la communication avec les serveurs
* Routage basé sur le chemin | Orienter les requêtes selon l'URL

## Résultat

Ce lab m'a permis de mettre en pratique plusieurs éléments de la gestion du trafic réseau Azure :

* déploiement de machines virtuelles ;
* création d'un Azure Load Balancer ;
* configuration d'un pool principal ;
* création d'une sonde d'intégrité ;
* configuration d'une règle d'équilibrage ;
* test de la répartition du trafic ;
* création d'une Application Gateway ;
* configuration d'un écouteur HTTP ;
* configuration du routage applicatif ;
* mise en place du routage basé sur les chemins URL ;
* vérification de l'état des serveurs backend.

## Ce que j'ai appris

J'ai compris comment Azure permet de répartir le trafic réseau entre plusieurs machines virtuelles grâce à un Load Balancer.

J'ai également compris l'importance des sondes d'intégrité, qui permettent de vérifier automatiquement la disponibilité des serveurs avant de leur envoyer du trafic.

L'Application Gateway m'a permis de découvrir une approche différente de la gestion du trafic, basée sur le niveau applicatif et notamment sur les chemins présents dans les URL.

Enfin, j'ai compris comment utiliser différentes règles de routage afin d'orienter les requêtes vers les serveurs appropriés.

## Approche professionnelle

Dans un environnement professionnel, les solutions de gestion du trafic permettent d'améliorer la disponibilité, la répartition de charge et l'organisation des applications.

Un Load Balancer peut être utilisé pour répartir les connexions entre plusieurs serveurs afin d'éviter qu'une seule machine ne supporte l'ensemble du trafic.

Une Application Gateway permet quant à elle de gérer le trafic HTTP au niveau applicatif et d'utiliser des règles de routage plus avancées.

La combinaison de ces mécanismes permet de construire une infrastructure Azure plus disponible, mieux organisée et plus facilement évolutive.

## Source

Lab basé sur les exercices pratiques Microsoft Learning — AZ-104 Microsoft Azure Administrator.

Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
