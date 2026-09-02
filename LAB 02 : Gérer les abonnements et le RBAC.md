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
## Environnement
Élément	Configuration
Cloud	Microsoft Azure
Identités	Microsoft Entra ID
Contrôle d’accès	Azure RBAC
Gouvernance	Azure Policy
Protection	Verrous de ressources
Interface	Portail Azure
Environnement	Lab personnel
## Réalisation
**1. Organisation avec les groupes d’administration**

Mise en place d'une structure permettant d'organiser les abonnements Azure au sein d'une hiérarchie.

Chemin :

*Portail Azure → Groupes d’administration*

Les groupes d’administration permettent de regrouper plusieurs abonnements et d'appliquer certaines règles de gouvernance à un niveau supérieur.

📸 Capture : hiérarchie des groupes d’administration.

**2. Création d'un rôle RBAC personnalisé**

Création d'un rôle personnalisé afin de contrôler précisément les opérations qu'un utilisateur peut effectuer sur les ressources Azure.

Le rôle permet notamment de définir :

les actions autorisées ;
les actions exclues ;
l'étendue d'application du rôle.

📸 Capture : définition du rôle personnalisé.

## Objectif

Appliquer le principe du moindre privilège en accordant uniquement les permissions nécessaires à un utilisateur ou à une équipe.

**3. Attribution d'un rôle Azure RBAC**

Attribution du rôle à un utilisateur ou à un groupe sur l'étendue définie.

Chemin :

*Groupe de ressources → Contrôle d’accès (IAM) → Ajouter → Ajouter une attribution de rôle*

📸 Capture : attribution du rôle.

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

📸 Capture : groupe de ressources avec l'étiquette configurée.

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

📸 Capture : configuration de la stratégie.

**6. Test de conformité de la stratégie**

Tentative de création d'une ressource sans renseigner l'étiquette obligatoire.

La création est alors refusée par Azure Policy.

📸 Capture : message indiquant que le déploiement est bloqué par la stratégie.

## Résultat

Azure Policy permet d'imposer automatiquement des règles de gouvernance et d'empêcher la création de ressources qui ne respectent pas les exigences définies.

**7. Remédiation avec Azure Policy**

Mise en place d'une stratégie permettant d'hériter automatiquement de l'étiquette définie sur le groupe de ressources lorsqu'elle est absente.

Chemin :

*Portail Azure → Policy → Affectations*

Une tâche de remédiation permet ensuite de mettre en conformité les ressources concernées.

📸 Capture : stratégie et/ou tâche de remédiation.

**8. Protection avec un verrou de ressource**

Mise en place d'un verrou de suppression sur le groupe de ressources.

Chemin :

*Groupe de ressources → Paramètres → Verrous*

Paramètre	Valeur
Nom du verrou	rg-lock
Type	Suppression

📸 Capture : verrou de ressource configuré.

## Objectif

Les verrous de ressources permettent de protéger des ressources importantes contre des suppressions accidentelles.

**9. Test du verrou de ressource**

Tentative de suppression du groupe de ressources afin de vérifier le fonctionnement du verrou.

La suppression est refusée tant que le verrou est présent.

📸 Capture : message indiquant que la suppression est bloquée.

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
