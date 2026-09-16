# Lab 10 — Supervision et monitoring Azure

AZ-104 — Microsoft Azure Administrator

# Objectif

Mettre en place et utiliser les outils de supervision Azure afin de surveiller les performances, l'état et les activités des ressources.

L'objectif est d'utiliser Azure Monitor et Log Analytics pour collecter, analyser et exploiter les données de supervision d'une machine virtuelle Azure.

## Compétences mises en pratique

- Création d'un espace de travail Log Analytics
- Configuration d'Azure Monitor
- Supervision d'une machine virtuelle
- Configuration des paramètres de diagnostic
- Analyse des métriques Azure
- Analyse des journaux avec Log Analytics
- Utilisation de requêtes KQL
- Consultation du journal d'activité

## Environnement

- Azure Portal
- Azure Monitor
- Log Analytics
- Azure Virtual Machines
- Azure Activity Log
- Groupe de ressources : `AZ-104-LAB10`

## Réalisation

### 1. Création de l'environnement de supervision

Déploiement de l'environnement nécessaire au laboratoire.

☀️ Chemin :

**Portail Azure → Déployer un modèle personnalisé**

Utiliser le modèle ARM fourni avec le laboratoire Microsoft.

Configuration principale :

- Groupe de ressources : `AZ-104-LAB10`
- Région : région Azure disponible
- Nom d'utilisateur : `localadmin`
- Mot de passe : mot de passe complexe

Le déploiement crée notamment une machine virtuelle et les ressources nécessaires à sa supervision.

📷 Capture d'écran : ressources déployées dans `AZ-104-LAB10`.

### 2. Création de l'espace de travail Log Analytics

Création d'un espace de travail permettant de centraliser et d'analyser les données de supervision.

☀️ Chemin :

**Portail Azure → Espaces de travail Log Analytics → Créer**

Configuration principale :

- Groupe de ressources : `AZ-104-LAB10`
- Nom : nom unique
- Région : même région que l'environnement de supervision

Sélectionner **Vérifier + créer**, puis **Créer**.

📷 Capture d'écran : création de l'espace de travail Log Analytics.

### 3. Vérification de la supervision de la machine virtuelle

Consultation des fonctionnalités de supervision disponibles pour la machine virtuelle.

☀️ Chemin :

**Machine virtuelle → Supervision**

Consulter notamment :

- Métriques
- Journaux
- Insights
- Alertes

Vérifier les informations disponibles concernant l'utilisation du processeur, de la mémoire et du réseau.

📷 Capture d'écran : supervision de la machine virtuelle avec les métriques disponibles.

### 4. Configuration des paramètres de diagnostic

Configuration des paramètres permettant d'envoyer les journaux de la machine virtuelle vers Log Analytics.

☀️ Chemin :

**Machine virtuelle → Supervision → Paramètres de diagnostic**

Créer ou modifier un paramètre de diagnostic.

Sélectionner l'espace de travail Log Analytics créé précédemment comme destination.

Enregistrer la configuration.

📷 Capture d'écran : paramètre de diagnostic associé à Log Analytics.

### 5. Analyse des métriques avec Azure Monitor

Utilisation de Metrics Explorer pour analyser les performances de la machine virtuelle.

☀️ Chemin :

**Machine virtuelle → Supervision → Métriques**

Sélectionner une métrique telle que :

**Pourcentage d'utilisation du processeur**

Configurer la période d'analyse puis observer l'évolution de la métrique.

📷 Capture d'écran : graphique de métrique Azure Monitor.

### 6. Consultation du journal d'activité

Consultation des opérations effectuées sur les ressources Azure.

☀️ Chemin :

**Portail Azure → Supervision → Journal d'activité**

Filtrer les événements selon :

- Abonnement
- Groupe de ressources
- Ressource
- Type d'opération
- Niveau de gravité

Vérifier les opérations réalisées sur les ressources du laboratoire.

📷 Capture d'écran : journal d'activité filtré.

### 7. Analyse des données avec Log Analytics

Ouverture de Log Analytics afin d'interroger les données collectées.

☀️ Chemin :

**Espace de travail Log Analytics → Journaux**

Exécuter une requête KQL permettant d'afficher les données disponibles.

Requête :

`Heartbeat | summarize count() by Computer`

Cette requête permet de vérifier les signaux de présence reçus depuis les machines supervisées.

📷 Capture d'écran : requête KQL et résultats dans Log Analytics.

### 8. Analyse des événements de la machine virtuelle

Utilisation de Log Analytics pour rechercher les événements collectés depuis la machine virtuelle.

☀️ Chemin :

**Espace de travail Log Analytics → Journaux**

Exécuter une requête sur les événements disponibles.

Requête :

`Event | where TimeGenerated > ago(1h) | summarize count() by EventLevelName`

Analyser les résultats obtenus et identifier les différents niveaux d'événements.

📷 Capture d'écran : résultats de la requête Log Analytics.

### 9. Consultation des alertes Azure Monitor

Consultation des règles d'alerte et des alertes générées par Azure Monitor.

☀️ Chemin :

**Portail Azure → Supervision → Alertes**

Vérifier les alertes disponibles pour les ressources du laboratoire.

Consulter notamment :

- Ressource concernée
- Condition
- Niveau de gravité
- État de l'alerte
- Heure de déclenchement

📷 Capture d'écran : page des alertes Azure Monitor.

### 10. Vérification finale de la supervision

Vérification de l'ensemble des composants configurés pendant le laboratoire.

Contrôler que :

- La machine virtuelle est supervisée.
- Les métriques sont disponibles.
- Les journaux sont envoyés vers Log Analytics.
- Les requêtes KQL peuvent être exécutées.
- Le journal d'activité est accessible.
- Les alertes Azure Monitor sont consultables.

📷 Capture d'écran : vue finale de la supervision Azure.

# Résultat

La machine virtuelle Azure est désormais intégrée à une solution de supervision basée sur **Azure Monitor** et **Log Analytics**.

Les métriques, journaux et événements peuvent être consultés et analysés depuis le portail Azure.

# Ce que j'ai appris

- Configurer un espace de travail Log Analytics.
- Utiliser Azure Monitor pour superviser des ressources.
- Analyser les métriques d'une machine virtuelle.
- Consulter le journal d'activité Azure.
- Collecter et analyser des journaux.
- Utiliser des requêtes KQL dans Log Analytics.
- Consulter les alertes Azure Monitor.

# Approche professionnelle

La supervision permet d'identifier les problèmes de performance, les erreurs et les événements importants affectant les ressources Azure.

Azure Monitor centralise les fonctionnalités de supervision tandis que Log Analytics permet d'effectuer des recherches et analyses avancées sur les données collectées.

# Source

Microsoft Learning — AZ-104 Microsoft Azure Administrator — Lab 11 : Implement Monitoring
