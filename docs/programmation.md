---
layout: default
nav_order: 8
title: Programmation
---

# <span style="color:#003366">_Programmation_</span>

# <span style="color:#DB1702">_IDE Arduino_</span>

Pour programmer mon microprocesseur ESP32, j'ai opté pour l'utilisation de l'IDE Arduino. J'ai choisi cette application parce que je l'ai déjà utilisée auparavant et qu'elle est réputée pour sa simplicité d'utilisation. 

Pour vous expliquer globalement le processus, voici les étapes que j'ai suivies :

- _**Écriture du code**_ : J'ai rédigé mon code dans l'éditeur intégré de l'IDE Arduino, qui est spécifiquement conçu pour le développement de projets basés sur des microcontrôleurs comme l'ESP32.

- _**Compilation du code**_ : Une fois le code écrit, je l'ai compilé à l'aide de l'outil de compilation intégré. Cette étape est cruciale car elle permet de vérifier si le code comporte des erreurs de syntaxe ou de logique.

- _**Détection des erreurs**_ : Si des erreurs sont présentes dans le code, l'IDE Arduino fournit des messages d'erreur détaillés qui indiquent précisément où ces erreurs se trouvent. Cela permet de corriger rapidement les problèmes identifiés.

- _**Vérification avant l'injection**_ : L'un des avantages majeurs de l'IDE Arduino est qu'il permet de vérifier et de déboguer le code avant de l'injecter dans le microprocesseur ESP32. Cette étape de pré-injection garantit que le code fonctionnera comme prévu une fois transféré sur le matériel.

![Illustration presentation](images/arduino.png)

# <span style="color:#003366">_Explication du Fonctionnement du Code de la Manette Multi-Usage a l'aide d'un schéma bloc_</span>

Pour vous expliquer le fonctionnement de mon code, j'ai décidé de vous fournir une explication illustrée à l'aide d'un schéma en blocs. Ce schéma permettra de visualiser de manière claire et structurée le mécanisme de mon code, facilitant ainsi la compréhension de son fonctionnement global. 

Pour ceux qui sont plus à l'aise techniquement, j'ai également inclus, après le schéma en blocs, des extraits de mon code. Chaque extrait est accompagné d'explications détaillées pour décrire précisément le rôle de chaque segment de code, les logiques appliquées, et les interactions entre les différentes parties. 

Cette approche vous permettra de comprendre non seulement l'architecture générale du code, mais aussi les détails techniques qui le composent, rendant ainsi l'ensemble du processus transparent et accessible à différents niveaux de compétence.

![Illustration presentation](images/arduino1.png)

# <span style="color:#DB1702">_Explication Détaillée du Fonctionnement du Code de la Manette Multi-Usage_</span>

Pour mieux comprendre le fonctionnement du code de notre manette multi-usage, nous allons approfondir chaque étape de la programmation en suivant les blocs décrits dans le schéma.

Voici comment je diviserais le code en 5 grandes parties selon les différentes fonctionnalités :

## Partie 1: Inclusions de bibliothèques et déclarations de constantes
Cette partie comprend les inclusions de bibliothèques nécessaires et les déclarations des pins pour les entrées.

```cpp
#include <Arduino.h>                // Inclusion de la bibliothèque de base Arduino
#include <Wire.h>                   // Inclusion de la bibliothèque Wire pour la communication I2C
#include <LiquidCrystal_I2C.h>      // Inclusion de la bibliothèque LiquidCrystal_I2C pour l'écran LCD
#include <BluetoothSerial.h>        // Inclusion de la bibliothèque BluetoothSerial pour la communication Bluetooth

// Déclaration des pins pour les entrées
const int pinJoystick1X = 36;       // Pin pour l'axe X du joystick 1
const int pinJoystick1Y = 39;       // Pin pour l'axe Y du joystick 1
const int pinJoystick2X = 34;       // Pin pour l'axe X du joystick 2
const int pinJoystick2Y = 35;       // Pin pour l'axe Y du joystick 2
const int pinButton1 = 13;          // Pin pour le bouton poussoir 1
const int pinButton2 = 12;          // Pin pour le bouton poussoir 2
const int pinButton3 = 14;          // Pin pour le bouton poussoir 3
const int pinButton4 = 27;          // Pin pour le bouton poussoir 4
const int pinOnOff1 = 26;           // Pin pour le bouton ON/OFF 1
const int pinOnOff2 = 25;           // Pin pour le bouton ON/OFF 2
```

