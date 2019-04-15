# CanGateway_ESP8266
Passerelle CAN/WiFI/Serial sur ESP8266

Cette passerelle permet d'interconnecter un bus CAN avec un réseau en Ethernet et/ou WiFi mais également en utilisant le port série de l'ESP8266.

Ce projet est compatible avec la norme CAN V2.0B et permet d'utiliser des identifiants standards à 11 bits ou étendus à 29 bits.

La bibliothèque utilisée est CAN_BUS_Shield de Seeed-Studio mais modifiée par Locoduino et disponible ici : https://github.com/Locoduino/CAN_BUS_Shield

Le projet est encore en cours de développement mais néanmoins opérationnel.

Un schéma de câblage avec un module NiRen est disponible ici : http://www.locoduino.org/local/cache-vignettes/L438xH1000/nodemcu_niren-4b03c.jpg?1552261120

Le dossier data contient une application HTML/JavaScript de démo et doit être copié dans la mémoire SPIFF de l'ESP.

Les réglages sont à faire dans le fichier « Config.h » en renseignant l’identifiant de votre réseau (SSID) et le mot de passe (PSW)

// WIFI
#define WIFI_SSID          "your_SSID"
#define WIFI_PSW           "your_PSW"

Le mapping des pins avec un controleur CAN est renseigné également dans ce fichier :

/* PINS:  CS=D0, INT=D4, SCK=D5, SO=D6, SI=D7 */
#define CAN_CSPIN              16   // Set CS to pin 16 (D0)
#define CAN_INTERPIN            2   // Set INT to pin 2 (D4)

#define CAN_BAUDRATE           18

Un debug peut être affiché en utilisant le port Serial1 de l’ESP dont le TX est disponible sur la pin D4.

#define DBG_OUTPUT           Serial1    // Debug sur le port Serial1 sur GPIO2 (D4)

Vous pouvez modifier « #define DBG_OUTPUT Serial » pour afficher le debug sur le moniteur série relié au port USB de l’ESP8266.

Le programme est configuré pour pouvoir fournir une adresse DNS qui est cangw (modifiable).

#define HOST                 "cangw"

Après lancement du programme, l’application est normalement disponible à l’adresse : http://cangw/satellite.html

En cas de problème avec l’adresse DNS, l’adresse IP du serveur s’affiche dans le moniteur du debug :

Serial port ok !
Wifi connecting to AP....
Wifi connection established !
IP address :.....192.168.86.38
Netmask :........255.255.255.0
Gateway :........192.168.86.1
Mac adress :.....84:F3:EB:18:76:2C
DNS :............http://cangw/

Ici,192.168.86.38. L’application devra alors être appelée sur l’URL : http://192.168.86.38/satellite.html

En manipulant les boutons et sliders, les informations de positions sont envoyées en temps réel et seront visibles dans la fenêtre du moniteur sous cette forme :

Wifi [0] get Text: 0x1FFFFF21 1 3 0x1 0x12 0x73

Il s’agit ici d’un message CAN avec un identifiant sur 11 bits (0x1FFFFF21) avec 3 octets de données (0x1 0x12 0x73).

Notez que ce même message : 0x1FFFFF21 1 3 0x1 0x12 0x73 pourrait être directement saisie dans une application gérant des communications	série ou plus simplement dans la zone de saisie de la fenêtre moniteur de l’IDE Arduino si vous utilisez cette application.


