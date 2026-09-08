Lab 03 — Gestion des ressources Azure avec des modèles ARM

AZ-104 — Microsoft Azure Administrator

## Objectif

Apprendre à automatiser le déploiement de ressources Azure avec des modèles ARM et Bicep.

L'objectif est de comprendre comment créer une ressource, récupérer son modèle, puis réutiliser ce modèle avec différentes méthodes de déploiement.

## Compétences mises en pratique
Création d'un modèle ARM
Modification d'un modèle ARM
Déploiement de ressources avec un modèle
Utilisation d'Azure Cloud Shell
Azure PowerShell
Azure CLI
Utilisation de Bicep
Vérification des déploiements
## Environnement
Élément	Configuration
Cloud	Microsoft Azure
Interface	Portail Azure
Automatisation	ARM / Bicep
Terminal	Azure Cloud Shell
Région	East US
Groupe de ressources	az104-rg3
Environnement	Lab personnel
# Réalisation

**1. Création d'un modèle ARM**

Création d'un disque managé dans le groupe de ressources TESTLAB3.

Paramètres principaux :

Nom : az104-disk1
Région : France Central
Taille : 32 GiB
Performance : Standard HDD

Une fois le disque créé, export du modèle ARM depuis la ressource.

Chemin :

*Disks → az104-disk1 → Exporter un modèle*

Le modèle et le fichier de paramètres sont ensuite téléchargés afin de pouvoir les réutiliser.

<img width="608" height="983" alt="image" src="https://github.com/user-attachments/assets/414fd323-bb4d-48a4-ae84-6d675aa04f20" />

<img width="824" height="668" alt="image" src="https://github.com/user-attachments/assets/1391c3ec-1322-4136-917e-dd366b832f02" />

**2. Modification et redéploiement du modèle ARM**

Utilisation du modèle téléchargé pour créer un deuxième disque sans refaire toute la configuration manuellement.

Chemin :

*Portail Azure → Déployer un modèle personnalisé → Créer votre propre modèle dans l'éditeur*

Modification du modèle :

remplacement du nom du disque par az104-disk2 ;
adaptation du fichier parameters.json.

Le modèle est ensuite déployé dans TESTLAB3.

<img width="1050" height="883" alt="image" src="https://github.com/user-attachments/assets/0df87923-1229-43c1-8d6c-875fd7ea6aa7" /> 
<img width="1372" height="813" alt="image" src="https://github.com/user-attachments/assets/a6ccff64-b4c7-404e-bb1a-9bc8b8aabe7d" />


<img width="1122" height="450" alt="image" src="https://github.com/user-attachments/assets/80becfa2-e5a5-4198-bc70-7ce01f3ad13b" />

**3. Déploiement avec Azure PowerShell**

Utilisation d'Azure Cloud Shell avec PowerShell pour déployer le modèle.

Chemin :

*Portail Azure → Cloud PowerShell ( icone de Terminal en haut à droite )*

Le nom du disque est modifié en az104-disk3 : 

<img width="2254" height="862" alt="image" src="https://github.com/user-attachments/assets/df7d3f79-e9b2-47fe-b7d7-0302a0f3f8e6" />

<img width="1050" height="602" alt="image" src="https://github.com/user-attachments/assets/695dba3b-519f-4cfc-b4a0-4c9905eb986b" />

Le déploiement est réalisé avec la commande :

New-AzResourceGroupDeployment -ResourceGroupName TESTLAB3 -TemplateFile template.json -TemplateParameterFile parameters.json

Une vérification est ensuite effectuée pour confirmer la création du disque avec cette commande : Get-AzDisk | ft Name,ResourceGroupName,Location,DiskSizeGb,ProvisioningState 
Mais vous pouvez toujours vérifier directement en allant dans le groupe de ressources.

<img width="952" height="248" alt="image" src="https://github.com/user-attachments/assets/91a70ee6-deff-4305-9c43-8fd2bfd42120" />

<img width="836" height="589" alt="image" src="https://github.com/user-attachments/assets/fb61dade-d9fc-435a-b82d-b6c0d244f8c4" />

**4. Déploiement avec Azure CLI**

Utilisation d'Azure Cloud Shell avec Bash / Azure CLI.

Chemin :

*Cloud Shell → Basculer vers Bash*

Le nom du disque est modifié en :

az104-disk4

Le modèle est ensuite déployé avec :

az deployment group create --resource-group TESTLAB3 --template-file template.json --parameters parameters.json

Une commande permet ensuite de vérifier les disques présents dans le groupe de ressources.

<img width="1233" height="815" alt="image" src="https://github.com/user-attachments/assets/50d0555a-e4ec-4e4b-ba81-8a6965b6365a" />

<img width="470" height="94" alt="image" src="https://github.com/user-attachments/assets/66a5eed5-1d69-42f4-8fb8-c7a29be14886" />

**5. Déploiement avec Azure Bicep**

Utilisation d'un fichier Bicep pour créer un dernier disque.

Chemin :

*Cloud Shell → Gérer les fichiers  → Charger*

Le fichier azuredeploydisk.bicep est chargé dans Cloud Shell puis modifié.

Paramètres modifiés :

Nom : az104-disk5
Taille : 32 GiB
Type : StandardSSD_LRS

Le fichier Bicep est ensuite déployé avec Azure PowerShell.

New-AzResourceGroupDeployment -ResourceGroupName "TESTLAB3" -TemplateFile ".\azuredeploydisk.bicep"

<img width="915" height="1027" alt="image" src="https://github.com/user-attachments/assets/93985655-13e8-4617-97d5-d9e4a2a3c6d1" />

## Comparaison des méthodes
Méthode	Utilisation
Portail Azure	Création et export d'un modèle
ARM Template	Déploiement reproductible avec un fichier JSON
Azure PowerShell	Déploiement avec des commandes PowerShell
Azure CLI	Déploiement avec des commandes Bash
Bicep	Déploiement avec une syntaxe simplifiée
Résultat

Ce lab m'a permis de mettre en pratique plusieurs méthodes d'automatisation des ressources Azure.

Cinq disques managés ont été déployés avec différentes méthodes :

az104-disk1 → création et export du modèle ARM ;
az104-disk2 → redéploiement du modèle ARM ;
az104-disk3 → Azure PowerShell ;
az104-disk4 → Azure CLI ;
az104-disk5 → Azure Bicep.
Ce que j'ai appris

J'ai compris qu'un modèle ARM permet de décrire la configuration d'une ressource Azure sous forme de code.

Un modèle peut ensuite être modifié et réutilisé pour créer d'autres ressources.

J'ai également utilisé PowerShell, Azure CLI et Bicep pour automatiser les déploiements.

Bicep permet notamment d'écrire une infrastructure Azure de manière plus simple que le format JSON des modèles ARM.

## Approche professionnelle

Dans un environnement professionnel, l'automatisation permet de réduire les manipulations manuelles et les risques d'erreur.

Les modèles ARM et Bicep permettent de reproduire une infrastructure de manière cohérente.

PowerShell et Azure CLI permettent quant à eux d'automatiser les opérations d'administration et les déploiements.

Cette approche constitue une base pour l'Infrastructure as Code (IaC).

## Source

Lab basé sur les exercices pratiques Microsoft Learning — AZ-104 Microsoft Azure Administrator.

Les manipulations ont été réalisées dans mon propre environnement Azure à des fins d'apprentissage.
