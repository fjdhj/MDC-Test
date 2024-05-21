# Comment utiliser le serveur NGINX avec PHP pour tester le site MDC?


Pour initialiser le site (sous module git)
```
git submodule update --init
```


Pour installer et/ou démarrer le serveur utiliser la commande :
```
Classique
docker compose up


Mode demon
docker compose up -d
```
Le mode demon a pour intérêt de tourner en arrière plan.


Autre commande docker utile :
```
Voir les containers:
docker ps [-a]
```


Le serveur a pour racine le dossier myDoorCenter, il est situé au même niveau que le fichier docker-compose.yml.
En suivant les étapes, ce dossier devrait contenir le dépôt git ImadIsMad/myDoorCenter en tant que "submodule".


Un sous-module étant un projet git classique, toutes les commandes de git sont disponibles et fonctionneront normalement pour le projet ImadIsMad/myDoorCenter en vous plaçant dans le dossier myDoorCenter


Pour travailler sur le projet myDoorCenter, démarrer le serveur a l'aide de la commande plus haut et ouvrez votre le dossier myDoorCenter avec votre IDE.


# Interaction avec la BDD
La Base De Données (BDD) est accessible différemment en fonction de la source :
### Accès depuis l'hôte (par exemple MySQLWorbench)
L'adresse de connexion est au choix :
- localhost:4306
- localhost:43060


Par défaut, la BDD est créée avec comme unique utilisateur :
|Utilisateur|Mot de Passe|
|-|-|
|root|rootPassword|


Il est recommandé d'initialiser la BDD avec les scripts fournis pas le projet MyDoorCenter avant de faire des tests.


### Accès depuis un conteneur (par exemple le serveur web)
L'adresse de connexion est :
- db


La connexion peut se faire avec l'utilisateur root, mais il est recommandé d'utiliser un autre utilisateur pour faire ça. Exemple de configuration disponible après avoir exécuté les scripts SQL qui créent l'utilisateur TestDB:
```
Fichier : BDD/config.php


<?php
const SQL_SERVER="db";
const SQL_USER="TestBDD";
const SQL_PASSWORD="";
const SQL_BDD_NAME="DW";
?>
```


# Impossible de démarrer le serveur :
- Vérifiez qu'un autre serveur web n'est pas déjà en execution et si c'est le cas, arrêtez-le. Exemple avec Apache2
```
Vérifier si Apache 2 est lancé :
systemctl status apache2.service


Arrêter Apache 2:
sudo systemctl stop apache2.service
```

