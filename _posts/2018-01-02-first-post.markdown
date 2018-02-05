---
layout: post
title:  "Liaison série"
date:  2018-01-02 21:59:00
categories: jekyll update
---

La liaison série est un moyen de transmission par interface uart, RS-232 ou USB. Contrairement à une liaison Ethernet par exemple, le série envoie bit par bit. Ils sont ensuite reçus et remis ensemble pour former un octet.

## Le protocole
Le protocole d'envoi contient donc : 

- **un bit de start** : indique le début d'un message
- **un bit de stop** : indique la fin d'un message
- **un bit de parité** : permets de vérifier l'intégrité du message et correspond au nombre de 0 ou de 1 dans le message
- **les données à envoyer** : 8 bits

On peut le visualiser de la sorte : 

|start|d0|d1|d2|d3|d4|d5|d6|d7|parité|stop|

|-----|--|--|--|--|--|--|--|--|------|----|

## La vitesse d'envoi/récéption
La vitesse d'envoi d'une liaison série s'exprime en bauds.
La convention baud étant la vitesse de transmission. Il s'agit non pas de bit par seconde mais du nombre de modulation ou de changement d'état par symboles.

En règle général, la vitesse est normalisée : 
**150, 300, 600, 1200, 2400, 9600, 19200**

## Les normes
#### RS-232
C'est une liaison asynchrone. Elle se distingue par son brochage et son niveau de tension. Elle possède un rx un tx et une masse. Le niveau logique "0" est considéré pour une tension de 3V à 25v et le niveau logique "1" pour une tension de -3V à -25V.

#### RS-485
Assez similaire au RS-232, la différence est qu'il y a un rx+ et un rx-. De même pour le tx. Cela permet d'avoir moins de parasite et de communiquer sur des câbles plus long. La connexion multipoint est ainsi gérée.

#### UART 
L'uart n'est pas une liaison en elle-même mais représente uniquement le fait de supporter une liaison série avec du rx et du tx. Il n'est pas spécifié le protocole avec le niveau de voltage.

## Lire du série sur Linux
Une liste des ports série reconnu se situe dans le dossier /dev. En réalité chaque port possède son fichier qui reflète directement le registre de réception du port. On peut donc allez lire et écrire sur le fichier comme sur le port
#### Comment trouver le nom de son port série
Tout simplement en tapant la commande 

    $ dmesg

La commande retourne l'ensemble des états des ports de l'ordinateur.
Il suffit de surveiller le branchement du bon port.

#### Les noms usuels

Il commence très souvent par "/tty" et peut se terminer par : 

- /ttyUSB* pour un connecteur USB
- /ttyAMA0 pour l'uart du raspberry pi
- /ttyACM0 pour une caméra USB
- etc...

#### Lire les informations
Après avoir isolé le nom du port, on peut s'aider d'outils tels que minicom ou miniterm. Un cat peut simplement suffire. 

La vitesse de communication est toutefois importante, sinon des caractères spéciaux peuvent apparaitre et on peut s'en prendre qu'a nous-même.
