# Lab 10 — Supervision et monitoring Azure

AZ-104 — Microsoft Azure Administrator

# Objectif

Mettre en place et utiliser les outils de supervision Azure afin de surveiller les ressources et détecter les changements importants dans l'environnement.

L'objectif est d'utiliser Azure Monitor et Log Analytics pour collecter et analyser les données d'une machine virtuelle, créer une alerte basée sur le journal d'activité et configurer les notifications associées.

## Compétences mises en pratique

- Déploiement d'une machine virtuelle Azure
- Configuration d'Azure Monitor
- Utilisation d'un espace de travail Log Analytics
- Utilisation d'Azure Monitor Agent
- Configuration d'une Data Collection Rule
- Analyse des données avec Log Analytics
- Utilisation de requêtes KQL
- Création d'un groupe d'actions
- Création d'une alerte du journal d'activité
- Configuration d'une règle de traitement des alertes
- Vérification du déclenchement d'une alerte

## Réalisation

### 1. Déploiement de l'infrastructure du laboratoire

Déploiement d'une machine virtuelle et des ressources nécessaires à la collecte des données de supervision.

Chemin :

**Portail Azure → Déployer un modèle personnalisé → Créer votre propre modèle dans l'éditeur**

Utiliser le fichier `az104-11-vm-template.json` fourni avec le laboratoire Microsoft.

Configuration principale :

- Groupe de ressources : `AZ-104-LAB10`
- Région : région Azure disponible
- Taille de VM : `Standard_D2s_v5` si disponible
- Nom d'utilisateur : `localadmin`
- Mot de passe : mot de passe complexe

Le déploiement crée notamment :

- Une machine virtuelle `az104-vm0`
- Un espace de travail Log Analytics
- Une Data Collection Rule
- Un réseau virtuel
- Une interface réseau
- Une adresse IP publique
- Un groupe de sécurité réseau
- Un compte de stockage

<img width="2136" height="2013" alt="image" src="https://github.com/user-attachments/assets/d19f54dd-ea3f-4c26-bd92-28d9182cf3a2" />

### 2. Vérification de la supervision de la machine virtuelle

Vérification que les composants nécessaires à la collecte des données sont correctement configurés.

Chemin :

**Machine virtuelle → Paramètres → Extensions + applications**

Vérifier que l'extension :

**AzureMonitorWindowsAgent**

possède le statut **Provisioning succeeded**.

Chemin :

**Data Collection Rule → Configuration → Ressources**

Vérifier que la machine virtuelle `az104-vm0` est associée à la Data Collection Rule.

<img width="1067" height="334" alt="image" src="https://github.com/user-attachments/assets/d90013ef-ff5e-4732-b841-54e4b1736c45" />
<img width="1061" height="323" alt="image" src="https://github.com/user-attachments/assets/4c5bcb19-8e33-400e-8882-e5dc2c6ce50f" />

### 3. Vérification des données avec Log Analytics

Vérification que l'agent Azure Monitor envoie correctement les données de supervision vers Log Analytics.

Chemin :

**Espace de travail Log Analytics → Journaux**

Utiliser une requête KQL permettant de vérifier les signaux de présence de la machine virtuelle.

Requête :

`Heartbeat | where TimeGenerated > ago(30m) | where Computer =~ "az104-vm0" | summarize HeartbeatCount = count(), LastHeartbeat = max(TimeGenerated) by Computer, Category`

Vérifier que les résultats contiennent `az104-vm0`.

📷 Capture d'écran : requête KQL et résultats contenant `az104-vm0`.

Effectuer ensuite une requête permettant de vérifier les données de performance de la machine virtuelle.

Requête :

`InsightsMetrics | where TimeGenerated > ago(30m) | where Computer =~ "az104-vm0" | where Name == "UtilizationPercentage" | summarize AverageUtilization = avg(Val) by bin(TimeGenerated, 5m), Computer | render timechart`

<img width="1047" height="937" alt="image" src="https://github.com/user-attachments/assets/db0169fa-8d0d-4ec5-a6ba-9f570d382dd8" />

### 4. Création d'un groupe d'actions

Création d'un groupe d'actions permettant d'envoyer une notification lorsqu'une alerte est déclenchée.

Chemin :

**Portail Azure → Monitor → Alertes → Groupes d'actions → Créer**

Configuration principale :

- Groupe de ressources : `AZ-104-LAB10`
- Région : `Global`
- Nom du groupe d'actions : `Alert the operations team`
- Nom d'affichage : `AlertOpsTeam`

Ajouter une notification :

- Type : **E-mail/SMS/Push/Voix**
- Nom : `VM was deleted`
- Notification : **E-mail**
- Adresse e-mail : adresse e-mail utilisée

Sélectionner **Vérifier + créer**, puis **Créer**.

