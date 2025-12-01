-----

# 🚀 Résumé de Projets Techniques

Ce dépôt rassemble les réalisations de deux projets majeurs :

1.  Un projet **Cloud Native & DevOps** sur Google Kubernetes Engine (GKE) impliquant le déploiement de microservices, la gestion des clusters et la mise en place de la surveillance.
2.  Un **Projet Tutoré** académique sur la conception et la réalisation d'un **Afficheur Ubiquitaire** (Mur d'images) basé sur la technologie SAGE2.

-----

## ☁️ Projet Cloud Native & DevOps (GKE/Microservices)

Ce projet a consisté à déployer et gérer une application de microservices (Online Boutique) sur Google Kubernetes Engine (GKE) en respectant des directives strictes de configuration, de migration et de mise à jour.

### ⚙️ Environnement Technique

| Catégorie | Détail |
| :--- | :--- |
| **Application** | Microservices Demo (Online Boutique) |
| **Plateforme** | Google Kubernetes Engine (GKE) |
| **Nom du Cluster** | `onlineboutique-cluster-422` |
| **Zone de Déploiement** | `us-east1-c` |
| **Taille des Nœuds** | `e2-standard-2` (2 vCPU, 8 Go) |
| **Canal de Publication** | `rapid` |
| **Surveillance** | Cloud Logging & Monitoring Agents |

### 🛠️ Tâches Clés Réalisées

#### **1. Déploiement Initial**

  * Création d'un cluster zonal de **2 nœuds**.
  * Mise en place des namespaces `dev` et `prod` pour séparer les environnements.
  * Déploiement initial de l'application dans le namespace `dev`.

<!-- end list -->

```bash
git clone https://github.com/GoogleCloudPlatform/microservices-demo.git
cd microservices-demo
kubectl apply -f ./release/kubernetes-manifests.yaml --namespace dev
```

#### **2. Migration des Pools de Nœuds**

Une migration des déploiements vers un nouveau pool de nœuds a été effectuée pour respecter une nouvelle spécification de machine :

  * Création d'un nouveau pool de **2 nœuds** avec une machine de type `custom-2-3584`.
  * Migration sécurisée des déploiements par **cordonnement (`cordoning off`) et drainage (`draining`)** du `default-pool`.
  * Suppression du `default-pool` une fois la migration terminée.

#### **3. Mise en Place de la Surveillance**

L'installation des agents sur la VM `apache-vm` a été effectuée pour assurer la collecte de métriques et de logs.

  * Installation des agents Cloud Logging et Cloud Monitoring.
  * Activation du plugin pour la surveillance du serveur Web Apache.

#### **4. Mise à Jour du Frontend (Haute Disponibilité)**

Une mise à jour de l'image du service `frontend` a été appliquée tout en garantissant la continuité du service :

  * Création d'un **Pod Disruption Budget (PDB)** nommé `onlineboutique-frontend-pdb`.
  * Configuration de la `min-availability` (disponibilité minimale) à **1**.
  * Mise à jour de l'image Docker du déploiement `frontend` vers la version `gcr.io/qwiklabs-resources/onlineboutique-frontend:v2.1`.
  * Définition de la politique de tirage d'image (`ImagePullPolicy`) à `Always`.

-----

## 🖼️ Projet Tutoré: Afficheur Ubiquitaire Multi-Écran

Ce projet tutoré (Année 2019-2020) portait sur la conception et la réalisation d'une architecture de visualisation nomade et multi-écran, connue sous le nom d'**Afficheur Ubiquitaire** ou mur d'images.

### 💡 Solution et Technologies

| Catégorie | Détail | Source |
| :--- | :--- | :--- |
| **Objectif** | Réaliser un afficheur nomade ubiquitaire (DIY Project) | |
| **Solution Retenue** | **SAGE2** (Scalable Amplified Group Environment) | |
| **Alternatives Étudiées** | PiWall, TIDE | |
| **Description SAGE2** | Plate-forme Web permettant d'afficher, de gérer et de juxtaposer des ensembles de données et des supports numériques sur des murs d'affichage carrelés | |
| **Logiciels Pré-requis** | **Node.js** (pour lancer les scripts) et Google Chrome 64bit | |

### 📐 Architecture Physique (Maquette)

L'architecture est basée sur un modèle client/serveur avec un mur d'images de $3 \times 3$ écrans.

| Composant | Quantité | Rôle / Caractéristiques | Source |
| :--- | :--- | :--- | :--- |
| **Écrans** | 9 | LCD DELL 17 pouces, résolution 1440 x 900 | |
| **Clients d'Affichage** | 9 RPi | Un Raspberry Pi par écran | |
| **Serveur SAGE2** | 1 NUC | Serveur de diffusion de contenu (sous Windows 10) | |
| **Relais Réseau** | 1 RPi | Utilisé comme relais DHCP pour distribuer les adresses IP | |
| **Réseau** | 1 Switch 24 ports Gb, 1 AP wireless AC Gb | Réseau 192.168.1.0/24. Débit de **30 Mb/s** envoyé à chaque RPi | |
| **Support** | Planche en bois (1,40 m²), Support métallique (1,40m / 2m) | Conception et assemblage de la structure physique (conception SolidWorks) | |

### 💻 Configuration SAGE2

  * **Exécution :** L'exécution de SAGE2 est contrôlée par le processus **Launcher** (fichier `Launcher.bat`).
  * **Accès :** Le Launcher est accessible sur l'URL `http://localhost:10000`.
  * **Authentification :** Les identifiants par défaut pour le Launcher sont **`sage2`** / **`sage2`**.
  * **Configuration Client :** Chaque Raspberry Pi est configuré pour ouvrir automatiquement une page Web (client SAGE2) au démarrage, et est identifié par son adresse MAC, IP et sa position dans l'architecture.