## Partie 2: Initialisation des périphériques et des objets
Cette partie comprend l'initialisation de l'écran LCD et de la communication Bluetooth, ainsi que la configuration des pins.

```cpp
// Initialisation de l'écran LCD
LiquidCrystal_I2C lcd(0x27, 16, 2); // Création d'un objet lcd avec l'adresse I2C 0x27 et un écran de 16 colonnes et 2 lignes

// Initialisation du Bluetooth
BluetoothSerial SerialBT;           // Création d'un objet SerialBT pour la communication Bluetooth

// Fonction d'initialisation
void setup() {
    // Initialisation des pins et des périphériques (LCD, Bluetooth, etc.)
    pinMode(pinJoystick1X, INPUT);        // Configure la pin de l'axe X du joystick 1 en entrée
    pinMode(pinJoystick1Y, INPUT);        // Configure la pin de l'axe Y du joystick 1 en entrée
    pinMode(pinJoystick2X, INPUT);        // Configure la pin de l'axe X du joystick 2 en entrée
    pinMode(pinJoystick2Y, INPUT);        // Configure la pin de l'axe Y du joystick 2 en entrée
    pinMode(pinButton1, INPUT_PULLUP);    // Configure la pin du bouton 1 en entrée avec résistance de pull-up interne
    pinMode(pinButton2, INPUT_PULLUP);    // Configure la pin du bouton 2 en entrée avec résistance de pull-up interne
    pinMode(pinButton3, INPUT_PULLUP);    // Configure la pin du bouton 3 en entrée avec résistance de pull-up interne
    pinMode(pinButton4, INPUT_PULLUP);    // Configure la pin du bouton 4 en entrée avec résistance de pull-up interne
    pinMode(pinOnOff1, INPUT_PULLUP);     // Configure la pin du bouton ON/OFF 1 en entrée avec résistance de pull-up interne
    pinMode(pinOnOff2, INPUT_PULLUP);     // Configure la pin du bouton ON/OFF 2 en entrée avec résistance de pull-up interne

    // Initialisation de l'écran LCD
    lcd.init();                           // Initialise l'écran LCD
    lcd.backlight();                      // Allume le rétroéclairage de l'écran LCD

    // Initialisation de la communication Bluetooth
    SerialBT.begin("ESP32_Controller");   // Démarre la communication Bluetooth avec le nom "ESP32_Controller"
}
```

## Partie 3: Lecture des Entrées
Cette partie contient la fonction pour lire les valeurs des joysticks et des boutons.

```cpp
// Fonction pour lire les entrées
void readInputs() {
    joystick1X = analogRead(pinJoystick1X);         // Lecture de l'axe X du joystick 1
    joystick1Y = analogRead(pinJoystick1Y);         // Lecture de l'axe Y du joystick 1
    joystick2X = analogRead(pinJoystick2X);         // Lecture de l'axe X du joystick 2
    joystick2Y = analogRead(pinJoystick2Y);         // Lecture de l'axe Y du joystick 2
    button1 = digitalRead(pinButton1) == LOW;       // Lecture de l'état du bouton 1
    button2 = digitalRead(pinButton2) == LOW;       // Lecture de l'état du bouton 2
    button3 = digitalRead(pinButton3) == LOW;       // Lecture de l'état du bouton 3
    button4 = digitalRead(pinButton4) == LOW;       // Lecture de l'état du bouton 4
    buttonOnOff1 = digitalRead(pinOnOff1) == LOW;   // Lecture de l'état du bouton ON/OFF 1
    buttonOnOff2 = digitalRead(pinOnOff2) == LOW;   // Lecture de l'état du bouton ON/OFF 2
}
```

