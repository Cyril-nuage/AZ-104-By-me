Lab 02 — Gouvernance et contrôle d’accès Azure

AZ-104 — Microsoft Azure Administrator

## Objectif

Mettre en pratique la gouvernance Azure et la gestion des accès à travers Microsoft Entra ID, Azure RBAC, Azure Policy, les étiquettes et les verrous de ressources.

## Compétences mises en pratique
Organisation des ressources Azure
Groupes d’administration
Azure RBAC
Création de rôles personnalisés
Attribution de rôles
Azure Policy
Gestion des étiquettes
Verrous de ressources
Contrôle de conformité
Principe du moindre privilège
## Réalisation
**1. Organisation avec les groupes d’administration**

Mise en place d'une structure permettant d'organiser les abonnements Azure au sein d'une hiérarchie.

Chemin :

*Portail Azure → Groupes d’administration*

Les groupes d’administration permettent de regrouper plusieurs abonnements et d'appliquer certaines règles de gouvernance à un niveau supérieur.

<img width="669" height="477" alt="Capture d&#39;écran 2026-08-31 133823" src="https://github.com/user-attachments/assets/2dd0d882-d570-4adf-9faf-5cf8e378b51e" />


**2. Création d'un rôle RBAC personnalisé**

Création d'un rôle personnalisé afin de contrôler précisément les opérations qu'un utilisateur peut effectuer sur les ressources Azure.

Le rôle permet notamment de définir :

les actions autorisées ;
les actions exclues ;
l'étendue d'application du rôle.

<img width="712" height="970" alt="Capture d&#39;écran 2026-08-31 141541" src="https://github.com/user-attachments/assets/90e040aa-4df9-46a6-8aa0-1e36595ea911" />

## Objectif

Appliquer le principe du moindre privilège en accordant uniquement les permissions nécessaires à un utilisateur ou à une équipe.

**3. Attribution d'un rôle Azure RBAC**

Attribution du rôle à un utilisateur ou à un groupe sur l'étendue définie.

Chemin :

*Groupe de ressources → Contrôle d’accès (IAM) → Ajouter → Ajouter une attribution de rôle*

## À retenir

Azure RBAC permet de déterminer :

Qui peut faire quoi, sur quelle ressource.

**4. Mise en place des étiquettes**

Ajout d'une étiquette au groupe de ressources afin d'identifier son centre de coût.

Exemple :

Étiquette	Valeur
Centre de coûts	000

Chemin :

*Groupe de ressources → Étiquettes*

<img width="434" height="689" alt="image" src="https://github.com/user-attachments/assets/dc55d031-c99d-47d4-bbea-6ff6800af667" />

## Objectif

Les étiquettes permettent notamment de faciliter :

l'identification des ressources ;
le suivi des coûts ;
la classification ;
la gestion des propriétaires ;
la gouvernance.
**5. Mise en place d'Azure Policy**

Création d'une stratégie Azure Policy afin d'imposer la présence d'une étiquette sur les ressources.

Chemin :

*Portail Azure → Policy → Définitions*

Stratégie utilisée :

Require a tag and its value on resources

Paramètres :

Étiquette : Centre de coûts
Valeur : 000
Application : Activée

<img width="837" height="941" alt="image" src="https://github.com/user-attachments/assets/765ed4b1-903c-41bc-9b6f-3bbc4927e1bd" />

**6. Test de conformité de la stratégie**

Tentative de création d'une ressource sans renseigner l'étiquette obligatoire.

La création est alors refusée par Azure Policy.

<img width="1087" height="339" alt="image" src="https://github.com/user-attachments/assets/32b180b8-56d8-4bbc-a3b1-19304d782493" />

## Résultat

Azure Policy permet d'imposer automatiquement des règles de gouvernance et d'empêcher la création de ressources qui ne respectent pas les exigences définies.

**7. Remédiation avec Azure Policy**

Mise en place d'une stratégie permettant d'hériter automatiquement de l'étiquette définie sur le groupe de ressources lorsqu'elle est absente.

Chemin :

*Portail Azure → Policy → Affectations*

Une tâche de remédiation permet ensuite de mettre en conformité les ressources concernées.

<img width="1092" height="942" alt="image" src="https://github.com/user-attachments/assets/8422a659-e2a8-4e99-977b-916ed72f9219" />

**8. Protection avec un verrou de ressource**

Mise en place d'un verrou de suppression sur le groupe de ressources.

Chemin :

*Groupe de ressources → Paramètres → Verrous*

Paramètre	Valeur
Nom du verrou	rg-lock
Type	Suppression

<img width="1183" height="391" alt="image" src="https://github.com/user-attachments/assets/7890c49f-319f-4f44-b43d-e0637ebd34b1" />

## Objectif

Les verrous de ressources permettent de protéger des ressources importantes contre des suppressions accidentelles.

**9. Test du verrou de ressource**

Tentative de suppression du groupe de ressources afin de vérifier le fonctionnement du verrou.

La suppression est refusée tant que le verrou est présent.

<img width="2493" height="490" alt="image" src="https://github.com/user-attachments/assets/11744482-647b-4b4e-8138-e5ac96d2acc7" />

## Résultat

Ce lab m'a permis de mettre en pratique plusieurs mécanismes fondamentaux de gouvernance Azure :

Organisation avec les groupes d’administration
Contrôle des accès avec Azure RBAC
Création d'un rôle personnalisé
Attribution de permissions
Classification avec les étiquettes
Application de règles avec Azure Policy
Remédiation des ressources non conformes
Protection contre les suppressions avec les verrous de ressources
## Ce que j'ai appris

Ce lab m'a permis de comprendre le rôle de plusieurs mécanismes complémentaires :

Azure RBAC → contrôle les actions qu'un utilisateur ou un groupe peut effectuer.

Azure Policy → définit et fait respecter des règles de conformité.

Étiquettes → permettent de classifier et d'identifier les ressources.

Verrous de ressources → protègent les ressources contre certaines opérations accidentelles.

## Approche professionnelle

Dans un environnement d'entreprise, la gouvernance permet de maintenir une infrastructure Azure organisée, sécurisée et conforme aux règles internes.

Une administration structurée consiste notamment à :

organiser les abonnements et ressources ;
appliquer le principe du moindre privilège ;
standardiser les ressources avec des étiquettes ;
contrôler la conformité avec Azure Policy ;
protéger les ressources critiques avec des verrous.

Ces mécanismes permettent également de réduire les erreurs d'administration et de faciliter le suivi de l'infrastructure.
