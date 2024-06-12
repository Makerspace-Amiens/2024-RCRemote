---
layout: default
nav_order: 2
title: Objectifs du projet
---

# <span style="color:#003366">_Introduction_</span>

Nous sommes deux étudiants en troisième année à UniLaSalle Amiens. Dans le cadre de notre formation en ingénierie, il nous a été demandé de réaliser un projet ayant pour objectif de nous faire découvrir les divers domaines qu’un ingénieur peut être amené à gérer. Pour répondre à cet objectif, nous avons choisi de concevoir et de réaliser une manette multi-usage capable de contrôler divers objets via une connexion Bluetooth.

Ce projet nous a permis d’explorer différentes facettes de l'ingénierie, notamment la conception électronique, la modélisation 3D, l'impression 3D, et la programmation de microcontrôleurs. Nous avons utilisé des logiciels spécialisés tels que KICAD pour la conception de circuits imprimés et Onshape pour la modélisation 3D, ainsi que l'IDE Arduino pour programmer notre microcontrôleur ESP32. 

En surmontant les divers défis techniques, nous avons non seulement acquis des compétences techniques précieuses mais également développé notre capacité à résoudre des problèmes complexes et à travailler efficacement en équipe. Ce projet représente une étape importante dans notre formation, nous préparant à affronter les défis réels du métier d'ingénieur.

![Illustration introduction](images/image7.png)

# <span style="color:#DB1702">_Contexte du Projet_</span>

Dans le cadre de notre troisième année à UniLaSalle Amiens, nous avons entrepris un projet visant à nous immerger dans différents domaines de l'ingénierie. L'objectif principal est de développer une compréhension pratique des compétences nécessaires pour concevoir, fabriquer et programmer des dispositifs technologiques.

L'ingénierie étant vaste et multidisciplinaire, nous avons choisi de concevoir une manette multi-usage, capable de contrôler divers appareils via Bluetooth, en utilisant un microcontrôleur ESP32.

Ce projet, basé sur l'apprentissage par la pratique, nous prépare aux défis réels de notre future carrière d'ingénieur. Nous avons dû maîtriser des logiciels de conception de circuits imprimés (KICAD) et de modélisation 3D (Onshape), assembler les composants électroniques, résoudre des problèmes d'impression 3D, et programmer l'ESP32 en langage C. Ce projet synthétise les compétences acquises au cours de notre formation et nous prépare aux exigences du monde professionnel.

![Illustration contexte](images/image1.jpg)


# <span style="color:#003366">_Objectifs du Projet_</span>


L'objectif principal de notre projet est de concevoir, fabriquer et programmer une manette multi-usage capable de contrôler divers appareils électroniques via une connexion Bluetooth, en utilisant un microcontrôleur ESP32. Ce projet vise à :

- Développer des compétences pratiques : Appliquer nos connaissances théoriques en électronique, modélisation 3D et programmation pour créer un dispositif fonctionnel.
- Maîtriser des outils technologiques : Utiliser des logiciels spécialisés tels que KICAD pour la conception de circuits imprimés et Onshape pour la modélisation 3D.
- Résoudre des problèmes techniques : Surmonter les défis rencontrés lors de l'assemblage physique des composants et de l'impression 3D.
- Intégrer différentes disciplines de l'ingénierie : Combiner des compétences en électronique, en mécanique et en programmation pour réaliser un projet complet et fonctionnel.
- Préparer à la vie professionnelle : Acquérir une expérience pratique et développer des compétences transférables nécessaires à notre future carrière d'ingénieur.

![Illustration contexte](images/image2.jpeg)

# <span style="color:#DB1702">_Existant_</span>

Avant de débuter ce projet, nous avions acquis une base solide de connaissances théoriques et pratiques dans plusieurs domaines de l'ingénierie grâce à notre cursus à UniLaSalle Amiens. Voici un résumé de ce que nous savions avant de commencer le projet :

## Électronique :

- Conception de Circuits : Connaissances fondamentales sur la conception de circuits électroniques, la lecture de schémas et l'utilisation de logiciels de conception de circuits imprimés (KICAD).
- Composants Électroniques : Compréhension des différents types de composants électroniques (résistances, condensateurs, microcontrôleurs, etc.) et de leurs fonctions.

## Programmation :

- Langages de Programmation : Maîtrise des langages de programmation tels que le C et le C++, particulièrement dans le contexte de la programmation de microcontrôleurs.
- Développement avec Arduino : Expérience de programmation sur des plateformes comme Arduino, avec des projets précédents utilisant l'IDE Arduino pour développer des applications simples.

## Modélisation 3D :

- Logiciels de CAO : Utilisation de logiciels de conception assistée par ordinateur (CAO) tels que Onshape pour créer et modifier des modèles 3D.
- Techniques de Modélisation : Compétences de base en modélisation 3D, y compris la création de formes géométriques, l'assemblage de composants et la préparation de modèles pour l'impression 3D.

## Impression 3D :

- Préparation des Modèles : Connaissance des processus de tranchage et de préparation des fichiers pour l'impression 3D, notamment l'utilisation de logiciels comme Cura.
- Matériaux et Techniques d'Impression : Familiarité avec les types de matériaux d'impression 3D et les techniques de base pour réaliser des impressions de qualité.