## Partie 4: Traitement des Données
Cette partie contient la fonction pour traiter les valeurs lues des joysticks et des boutons.

```cpp
// Fonction pour traiter les entrées
void processInputs() {
    // Traitement des joysticks
    if (joystick1X > threshold) {
        // Action correspondante au mouvement du joystick 1 vers la droite
        SerialBT.println("Joystick 1 droite");
    } else if (joystick1X < -threshold) {
        // Action correspondante au mouvement du joystick 1 vers la gauche
        SerialBT.println("Joystick 1 gauche");
    }

    if (joystick1Y > threshold) {
        // Action correspondante au mouvement du joystick 1 vers le haut
        SerialBT.println("Joystick 1 haut");
    } else if (joystick1Y < -threshold) {
        // Action correspondante au mouvement du joystick 1 vers le bas
        SerialBT.println("Joystick 1 bas");
    }

    // Traitement similaire pour joystick 2
    if (joystick2X > threshold) {
        // Action correspondante au mouvement du joystick 2 vers la droite
        SerialBT.println("Joystick 2 droite");
    } else if (joystick2X < -threshold) {
        SerialBT.println("Joystick 2 gauche");
    }

    if (joystick2Y > threshold) {
        // Action correspondante au mouvement du joystick 2 vers le haut
        SerialBT.println("Joystick 2 haut");
    } else if (joystick2Y < -threshold) {
        SerialBT.println("Joystick 2 bas");
    }

    // Traitement des boutons poussoirs
    if (button1) {
        SerialBT.println("Bouton 1 appuyé");
    }
    if (button2) {
        SerialBT.println("Bouton 2 appuyé");
    }
    if (button3) {
        SerialBT.println("Bouton 3 appuyé");
    }
    if (button4) {
        SerialBT.println("Bouton 4 appuyé");
    }

    // Traitement des boutons ON/OFF
    if (buttonOnOff1) {
        SerialBT.println("Bouton ON/OFF 1 activé");
    }
    if (buttonOnOff2) {
        SerialBT.println("Bouton ON/OFF 2 activé");
    }
}
```

## Partie 5: Boucle Principale
Cette partie contient la boucle principale du programme qui appelle les fonctions pour lire les entrées, traiter les données et envoyer les commandes.

```cpp
// Boucle principale
void loop() {
    // Lecture des entrées
    readInputs();                         // Lit les valeurs des joysticks et des boutons
    
    // Traitement des données
    processInputs();                      // Traite les valeurs lues
    
    // Envoi des commandes de contrôle
    sendCommands();                       // Met à jour l'écran LCD et envoie les données via Bluetooth
    
    // Petite pause pour éviter une surcharge du processeur
    delay(10);                            // Attente de 10 millisecondes
}
```

Chaque partie est maintenant clairement divisée selon sa fonctionnalité dans le programme Arduino.

## Illustration

Mon code compile correctement dans l'IDE Arduino sans afficher aucun message d'erreur, ce qui démontre sa compatibilité. De plus, je peux le simuler sur Wokwi pour illustrer ses capacités et fonctionnalités.

![Illustration programmation ](images/arduino.png)

### Conclusion

Notre code pour la manette multi-usage est conçu pour être modulaire et extensible, adapté à diverses applications grâce à une liaison Bluetooth intégrée et à des fonctionnalités bien définies. Chaque étape de la boucle principale (lecture des entrées, traitement des données, envoi des commandes) est clairement définie et peut être ajustée ou étendue selon les besoins spécifiques du projet. Cette structure permet une adaptation aisée de notre manette à différents contextes, que ce soit pour des jeux, le contrôle de robots, ou d'autres systèmes interactifs.



Page web réalisée par Logan DESGARDIN , étudiant à UniLaSalle Amiens.