<img width="1062" height="984" alt="image" src="https://github.com/user-attachments/assets/1940e32e-e489-42a0-9a69-d600ba60babb" />
<img width="506" height="219" alt="image" src="https://github.com/user-attachments/assets/5ec704e7-2bef-4d5a-b935-c01af4cfecb8" />

Vérifier également la réception de l'e-mail confirmant l'ajout au groupe d'actions.

### 5. Création d'une alerte du journal d'activité

Création d'une alerte permettant de détecter la suppression d'une machine virtuelle.

Chemin :

**Azure Monitor → Alertes → Créer → Règle d'alerte**

Dans **Étendue**, sélectionner l'abonnement Azure utilisé.

Dans **Condition**, sélectionner :

**Journal d'activité**

Puis sélectionner le signal :

**Delete Virtual Machine (Virtual Machines)**

L'opération correspond à :

`Microsoft.Compute/virtualMachines/delete`

Dans **Actions**, sélectionner le groupe d'actions :

`Alert the operations team`

Dans **Détails**, configurer :

- Groupe de ressources : `AZ-104-LAB10`
- Nom de la règle : `VM was deleted`
- Description : `A VM in the subscription was deleted`
- Région : `Global`
- Activer la règle lors de sa création : Oui

Sélectionner **Vérifier + créer**, puis **Créer**.

<img width="782" height="886" alt="image" src="https://github.com/user-attachments/assets/6c1d54f4-7887-46fe-a286-685dc959ed00" />

Chemin :

**Azure Monitor → Alertes → Règles d'alerte**

Vérifier que la règle `VM was deleted` est active.

<img width="1065" height="354" alt="image" src="https://github.com/user-attachments/assets/5d831104-a62b-40c0-b8f2-0894ebf318ea" />

### 6. Configuration d'une règle de traitement des alertes

Configuration d'une règle permettant de supprimer les notifications pendant une période de maintenance planifiée.

Chemin :

**Azure Monitor → Alertes → Règles de traitement des alertes → Créer**

Sélectionner l'abonnement Azure comme portée.

Dans les paramètres de la règle :

**Supprimer les notifications**

Configurer la période de maintenance :

- Application de la règle : **À une heure spécifique**
- Début : aujourd'hui à 22:00
- Fin : demain à 07:00
- Fuseau horaire : fuseau horaire local

<img width="749" height="749" alt="image" src="https://github.com/user-attachments/assets/3079ffd7-81d2-43c2-9cd3-8f3d54efa902" />

Dans les détails :

- Groupe de ressources : `AZ-104-LAB10`
- Nom : `Planned Maintenance`
- Description : `Suppress notifications during planned maintenance.`

Sélectionner **Vérifier + créer**, puis **Créer**.

### 7. Déclenchement et vérification de l'alerte

Suppression de la machine virtuelle afin de vérifier que l'alerte du journal d'activité fonctionne correctement.

Avant la suppression, vérifier que la règle `VM was deleted` est activée.

Chemin :

**Portail Azure → Machines virtuelles → `az104-vm0` → Supprimer**

Supprimer la machine virtuelle et confirmer la suppression des ressources.

<img width="1067" height="267" alt="image" src="https://github.com/user-attachments/assets/aa7c038f-1b41-4795-a4de-24e23e500cae" />
<img width="776" height="180" alt="image" src="https://github.com/user-attachments/assets/158839cd-d335-4f92-9052-b4284957105f" />

# Résultat

La machine virtuelle Azure a été intégrée à une solution de supervision basée sur **Azure Monitor** et **Log Analytics**.

Les données de présence et de performance ont été collectées puis vérifiées à l'aide de requêtes KQL.

Un groupe d'actions et une alerte basée sur le journal d'activité ont été configurés afin de détecter la suppression d'une machine virtuelle et d'envoyer une notification par e-mail.

Une règle de traitement des alertes a également été mise en place afin de supprimer les notifications pendant une période de maintenance planifiée.

# Ce que j'ai appris

- Déployer une infrastructure Azure destinée à la supervision.
- Utiliser Azure Monitor et Log Analytics.
- Vérifier la collecte des données d'une machine virtuelle.
- Utiliser des requêtes KQL pour analyser les données.
- Créer un groupe d'actions.
- Créer une alerte basée sur le journal d'activité.
- Configurer une règle de traitement des alertes.
- Vérifier le déclenchement et la notification d'une alerte.

# Approche professionnelle

La supervision permet aux administrateurs d'identifier les événements importants et de surveiller l'état des ressources Azure.

Azure Monitor permet de centraliser la supervision et les alertes, tandis que Log Analytics permet d'analyser les données collectées à l'aide de requêtes KQL.

La mise en place de groupes d'actions et de règles de traitement permet également d'adapter les notifications aux besoins opérationnels et aux périodes de maintenance.

# Source

Lab basé sur les exercices pratiques Microsoft Learning — AZ-104 Microsoft Azure Administrator.
Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
