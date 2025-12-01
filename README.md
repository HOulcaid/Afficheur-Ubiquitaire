---

# 🖼️ Projet Tutoré: Afficheur Ubiquitaire Multi-Écran

## 🌟 Vue d'Ensemble du Projet

Ce projet tutoré, réalisé dans le cadre de la Licence Professionnelle **LP MERIT** à l'UPECiut (Université Paris-Est Créteil), avait pour objectif la conception et la réalisation d'une architecture de **visualisation nomade et multi-écran**, souvent désignée comme un **Afficheur Ubiquitaire** (ou Mur d'images). Il s'agissait d'un projet **DIY (Do It Yourself)** visant à présenter une maquette fonctionnelle.

* **Année :** 2019-2020
* **Auteurs :** Matthieu COURBE, Hassan OULCAID, Guillaume SEUROT, Tarek AISSAOUI
* **Tuteur :** M.SOUHI Sami

---

## 💡 Choix de la Solution Technique : SAGE2

Après une étude comparative (état de l'art) de différentes architectures possibles, le groupe a retenu la solution **SAGE2**.

| Solution Étudiée | Description |
| :--- | :--- |
| **PiWall** | Mur d'images reposant sur un modèle client/serveur avec des Raspberry Pi (RPi) clients pour le cast de flux vidéo. |
| **TIDE** | Tiled Interactive Display Environment (Environnement d'affichage interactif en mosaïque de BlueBrain) offrant une interaction tactile multi-fenêtres et multi-utilisateurs. |
| **SAGE2** | **S**calable **A**mplified **G**roup **E**nvironment. Plate-forme Web permettant aux équipes d'afficher, de gérer, de partager et d'étudier des ensembles de données à grande échelle sur des murs d'affichage carrelés. |

**SAGE2** a été choisi pour sa flexibilité, étant une refonte complète de SAGE basée sur des technologies web et cloud.

---

## 🛠️ Matériel et Architecture Physique

La maquette physique a été conçue sur une architecture de $3 \times 3$ écrans et un modèle Client/Serveur.

### Composition Matérielle

| Composant | Quantité | Rôle / Caractéristiques |
| :--- | :--- | :--- |
| **Écrans** | 9 | Écrans **LCD DELL 17 pouces** (1440 x 900 à 60 Hz, connectique VGA). |
| **Clients** | 9 RPi | Un **Raspberry Pi** par écran. |
| **Serveur** | 1 NUC | Serveur SAGE2 de diffusion de contenu (sous **Windows 10**). |
| **Réseau** | 1 RPi | Un RPi supplémentaire servant de **relais DHCP**. |
| **Connectivité** | 1 Switch 24 ports Gb, 1 AP wireless AC Gb. | Le rôle de l'AP est de permettre un accès sans fil au serveur. |
| **Support** | Bois et Métal | Plaque en bois (1,40 m²) et support métallique (1,40m / 2m). |

### Réseau et Flux

* **Réseau Utilisé :** `192.168.1.0/24`.
* **Flux Vidéo :** Le serveur NUC envoie **30 Mb/s** à chaque Raspberry Pi.
* **Identification Client :** Chaque RPi est identifié par son adresse MAC, son adresse IP et sa position dans l'architecture.

---

## 💻 Installation et Configuration Logicielle

Le fonctionnement de SAGE2 repose sur des technologies Web pour le serveur et des navigateurs pour les clients.

### 1. Pré-requis et Serveur

* **Pré-requis logiciel :** Installation de **Node.js** pour lancer les scripts SAGE2.
* **Exécution de SAGE2 :** Contrôlée par le processus de **"Launcher"** (fichier `Launcher.bat`).
* **Accès au Launcher :** Accessible à l'URL `http://localhost:10000`.

### 2. Accès et Gestion

* **Authentification par défaut :** Le Launcher est protégé par un mot de passe.
    * **Nom d'utilisateur :** `sage2`
    * **Mot de passe :** `sage2`
* **Interface de base :** Les fonctions principales (Start, Stop, Set a meeting access) sont accessibles sur `http://localhost:10000/#SAGE2`.
* **Gestion des ressources :** Un gestionnaire de fichiers est disponible pour gérer et organiser les médias (vidéos, images, documents).

### 3. Configuration des Clients (RPi)

* Chaque Raspberry Pi est configuré pour ouvrir une **page Web** (client SAGE2) à chaque démarrage, avec son ID apparaissant dans le lien de la page.
* L'interface d'administration permet de gérer la résolution de chaque écran, les numéros de ports d'accès, et la disposition de chacun sur le quadrillage.

---

## 📜 Conclusion

Ce projet a permis à l'équipe d'approfondir ses connaissances en nouvelles technologies de communication, de maîtriser la technologie **SAGE2**, et de développer des compétences humaines essentielles telles que le travail collaboratif, le respect des jalons et la gestion des difficultés.
