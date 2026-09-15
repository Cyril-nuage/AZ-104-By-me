# Lab 07 — Gestion du trafic et mise à l’échelle des machines virtuelles

AZ-104 — Microsoft Azure Administrator

## Objectif

Mettre en pratique la gestion du trafic réseau et la mise à l'échelle des ressources Azure à travers la création de machines virtuelles, l'utilisation de disques managés, la configuration d'un Load Balancer, d'une Application Gateway, d'un Traffic Manager et d'un Virtual Machine Scale Set.

## Compétences mises en pratique

Création et gestion de machines virtuelles Azure
Gestion des disques managés
Configuration d'un Azure Load Balancer
Configuration d'une Application Gateway
Gestion du trafic avec Azure Traffic Manager
Création et gestion d'un Virtual Machine Scale Set
Mise à l'échelle automatique des machines virtuelles
Vérification de la disponibilité des ressources

## Réalisation

### 1. Création des ressources réseau

Création du réseau virtuel et des sous-réseaux nécessaires à l'hébergement des ressources du laboratoire.

Chemin :

**Portail Azure → Réseaux virtuels → Créer**

Configuration principale :

Réseau virtuel : AZ-104-VNet
Sous-réseau VM : Subnet-VMSS
Sous-réseau Application Gateway : Subnet-AppGateway
Groupe de ressources : AZ-104-LAB7

Le réseau permet de séparer les ressources et de préparer l'intégration entre les machines virtuelles et les services de gestion du trafic.

### 2. Création d'une machine virtuelle

Création d'une machine virtuelle Azure afin de mettre en pratique la gestion des ressources de calcul et des disques managés.

Chemin :

**Portail Azure → Machines virtuelles → Créer → Machine virtuelle Azure**

Configuration principale :

Groupe de ressources : AZ-104-LAB7
Nom : AZ-104-VM01
Image : Windows Server
Taille : selon les ressources disponibles
Disque du système d'exploitation : disque managé

La machine virtuelle sert de base pour comprendre la configuration des instances qui pourront ensuite être reproduites avec un groupe identique.

### 3. Gestion des disques managés

Vérification du disque du système d'exploitation et gestion des disques associés à la machine virtuelle.

Chemin :

**Portail Azure → Machines virtuelles → AZ-104-VM01 → Disques**

Les disques managés permettent de stocker les données des machines virtuelles sans avoir à gérer directement le stockage physique sous-jacent.

### 4. Création du Virtual Machine Scale Set

Création d'un groupe identique de machines virtuelles afin de disposer de plusieurs instances pouvant être gérées de manière centralisée.

Chemin :

**Portail Azure → Groupes identiques de machines virtuelles → Créer**

Configuration principale :

Nom : AZ-104-VMSS
Groupe de ressources : AZ-104-LAB7
Nombre initial d'instances : 2
Réseau virtuel : AZ-104-VNet
Sous-réseau : Subnet-VMSS

Le Virtual Machine Scale Set permet de gérer plusieurs instances identiques et de faire évoluer automatiquement leur nombre en fonction de la charge.

### 5. Configuration du Load Balancer

Création d'un Azure Load Balancer afin de répartir le trafic entrant entre les différentes instances du Virtual Machine Scale Set.

Chemin :

**Portail Azure → Équilibreurs de charge → Créer**

Configuration principale :

Nom : AZ-104-LB
Type : Public
SKU : Standard
Adresse IP publique : nouvelle adresse IP

Une règle d'équilibrage et une sonde d'intégrité sont configurées afin de vérifier la disponibilité des instances et de distribuer le trafic vers les ressources disponibles.

### 6. Création de l'Application Gateway

Création d'une Application Gateway afin de gérer et distribuer le trafic HTTP vers les ressources hébergeant l'application.

Chemin :

**Portail Azure → Application Gateway → Créer**

Configuration principale :

Nom : AZ-104-AppGateway
Groupe de ressources : AZ-104-LAB7
Réseau virtuel : AZ-104-VNet
Sous-réseau : Subnet-AppGateway
Adresse IP frontale : publique
Pool principal : AZ-104-VMSS

Une règle de routage HTTP est configurée afin de transmettre les requêtes vers les instances du groupe identique.

### 7. Configuration d'Azure Traffic Manager

Création d'un profil Traffic Manager afin de mettre en place une gestion du trafic basée sur DNS.

Chemin :

**Portail Azure → Traffic Manager → Créer un profil**

Configuration principale :

Nom : AZ-104-TrafficManager
Méthode de routage : selon le scénario
Point de terminaison : ressource exposant l'application

Traffic Manager permet de diriger les utilisateurs vers différents points de terminaison en fonction de la méthode de routage configurée et de leur disponibilité.

### 8. Mise en place de la mise à l'échelle automatique

Configuration de l'autoscaling du Virtual Machine Scale Set afin d'adapter automatiquement le nombre d'instances en fonction de la charge.

Chemin :

**Portail Azure → Groupes identiques de machines virtuelles → AZ-104-VMSS → Mise à l'échelle**

Configuration principale :

Nombre minimal d'instances : 2
Nombre maximal d'instances : 4
Instances par défaut : 2
Critère : utilisation du processeur

Le nombre d'instances peut ainsi augmenter lorsque la charge devient importante et diminuer lorsque celle-ci revient à un niveau normal.

### 9. Vérification de l'environnement

Vérification de l'état des machines virtuelles, du Virtual Machine Scale Set et des différents services de gestion du trafic.

Chemin :

**Portail Azure → Groupes identiques de machines virtuelles → AZ-104-VMSS → Instances**

Puis :

**Portail Azure → Application Gateway → AZ-104-AppGateway → Pools principaux**

Puis :

**Portail Azure → Traffic Manager → AZ-104-TrafficManager → Points de terminaison**

Les instances, les sondes d'intégrité et les points de terminaison sont vérifiés afin de confirmer le bon fonctionnement de l'architecture.

## Résultat

Une architecture Azure combinant calcul, stockage et gestion du trafic a été mise en place.

Le Virtual Machine Scale Set permet de gérer plusieurs instances de machines virtuelles tandis que les disques managés assurent leur stockage.

Le Load Balancer, l'Application Gateway et Traffic Manager permettent de mettre en œuvre différents mécanismes de distribution et de gestion du trafic.

L'autoscaling permet enfin d'adapter automatiquement le nombre d'instances disponibles en fonction de la charge.

## Ce que j'ai appris

Ce lab m'a permis de comprendre comment combiner plusieurs services Azure afin de construire une architecture capable de gérer la charge et de maintenir la disponibilité d'une application.

J'ai également approfondi la gestion des machines virtuelles, des disques managés et des groupes identiques de machines virtuelles.

La mise en pratique du Load Balancer, de l'Application Gateway et de Traffic Manager m'a permis de mieux comprendre les différents niveaux de gestion du trafic dans Azure.

## Approche professionnelle

Dans un environnement d'entreprise, la mise à l'échelle et la répartition du trafic permettent d'améliorer la disponibilité, la continuité de service et la capacité d'une infrastructure à absorber des variations de charge.

L'utilisation d'un Virtual Machine Scale Set permet notamment de standardiser la gestion de plusieurs machines virtuelles et de limiter les interventions manuelles lors des variations de capacité nécessaires.

Les solutions de Load Balancing et de gestion du trafic permettent également de construire des architectures plus résilientes et adaptées aux besoins des applications.

## Source

Lab basé sur le parcours pratique Microsoft Learning — AZ-104 Microsoft Azure Administrator.

Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
