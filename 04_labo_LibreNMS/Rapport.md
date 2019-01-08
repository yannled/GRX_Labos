# Labo 4 LibeNMS



## configurer la vm

Ouvrir la vm sur Virtual box sinon  il faut faire beaucoup de configuration réseau et ce n'est pas très pratique.

Se connecter sur la vm avec les credentials fournis.

Changer le clavier avec commande `sudo loadkeys ch`



## Objectif 3

il faut lancer le script `snmp-scan.py`sur le réseau de l'ip de notre vm.

`python3 snmp-scan.py 10.192.72.0/23`



Aller sur l'adresse `10.192.72.106` dans un navigateur.

Entrer le mot de passe fourni.



Aller dans l'onglet `device`.

#### Question 2 

1. 10.192.72.121
   1. Health
   2. Ports
   3. General infos
   4. Disque usages
2. 10.192.71.92
   1. Net State
   2. Ports
   3. General infos
   4. Performance

## Objectif 4

#### Question 3

1. Lister la localisation des machines.

`-> Devices -> Geo Locations -> All Locations `

2. Health permet de voir la santée des toutes les machines sur plusieurs points en un seul coup d'oeil.
3. Lister les ports de toutes les machines.
4. Dashboard flexible



#### Question 4

Nous voyons bien les possibilités que pourrait offrir LibeNMS dans le cadres de la surveillance d'un réseau. Il permet de mettre a disposition rapidement les informations et l'état de santé du réseau. Cela facilite le travail de l'ingénieur et voila.