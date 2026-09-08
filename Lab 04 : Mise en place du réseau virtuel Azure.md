Lab 04 — Mise en place du réseau virtuel Azure

AZ-104 — Microsoft Azure Administrator

# Objectif

Mettre en place et sécuriser un réseau virtuel Azure.

L'objectif est de créer des réseaux virtuels, des sous-réseaux et des règles de sécurité, puis de configurer le DNS Azure.

## Compétences mises en pratique
Création d'un réseau virtuel
Création de sous-réseaux
Déploiement avec un modèle ARM
Gestion des NSG
Gestion des ASG
Création de règles réseau
Configuration d'Azure DNS
Vérification de la configuration réseau
## Environnement
Élément	Configuration
Cloud	Microsoft Azure
Interface	Portail Azure
Réseau	Azure Virtual Network
Sécurité	NSG / ASG
DNS	Azure DNS
Environnement	Lab personnel
# Réalisation

**1. Création du réseau virtuel**

Création d'un réseau virtuel Azure afin de mettre en place l'infrastructure réseau du lab.

Chemin :

*Portail Azure → Réseaux virtuels → Créer*

Le réseau virtuel permet de connecter et d'organiser les différentes ressources Azure.

📸 Capture : configuration du réseau virtuel.

**2. Création des sous-réseaux**

Création des sous-réseaux nécessaires dans le réseau virtuel.

Les sous-réseaux permettent de séparer les différentes parties du réseau et d'organiser les ressources.

📸 Capture : liste des sous-réseaux.

**3. Déploiement d'un réseau avec un modèle ARM**

Utilisation d'un modèle ARM afin de déployer un deuxième réseau virtuel.

Le modèle permet de définir la configuration du réseau sous forme de code et de reproduire plus facilement le déploiement.

📸 Capture : modèle ARM et paramètres du déploiement.

📸 Capture : déploiement terminé.

**4. Création des groupes de sécurité**

Création d'un Application Security Group (ASG) et d'un Network Security Group (NSG).

L'ASG permet de regrouper les ressources ayant le même rôle.

Le NSG permet de contrôler le trafic réseau.

📸 Capture : ASG et NSG créés.

**5. Création des règles de sécurité**

Création d'une règle dans le NSG afin d'autoriser ou de bloquer certains types de trafic.

Les règles permettent de contrôler les communications entre les ressources.

📸 Capture : règle de sécurité configurée.

**6. Association du NSG au réseau**

Association du Network Security Group au sous-réseau concerné.

Cette configuration permet d'appliquer les règles de sécurité aux ressources présentes dans le sous-réseau.

📸 Capture : NSG associé au sous-réseau.

**7. Configuration d'Azure DNS**

Création d'une zone DNS publique et d'une zone DNS privée.

Le DNS permet de résoudre des noms de domaine et de faciliter l'accès aux ressources à l'aide de noms plutôt que d'adresses IP.

📸 Capture : zones DNS créées.

**8. Vérification de la configuration réseau**

Vérification de l'ensemble de la configuration créée pendant le lab.

Contrôles effectués :

réseaux virtuels ;
sous-réseaux ;
NSG ;
ASG ;
règles réseau ;
zones DNS.

📸 Capture : vue finale des ressources réseau.

# Comparaison des éléments
Élément	Utilisation
Virtual Network	Créer le réseau Azure
Subnet	Séparer le réseau
NSG	Contrôler le trafic réseau
ASG	Regrouper les ressources par rôle
DNS public	Résoudre des noms accessibles publiquement
DNS privé	Résoudre des noms dans le réseau privé
Résultat

Ce lab m'a permis de mettre en pratique plusieurs éléments de la gestion réseau Azure :

création de réseaux virtuels ;
création de sous-réseaux ;
déploiement avec un modèle ARM ;
sécurisation du réseau avec les NSG et ASG ;
création de règles réseau ;
configuration d'Azure DNS.
Ce que j'ai appris

J'ai compris comment fonctionne la structure réseau de base d'Azure.

Les Virtual Networks permettent de créer un réseau virtuel pour les ressources Azure.

Les subnets permettent de diviser ce réseau.

Les NSG permettent de contrôler les communications réseau tandis que les ASG facilitent l'organisation des règles de sécurité.

J'ai également découvert l'utilisation d'Azure DNS pour gérer la résolution des noms.

# Approche professionnelle

Dans un environnement professionnel, une bonne organisation du réseau permet de mieux sécuriser et administrer les ressources Azure.

Les sous-réseaux permettent de séparer les différentes parties de l'infrastructure et les NSG permettent de limiter les communications autorisées.

L'utilisation des ASG et des modèles ARM permet également de rendre la configuration plus organisée, reproductible et facilement maintenable.

# Source

Lab basé sur les exercices pratiques Microsoft Learning — AZ-104 Microsoft Azure Administrator.

Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
