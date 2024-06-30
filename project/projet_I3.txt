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

// Variables pour stocker les valeurs lues
int joystick1X, joystick1Y, joystick2X, joystick2Y;    // Variables pour stocker les valeurs des joysticks
bool button1, button2, button3, button4, buttonOnOff1, buttonOnOff2;  // Variables pour stocker l'état des boutons

// Seuil pour la détection de mouvement des joysticks
const int threshold = 512;          // Seuil pour détecter un mouvement significatif des joysticks

// Initialisation de l'écran LCD
LiquidCrystal_I2C lcd(0x27, 16, 2); // Création d'un objet lcd avec l'adresse I2C 0x27 et un écran de 16 colonnes et 2 lignes

// Initialisation du Bluetooth
BluetoothSerial SerialBT;           // Création d'un objet SerialBT pour la communication Bluetooth

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

// Fonction pour envoyer des données à l'écran LCD
void updateLCD() {
    lcd.clear();                      // Efface l'écran LCD
    lcd.setCursor(0, 0);              // Place le curseur à la première ligne, première colonne
    lcd.print("Joystick 1 X: ");      // Affiche "Joystick 1 X: "
    lcd.print(joystick1X);            // Affiche la valeur de l'axe X du joystick 1
    lcd.setCursor(0, 1);              // Place le curseur à la deuxième ligne, première colonne
    lcd.print("Joystick 1 Y: ");      // Affiche "Joystick 1 Y: "
    lcd.print(joystick1Y);            // Affiche la valeur de l'axe Y du joystick 1
    // Affichage des autres valeurs si nécessaire
}

// Fonction pour envoyer des données via Bluetooth
void sendData() {
    // Envoi des valeurs des joysticks
    SerialBT.print("Joystick1X: ");   // Envoie "Joystick1X: " via Bluetooth
    SerialBT.println(joystick1X);     // Envoie la valeur de l'axe X du joystick 1 via Bluetooth
    SerialBT.print("Joystick1Y: ");   // Envoie "Joystick1Y: " via Bluetooth
    SerialBT.println(joystick1Y);     // Envoie la valeur de l'axe Y du joystick 1 via Bluetooth
    SerialBT.print("Joystick2X: ");   // Envoie "Joystick2X: " via Bluetooth
    SerialBT.println(joystick2X);     // Envoie la valeur de l'axe X du joystick 2 via Bluetooth
    SerialBT.print("Joystick2Y: ");   // Envoie "Joystick2Y: " via Bluetooth
    SerialBT.println(joystick2Y);     // Envoie la valeur de l'axe Y du joystick 2 via Bluetooth

    // Envoi des états des boutons
    SerialBT.print("Button1: ");      // Envoie "Button1: " via Bluetooth
    SerialBT.println(button1);        // Envoie l'état du bouton 1 via Bluetooth
    SerialBT.print("Button2: ");      // Envoie "Button2: " via Bluetooth
    SerialBT.println(button2);        // Envoie l'état du bouton 2 via Bluetooth
    SerialBT.print("Button3: ");      // Envoie "Button3: " via Bluetooth
    SerialBT.println(button3);        // Envoie l'état du bouton 3 via Bluetooth
    SerialBT.print("Button4: ");      // Envoie "Button4: " via Bluetooth
    SerialBT.println(button4);        // Envoie l'état du bouton 4 via Bluetooth
    SerialBT.print("ButtonOnOff1: "); // Envoie "ButtonOnOff1: " via Bluetooth
    SerialBT.println(buttonOnOff1);   // Envoie l'état du bouton ON/OFF 1 via Bluetooth
    SerialBT.print("ButtonOnOff2: "); // Envoie "ButtonOnOff2: " via Bluetooth
    SerialBT.println(buttonOnOff2);   // Envoie l'état du bouton ON/OFF 2 via Bluetooth
}

// Fonction pour envoyer les commandes (mise à jour de l'écran LCD et envoi des données via Bluetooth)
void sendCommands() {
    updateLCD();                      // Met à jour l'écran LCD
    sendData();                       // Envoie les données via Bluetooth
}

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
