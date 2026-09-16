# Lab 09 — Protection des données Azure

AZ-104 — Microsoft Azure Administrator

## Objectif

Mettre en place une stratégie de protection des machines virtuelles Azure à l'aide d'Azure Backup et d'Azure Site Recovery.

L'objectif est de créer un coffre Recovery Services, configurer une stratégie de sauvegarde, protéger une machine virtuelle et mettre en place sa réplication vers une seconde région.

## Compétences mises en pratique

- Création et configuration d'un coffre Recovery Services
- Configuration d'Azure Backup
- Création d'une stratégie de sauvegarde
- Protection d'une machine virtuelle Azure
- Suivi des opérations de sauvegarde
- Configuration d'Azure Site Recovery
- Réplication d'une machine virtuelle vers une autre région

## Réalisation

### 1. Création de la machine virtuelle

Déploiement d'une machine virtuelle qui servira de ressource de test pour la sauvegarde et la réplication.

☀️ Chemin :

**Portail Azure → Déployer un modèle personnalisé**

Utiliser le modèle ARM fourni avec le laboratoire Microsoft.

Configuration principale :

- Groupe de ressources : `AZ-104-LAB9`
- Région : région Azure disponible
- Nom d'utilisateur : `localadmin`
- Mot de passe : mot de passe complexe

Attendre la fin du déploiement puis vérifier que la machine virtuelle est correctement créée.

📷 Capture d'écran : machine virtuelle déployée dans `AZ-104-LAB9`.

### 2. Création du coffre Recovery Services

Création d'un coffre Recovery Services destiné à stocker les points de récupération de la machine virtuelle.

☀️ Chemin :

**Portail Azure → Coffres Recovery Services → Créer**

Configuration principale :

- Groupe de ressources : `AZ-104-LAB9`
- Nom du coffre : `AZ-104-RSV-LAB9`
- Région : région Azure disponible

Sélectionner **Vérifier + créer**, puis **Créer**.

📷 Capture d'écran : configuration du coffre Recovery Services.

### 3. Configuration du coffre

Vérification des paramètres de protection du coffre Recovery Services.

☀️ Chemin :

**Recovery Services Vault → AZ-104-RSV-LAB9 → Paramètres → Propriétés**

Vérifier notamment :

- Type de réplication du stockage
- Suppression réversible
- Paramètres de sécurité du coffre

📷 Capture d'écran : propriétés du coffre Recovery Services.

### 4. Activation de la sauvegarde de la machine virtuelle

Configuration d'une sauvegarde quotidienne de la machine virtuelle.

☀️ Chemin :

**Recovery Services Vault → Vue d'ensemble → Sauvegarde**

Configuration principale :

- Où s'exécute votre charge de travail : **Azure**
- Que souhaitez-vous sauvegarder : **Machine virtuelle**
- Stratégie : **Créer une stratégie**
- Fréquence : **Quotidienne**
- Rétention : selon les paramètres proposés par le laboratoire

Sélectionner ensuite la machine virtuelle créée précédemment puis **Activer la sauvegarde**.

📷 Capture d'écran : stratégie de sauvegarde et machine virtuelle protégée.

### 5. Lancement d'une sauvegarde à la demande

Lancement manuel d'une sauvegarde afin de vérifier le fonctionnement d'Azure Backup.

☀️ Chemin :

**Recovery Services Vault → Éléments protégés → Éléments de sauvegarde → Machines virtuelles Azure**

Sélectionner la machine virtuelle puis choisir :

**Sauvegarder maintenant**

Conserver la durée de rétention proposée puis valider.

Vérifier ensuite que le travail de sauvegarde est créé.

📷 Capture d'écran : sauvegarde à la demande en cours ou terminée.

### 6. Vérification des travaux de sauvegarde

Vérification de l'état des opérations effectuées par Azure Backup.

☀️ Chemin :

**Recovery Services Vault → Supervision → Travaux de sauvegarde**

Rechercher le travail correspondant à la machine virtuelle.

Vérifier notamment :

- État du travail
- Machine virtuelle concernée
- Heure de début
- Heure de fin

📷 Capture d'écran : travail de sauvegarde terminé.

### 7. Configuration des paramètres de diagnostic

Activation des journaux permettant de superviser les opérations de sauvegarde et de récupération.

☀️ Chemin :

**Recovery Services Vault → Supervision → Paramètres de diagnostic**

Créer un paramètre de diagnostic et sélectionner les catégories de journaux demandées par le laboratoire.

Configurer ensuite la destination de stockage.

Enregistrer les modifications.

📷 Capture d'écran : paramètres de diagnostic du coffre.

### 8. Création du coffre de récupération après sinistre

Création d'un coffre Recovery Services destiné à la réplication de la machine virtuelle.

☀️ Chemin :

**Portail Azure → Coffres Recovery Services → Créer**

Configuration principale :

- Groupe de ressources : `AZ-104-LAB9`
- Nom : `AZ-104-RSV-DR-LAB9`
- Région : région différente de celle de la machine virtuelle

Sélectionner **Vérifier + créer**, puis **Créer**.

📷 Capture d'écran : création du coffre de récupération après sinistre.

### 9. Activation de la réplication de la machine virtuelle

Configuration d'Azure Site Recovery afin de répliquer la machine virtuelle vers une autre région Azure.

☀️ Chemin :

**Machine virtuelle → Opérations → Récupération d'urgence**

Configurer :

- Région source
- Région cible
- Abonnement
- Groupe de ressources cible
- Réseau virtuel cible

Vérifier la configuration puis sélectionner :

**Vérifier + démarrer la réplication**

Lancer ensuite la réplication.

📷 Capture d'écran : configuration de la réplication de la machine virtuelle.

### 10. Vérification de la réplication

Vérification de l'état de protection de la machine virtuelle.

☀️ Chemin :

**Recovery Services Vault → Éléments protégés → Éléments répliqués**

Sélectionner la machine virtuelle et vérifier :

- État de la réplication
- Intégrité de la réplication
- Progression de la synchronisation
- Région cible

Attendre la fin de la synchronisation initiale.

📷 Capture d'écran : machine virtuelle répliquée et protégée.

## Résultat

La machine virtuelle Azure est protégée par Azure Backup grâce à un coffre Recovery Services et une stratégie de sauvegarde.

La réplication de la machine virtuelle vers une seconde région est également configurée avec Azure Site Recovery.

## Ce que j'ai appris

- Mettre en place une sauvegarde de machine virtuelle avec Azure Backup.
- Configurer une stratégie de sauvegarde.
- Utiliser un coffre Recovery Services.
- Lancer et suivre une sauvegarde.
- Configurer les paramètres de diagnostic.
- Mettre en place la réplication d'une machine virtuelle avec Azure Site Recovery.
- Vérifier l'état de protection et de réplication d'une machine virtuelle.

## Approche professionnelle

Azure Backup permet de protéger les données et les machines virtuelles grâce à des points de récupération.

Azure Site Recovery complète cette protection en permettant de répliquer les machines virtuelles vers une autre région Azure afin de préparer un scénario de reprise après sinistre.

## Source

Microsoft Learning — AZ-104 Microsoft Azure Administrator
