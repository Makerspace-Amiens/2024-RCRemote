---
layout: default
nav_order: 8
title: Programmation
---

# <span style="color:#003366">_programmation_</span>

### Explication du Code pour la Programmation de la Manette Multi-Usage

Le schéma bloc fourni représente les différentes étapes de traitement et de communication de notre manette multi-usage, utilisant un microcontrôleur ESP32. Voici une explication détaillée du fonctionnement du code associé à chaque bloc :

#### Bloc 1 : Entrée
Ce bloc regroupe les dispositifs d'entrée, incluant :
- **Joystick 1**
- **Joystick 2**
- **Boutons poussoirs (4)**
- **Boutons ON / OFF (2)**

#### Bloc 2 : Traitement (ESP32)
Le microcontrôleur ESP32 est le cœur du système, chargé de lire les entrées, traiter les données et envoyer des commandes de contrôle. Ce bloc est divisé en trois sous-parties :

1. **Lecture des Entrées**
   - **Lecture Joystick 1 & 2** : Le code lit les valeurs des deux joysticks, qui sont généralement des signaux analogiques convertis en valeurs numériques par l'ESP32.
   - **Lecture Boutons poussoirs (4)** : Le code surveille les états des quatre boutons poussoirs, qui sont des entrées numériques.
   - **Lecture Boutons ON / OFF (2)** : De la même manière, les boutons ON / OFF sont surveillés pour détecter leur état (haut/bas).

   ```
   int joystick1X = analogRead(pinJoystick1X);
   int joystick1Y = analogRead(pinJoystick1Y);
   int joystick2X = analogRead(pinJoystick2X);
   int joystick2Y = analogRead(pinJoystick2Y);
   bool button1 = digitalRead(pinButton1);
   bool button2 = digitalRead(pinButton2);
   bool button3 = digitalRead(pinButton3);
   bool button4 = digitalRead(pinButton4);
   bool buttonOnOff1 = digitalRead(pinOnOff1);
   bool buttonOnOff2 = digitalRead(pinOnOff2);
   ```

2. **Traitement des Données**
   - **Traitement Joysticks** : Les valeurs des joysticks sont traitées pour déterminer la direction et l'intensité des mouvements.
   - **Traitement Boutons** : Les états des boutons sont interprétés pour déterminer quelles actions doivent être déclenchées.

   ```
   void processInputs() {
       // Traitement des données des joysticks
       if (joystick1X > threshold) {
           // Action correspondante au mouvement du joystick 1 à droite
       }
       if (joystick1Y > threshold) {
           // Action correspondante au mouvement du joystick 1 vers le haut
       }
       // Traitement similaire pour joystick 2 et boutons
   }
   ```

3. **Commandes de Contrôle**
   - **Commande vers Écran LCD** : Les informations traitées sont envoyées à l'écran LCD pour affichage.
   - **Commande vers Communication (WiFi/Bluetooth)** : Les données peuvent également être envoyées via WiFi ou Bluetooth pour une utilisation externe.

   ```
   void sendCommands() {
       // Commande vers l'écran LCD
       lcd.print("Joystick 1 X: ");
       lcd.print(joystick1X);
       // Commande pour la communication
       wifiSendData(joystick1X, joystick1Y, ...);
   }
   ```

#### Bloc 3 : Sortie
Ce bloc traite les dispositifs de sortie :
- **Écran LCD** : Affiche les informations relatives aux entrées et aux traitements.
- **Communication (WiFi/Bluetooth)** : Permet la communication des données traitées vers d'autres appareils ou systèmes.

#### Bloc 4 : Alimentation
Ce bloc assure l'alimentation des composants :
- **Source d’alimentation** : Fournit l'énergie nécessaire à tous les composants du système.
- **Régulateur de tension (si nécessaire)** : Stabilise la tension d'alimentation pour garantir un fonctionnement optimal des composants.

### Fonctionnement du Code Global
Le code de notre manette multi-usage suit une structure de boucle principale qui s'exécute en continu pour lire les entrées, traiter les données et envoyer les commandes appropriées. Voici un pseudocode simplifié illustrant ce fonctionnement :

```
void setup() {
    // Initialisation des pins et des périphériques (LCD, WiFi, etc.)
    initPins();
    initLCD();
    initWiFi();
}

void loop() {
    // Lecture des entrées
    readInputs();
    
    // Traitement des données
    processInputs();
    
    // Envoi des commandes de contrôle
    sendCommands();
    
    // Petite pause pour éviter une surcharge du processeur
    delay(10);
}
```

### Conclusion
Le code de notre manette multi-usage est structuré pour lire les entrées des différents dispositifs (joysticks et boutons), traiter ces données pour déterminer les actions appropriées, et envoyer des commandes aux dispositifs de sortie (écran LCD et modules de communication). Grâce à cette structure modulaire, notre manette peut être facilement adaptée à diverses applications, qu'il s'agisse de jeux, de contrôle de robots ou d'autres systèmes interactifs.
