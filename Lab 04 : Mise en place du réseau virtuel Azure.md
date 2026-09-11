Lab 04 — Mise en place du réseau virtuel Azure

AZ-104 — Microsoft Azure Administrator

# Objectif

Mettre en place et sécuriser un réseau virtuel Azure.

L'objectif est de créer des réseaux virtuels, des sous-réseaux et des règles de sécurité, puis de configurer le DNS Azure.

## Compétences mises en pratique
- Création d'un réseau virtuel
- Création de sous-réseaux
- Déploiement avec un modèle ARM
- Gestion des NSG
- Gestion des ASG
- Création de règles réseau
- Configuration d'Azure DNS
- Vérification de la configuration réseau
# Réalisation

**1. Création du réseau virtuel et des sous réseaux**

Création d'un réseau virtuel Azure afin de mettre en place l'infrastructure réseau du lab.

Chemin :

*Portail Azure → Réseaux virtuels → Créer*

<img width="811" height="986" alt="image" src="https://github.com/user-attachments/assets/17619130-cd55-4984-a106-4eb625701700" />

Le réseau virtuel permet de connecter et d'organiser les différentes ressources Azure.
Création des sous-réseaux nécessaires dans le réseau virtuel.

Les sous-réseaux permettent de séparer les différentes parties du réseau et d'organiser les ressources.

**2. Déploiement d'un réseau avec un modèle ARM**

Utilisation d'un modèle ARM afin de déployer un deuxième réseau virtuel.

Le modèle permet de définir la configuration du réseau sous forme de code et de reproduire plus facilement le déploiement. Il est composé de parametre.json et template.json : <img width="1402" height="2007" alt="image" src="https://github.com/user-attachments/assets/bb2105e7-0a29-4bc8-934c-85180dafb677" />
  <img width="910" height="424" alt="image" src="https://github.com/user-attachments/assets/0bb1af8e-0770-4121-981f-c388a0dc21dc" />

<img width="725" height="773" alt="image" src="https://github.com/user-attachments/assets/a83b3c08-e66c-41d1-b413-0b1233fac81e" />

**3. Création des groupes de sécurité**

Création d'un Application Security Group (ASG) et d'un Network Security Group (NSG).

Chemin : 

*Portail Azure → Groupes de sécurité d’application → Créer*

<img width="752" height="982" alt="image" src="https://github.com/user-attachments/assets/98565ad9-151f-45f1-9ab0-c5f83ba9bb72" />

L'ASG permet de regrouper les ressources ayant le même rôle.

Chemin : 

*Portail Azure → Groupe de sécurité réseau → Créer*

<img width="701" height="927" alt="image" src="https://github.com/user-attachments/assets/4c500c5b-fb10-4bba-9aa8-569637b68e37" />

Le NSG permet de contrôler le trafic réseau.

**4. Création des règles de sécurité**

Création d'une règle dans le NSG afin d'autoriser ou de bloquer certains types de trafic.

Les règles permettent de contrôler les communications entre les ressources.

<img width="1909" height="1963" alt="image" src="https://github.com/user-attachments/assets/92a3de69-a632-4c05-a216-48e57c03f84d" />
<img width="1897" height="1968" alt="image" src="https://github.com/user-attachments/assets/1bb2786d-5f15-43a8-8989-9d07e1461af1" />

**5. Association du NSG au réseau**

Association du Network Security Group au sous-réseau concerné.

Cette configuration permet d'appliquer les règles de sécurité aux ressources présentes dans le sous-réseau.

<img width="627" height="552" alt="image" src="https://github.com/user-attachments/assets/30524d2a-5cce-4eb9-9a80-2d90e362a07d" />

**6. Configuration d'Azure DNS**

Création d'une zone DNS publique et d'une zone DNS privée.

Chemin : 

*Portail Azure → Zones DNS publiques → Créer*

Le DNS permet de résoudre des noms de domaine et de faciliter l'accès aux ressources à l'aide de noms plutôt que d'adresses IP.

<img width="780" height="985" alt="Capture d&#39;écran 2026-09-10 023007" src="https://github.com/user-attachments/assets/60d1af84-4e57-41f1-8626-a07e79f2dc11" />

**7. Vérification de la configuration réseau**

Vérification de l'ensemble de la configuration créée pendant le lab.

<img width="943" height="986" alt="Capture d&#39;écran 2026-09-10 023301" src="https://github.com/user-attachments/assets/3f5e4915-7d6d-457a-86f0-4a43ce757c9c" />

Contrôles effectués :

<img width="505" height="203" alt="image" src="https://github.com/user-attachments/assets/80d8cadc-a7fb-408a-a218-e23a19aea0e6" />

# Comparaison des éléments

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