## Gestion de Projet :

- Planification et Organisation : Compétences en gestion de projet, incluant la planification des étapes de développement, la répartition des tâches et le suivi de l'avancement du projet.
- Travail en Équipe : Expérience de travail collaboratif sur des projets académiques, incluant la communication, la coordination et la résolution de conflits.

![Illustration etat de l'art](images/image3.png)

# <span style="color:#003366">_Cahier des Charges_</span>

## 1. Introduction

### 1.1 Contexte
Le projet consiste à développer une télécommande basée sur le microcontrôleur ESP32, capable de contrôler divers périphériques via WiFi ou Bluetooth. La télécommande inclut des composants tels que des joysticks, des boutons poussoirs, des boutons ON/OFF et un écran LCD pour afficher les informations.

### 1.2 Objectifs
L'objectif est de concevoir, réaliser et programmer une télécommande fonctionnelle, en utilisant l'ESP32 pour gérer les entrées des joysticks et des boutons, traiter les données et commander un écran LCD, ainsi que communiquer avec les périphériques cibles.

## 2. Spécifications Fonctionnelles

### 2.1 Composants Matériels
- **Microcontrôleur** : ESP32
- **Entrées** :
  - 2 Joysticks
  - 4 Boutons poussoirs
  - 2 Boutons ON/OFF
- **Sorties** :
  - Écran LCD
- **Alimentation** : Source d'alimentation adaptée (batterie ou alimentation externe)

### 2.2 Fonctionnalités
- **Lecture des Entrées** :
  - Capture de la position des joysticks (x, y).
  - Capture de l'état des boutons poussoirs (pressé/non pressé).
  - Capture de l'état des boutons ON/OFF.
- **Traitement des Données** :
  - Interprétation des mouvements des joysticks pour générer des commandes.
  - Détection et gestion des appuis sur les boutons poussoirs et ON/OFF.
- **Génération des Commandes** :
  - Affichage des informations pertinentes sur l'écran LCD.
  - Transmission des commandes via WiFi/Bluetooth pour contrôler les périphériques.

## 3. Spécifications Techniques

### 3.1 Microcontrôleur ESP32
- Double cœur Tensilica LX6
- Connectivité WiFi et Bluetooth intégrée
- Interfaces GPIO pour connecter les joysticks, boutons et écran LCD

### 3.2 Joysticks
- Module analogique avec deux axes (x, y)
- Connexion via entrées analogiques de l'ESP32

### 3.3 Boutons Poussoirs et ON/OFF
- Boutons numériques pour entrées binaires (haut/bas)
- Connexion via entrées GPIO de l'ESP32

### 3.4 Écran LCD
- Affichage des informations et retour visuel à l'utilisateur
- Connexion via SPI ou I2C à l'ESP32

### 3.5 Alimentation
- Source d'alimentation adaptée pour ESP32 et composants connectés
- Possibilité d'utiliser une batterie rechargeable

## 4. Architecture du Système

### 4.1 Diagramme Bloc
- Entrées : Joysticks, Boutons poussoirs, Boutons ON/OFF
- Microcontrôleur ESP32 : Lecture des entrées, Traitement des données, Génération des commandes
- Sorties : Écran LCD, Communication WiFi/Bluetooth
- Alimentation : Source d'alimentation

## 5. Contraintes

### 5.1 Contraintes Techniques
- Intégration et compatibilité des composants matériels avec l'ESP32
- Gestion de l'alimentation pour une utilisation optimale et durable
- Programmation en langage C/C++ avec l'IDE Arduino ou PlatformIO

### 5.2 Contraintes Fonctionnelles
- Réactivité des commandes et fluidité d'affichage sur l'écran LCD
- Fiabilité de la communication sans fil (WiFi/Bluetooth)
- Facilité d'utilisation et ergonomie de la télécommande

## 6. Étapes de Réalisation

### 6.1 Conception
- Sélection et acquisition des composants matériels
- Conception du schéma électronique

### 6.2 Développement
- Programmation du microcontrôleur ESP32
  - Lecture des entrées
  - Traitement des données
  - Gestion de l'affichage sur l'écran LCD
  - Communication sans fil (WiFi/Bluetooth)

### 6.3 Tests et Validation
- Test des fonctionnalités de chaque composant (joysticks, boutons, écran LCD)
- Validation des commandes envoyées et de la communication sans fil
- Optimisation de l'ergonomie et de la réactivité

### 6.4 Documentation
- Rédaction du manuel utilisateur
- Documentation technique détaillée

## 7. Conclusion

Ce projet vise à développer une télécommande basée sur l'ESP32, intégrant plusieurs composants matériels pour offrir un contrôle sans fil efficace et intuitif. La réussite de ce projet dépendra de la bonne intégration des composants, de la programmation efficace du microcontrôleur, et de la validation rigoureuse des fonctionnalités.

![Illustration cahier des charges](images/image6.jpeg)


Page web réalisée par Logan Desgardin, étudiant à UniLaSalle Amiens.
