# Labo 4 LibeNMS

Joel Schär, Yann Lederrey et Yohann Meyer



## Objectif 1: Construire le réseau et réaliser la configuration de base des équipements.

1. Connecter la machine utilisée sur le réseau Bleu.
2. Configurer la carte réseau de cette machine en mode DHCP.
3. Pour que la machine puisse recevoir des requêtes SNMP, il faut activer le service "SNMP service" et dans les propriétés, aller autoriser les requêtes avec la community string "public". 
   ![IMG_20181106_152549](./img/IMG_20181106_152549.jpg)

## Objectif 2 : Configurer la vm avec les serveur LibreNMS

1. Ouvrir la vm sur Virtualbox. (Avec VmWare il faut faire beaucoup de configuration réseau et ce n'est pas très pratique. Nos collègues en ont fait l’expérience. )
2. Configurer la carte réseau sur bridge.
3. Se connecter sur la vm avec les credentials fournis.

- username : librenms
- password: CDne3fwdfds

4. Changer le clavier vers le clavier suisse avec commande `sudo loadkeys ch`

![photo_2019-01-30_11-48-06](./img/photo_2019-01-30_11-48-06.jpg)

## Objectif 3, Monitoring d'un réseau

1. Installer python `sudo apt install python`

2. Il faut lancer le script `snmp-scan.py`sur le réseau d'ont fait partie l'ip de notre vm.
   `python3 snmp-scan.py 10.192.72.0/23`
   ![photo_2019-01-30_11-48-10](./img/photo_2019-01-30_11-48-10.jpg)

   Il faut attendre 2-3 minutes pour le scan soit terminé.

3. Accéder ensuite à l'adresse du serveur LibreNSM ( chez nous à l'adresse `10.192.72.106` ) dans un navigateur.
   Utiliser les crédentials fournis :
   - username : librenms
   - password: CDne3fwdfds

4. Aller dans l'onglet `device` pour voir le résultat du scan.

   ![photo_2019-01-30_11-48-12](./img/photo_2019-01-30_11-48-12.jpg)

#### Question 2 

1. 10.192.72.121
   1. Health

      ![photo_2019-01-30_11-48-57](./img/photo_2019-01-30_11-48-57.jpg)

   2. Ports![photo_2019-01-30_11-49-08](./img/photo_2019-01-30_11-48-17.jpg)

   3. General infos![photo_2019-01-30_11-49-01](./img/photo_2019-01-30_11-49-01.jpg)

   4. Disque usages![photo_2019-01-30_11-49-03](./img/photo_2019-01-30_11-49-03.jpg)
2. 10.192.71.92

   1. Net State![photo_2019-01-30_11-49-14](./img/photo_2019-01-30_11-49-14.jpg)
   2. Les Ports![photo_2019-01-30_11-49-08](./img/photo_2019-01-30_11-49-08.jpg)
   3. General infos![photo_2019-01-30_11-49-06](./img/photo_2019-01-30_11-49-06.jpg)
   4. Performance![photo_2019-01-30_11-49-10](./img/photo_2019-01-30_11-49-10.jpg)

## Objectif 4

#### Question 3

1. Lister la localisation des machines.

`-> Devices -> Geo Locations -> All Locations `

![photo_2019-01-30_11-49-16](./img/photo_2019-01-30_11-49-16.jpg)

2. "Health", permet de voir la santée des toutes les machines sur plusieurs points en un seul coup d'oeil.

   ![photo_2019-01-30_11-49-18](./img/photo_2019-01-30_11-49-18.jpg)

   ![photo_2019-01-30_11-49-22](./img/photo_2019-01-30_11-49-22.jpg)

3. Lister les ports de toutes les machines.
   ![photo_2019-01-30_11-49-25](./img/photo_2019-01-30_11-49-25.jpg)

4. Dashboard flexible

![photo_2019-01-30_11-49-28](./img/photo_2019-01-30_11-49-28.jpg)

#### Question 4

Nous voyons bien les possibilités que pourrait offrir LibeNMS dans le cadres de la surveillance d'un réseau. Il permet de mettre a disposition rapidement les informations et l'état de santé du réseau. Cela facilite le travail de l'ingénieur et voila.