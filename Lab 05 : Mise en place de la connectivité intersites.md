Lab 05 — Mise en place de la connectivité intersites

AZ-104 — Microsoft Azure Administrator

## Objectif

Mettre en place et tester la connectivité entre plusieurs réseaux virtuels Azure.

L'objectif est de créer plusieurs réseaux virtuels, de mettre en place une connexion entre eux à l'aide du VNet Peering, puis de configurer une table de routage afin de contrôler le chemin emprunté par le trafic réseau.

## Compétences mises en pratique

- Création de machines virtuelles Azure
- Création et configuration de réseaux virtuels
- Création de sous-réseaux
- Configuration du VNet Peering
- Test de la connectivité réseau
- Utilisation de Network Watcher
- Création d'une table de routage
- Configuration d'une User Defined Route (UDR)
- Analyse du routage Azure
- Vérification de la connectivité entre réseaux

## Realisation

1. Création de la machine virtuelle CoreServicesVM

Création d'une première machine virtuelle permettant de représenter les ressources du réseau principal.

La machine virtuelle est déployée dans un réseau virtuel nommé CoreServicesVnet.

Chemin :

Portail Azure → Machines virtuelles → Créer → Machine virtuelle Azure

Configuration principale :

Nom : CoreServicesVM
Réseau virtuel : CoreServicesVnet
Plage d'adresses : 10.0.0.0/16
Sous-réseau : Core
Plage du sous-réseau : 10.0.0.0/24

<img width="2026" height="1969" alt="image" src="https://github.com/user-attachments/assets/cc752a2d-6051-44d5-b3eb-68360943067e" />

<img width="1001" height="1015" alt="image" src="https://github.com/user-attachments/assets/a47d880b-f0ff-4851-ba52-1525f6b5bf5d" />

2. Création de la machine virtuelle ManufacturingVM

Création d'une deuxième machine virtuelle dans un réseau virtuel différent.

Cette séparation permet ensuite de mettre en place une communication entre deux réseaux Azure distincts.

Le réseau virtuel utilisé est ManufacturingVnet.

<img width="939" height="983" alt="image" src="https://github.com/user-attachments/assets/691098f3-5f79-4788-bea2-2c838e1f65a9" />

<img width="1924" height="1969" alt="image" src="https://github.com/user-attachments/assets/6e3145a2-ff2b-4e6c-8ed2-e5d1bbff7e71" />

3. Configuration du VNet Peering

Mise en place d'un VNet Peering entre CoreServicesVnet et ManufacturingVnet.

Le VNet Peering permet de connecter directement deux réseaux virtuels Azure afin que leurs ressources puissent communiquer entre elles.

Chemin :

Portail Azure → Réseaux virtuels → CoreServicesVnet → Peerings → Ajouter

Configuration du peering entre les deux réseaux.

<img width="944" height="985" alt="image" src="https://github.com/user-attachments/assets/b43fc69b-99b0-4544-9885-46e79de607e0" />

4. Vérification de la connectivité après le peering

Une nouvelle vérification est effectuée afin de confirmer que les machines virtuelles peuvent maintenant communiquer à travers les réseaux virtuels interconnectés.

Le test Test-NetConnection permet de vérifier la communication entre les adresses IP privées des machines virtuelles.

<img width="1096" height="952" alt="image" src="https://github.com/user-attachments/assets/8c3f3908-8cb7-4156-a9ca-4c776b560818" />

5. Utilisation de Network Watcher

Utilisation de Network Watcher afin d'analyser et de diagnostiquer la connectivité réseau Azure.

Network Watcher permet notamment de vérifier le chemin réseau utilisé par le trafic et d'identifier d'éventuels problèmes de communication.

Chemin :

Portail Azure → Network Watcher → Résolution des problèmes de connexion

<img width="875" height="923" alt="image" src="https://github.com/user-attachments/assets/d3c36a2d-200f-48c2-9d05-d88002710a39" />

6. Création d'une table de routage

Création d'une Route Table afin de définir un routage personnalisé pour le trafic réseau.

Une table de routage permet d'ajouter des routes personnalisées afin de contrôler la manière dont Azure achemine le trafic.

Chemin :

Portail Azure → Tables de routage → Créer

<img width="915" height="983" alt="image" src="https://github.com/user-attachments/assets/90ac2ed0-42d1-4850-8913-14fda7b0d99f" />

7. Création d'une User Defined Route

Création d'une route personnalisée (User Defined Route / UDR) permettant de définir le prochain saut du trafic réseau.

Cette configuration permet de mieux comprendre le fonctionnement du routage personnalisé dans Azure et le rôle d'une appliance réseau dans le chemin de communication.

<img width="1160" height="936" alt="image" src="https://github.com/user-attachments/assets/1c334ad6-c78b-4440-9f17-16cf3504aae1" />

8. Association de la table de routage au sous-réseau

Association de la Route Table au sous-réseau concerné.

Cette association permet d'appliquer les routes personnalisées aux ressources présentes dans le sous-réseau.

Chemin :

Réseau virtuel → Sous-réseaux → Sous-réseau concerné → Table de routage

<img width="1135" height="934" alt="image" src="https://github.com/user-attachments/assets/6799a692-96f7-4f1f-8489-ef7ad41050a4" />

## Comparaison des éléments
- Élément	Utilisation
- Virtual Network	Créer un réseau virtuel Azure
- Subnet	Diviser le réseau virtuel
- VNet Peering	Connecter deux réseaux virtuels
- Network Watcher	Diagnostiquer et analyser le réseau
- Route Table	Définir des routes personnalisées
- UDR	Contrôler le chemin du trafic
- Résultat

Ce lab m'a permis de mettre en pratique plusieurs éléments de la connectivité réseau Azure :

- création de réseaux virtuels ;
- création de sous-réseaux ;
- déploiement de machines virtuelles ;
- mise en place du VNet Peering ;
- test de la connectivité réseau ;
- utilisation de Network Watcher ;
- création de tables de routage ;
- configuration de routes personnalisées.

## Ce que j'ai appris

J'ai compris comment Azure permet de connecter plusieurs réseaux virtuels grâce au VNet Peering.

J'ai également compris qu'un réseau virtuel Azure est isolé par défaut et que la mise en place d'une connexion entre réseaux permet aux ressources de communiquer entre elles.

J'ai découvert le fonctionnement des Route Tables et des User Defined Routes, qui permettent de contrôler plus précisément le chemin emprunté par le trafic réseau.

Enfin, Network Watcher permet de diagnostiquer la connectivité et de mieux comprendre le routage utilisé par Azure.

## Approche professionnelle

Dans un environnement professionnel, la segmentation des réseaux permet d'organiser et de sécuriser l'infrastructure Azure.

Le VNet Peering peut être utilisé pour permettre la communication entre différents réseaux virtuels tout en conservant une séparation logique des environnements.

Les Route Tables et les UDR permettent quant à elles de contrôler précisément le chemin du trafic, notamment lorsqu'une infrastructure utilise des appliances réseau ou des équipements de sécurité.

Les outils de diagnostic comme Network Watcher facilitent enfin l'analyse des problèmes de connectivité et permettent aux administrateurs de vérifier le fonctionnement du réseau.

## Source

Lab basé sur les exercices pratiques Microsoft Learning — AZ-104 Microsoft Azure Administrator.

Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
