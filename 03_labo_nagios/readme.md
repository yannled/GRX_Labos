# Labo 3 Nagios

Joel Schär, Yann Lederrey, Yohann Meyer

## Objectif 1

On a fait la même chose que pour les derniers laboratoires.

### Extrait du laboratoire SNMP

### Configuration des machines

Il faut relier les équipements comme indiqué sur le schéma ci dessous. 
Les liaisons entre l'armoire de brassage et les machines Windows était le **B05LL09** et le **B05LL10**. Le schéma réseau ci dessous, illustre le montage réseau utilisé.

![schema_resau.jpg](./img/schema_resau.jpg)

Il faut ensuite configurer les machines en leur attribuant les adresses ip indiquées dans le tableau ci- dessous.

| Équipement |     OS      | Interface | Adresse IP  | Masque de sous-réseau | Passerelle par défaut |
| :--------- | :---------: | --------- | :---------: | :-------------------: | :-------------------: |
| R1         |    CISCO    | 0 / 1     | 192.168.3.1 |     255.255.255.0     |      192.168.3.1      |
| R1         |    CISCO    | 0 /0      | 192.168.1.1 |     255.255.255.0     |      192.168.1.1      |
| S1         |    CISCO    | 21        | 192.168.1.2 |     255.255.255.0     |      192.168.1.1      |
| S1         |    CISCO    | 23        | 192.168.1.2 |     255.255.255.0     |      192.168.1.1      |
| Dell 9010  |   Win 10    | NIC       | 192.168.1.3 |     255.255.255.0     |      192.168.1.1      |
| Dell 9010  | Ubuntu (VM) | NIC       | 192.168.1.4 |     255.255.255.0     |      192.168.1.1      |
| Dell 9020  |   Win 10    | NIC       | 192.168.3.3 |     255.255.255.0     |      192.168.3.1      |

Pour ce qui est des machines Windows, il faut faire la configuration dans les paramètres réseau dédiée et reliée au montage.

Pour la machine virtuelle Ubuntu, il est nécessaire de régler la carte réseau en mode **Bridged Networking** dans les paramètres de configuration VMware et d'associer la carte virtuelle avec la carte physique correspondante. Définir ensuite les paramètres Ip dans les réglage réseau de la machine Linux.

Pour la configuration du router cisco il faut entrer les commandes suivantes dans le terminal.

```
> enable
> configure terminal
> interface GigabitEthernet 0/0
> ip address 192.168.1.1 255.255.255.0
> no shutdown
> exit
> interaface GigabitEthernet 0/1
> ip address 192.168.3.1 255.255.255.0
> no shutdown
> exit
> exit
> exit
```

Pour attribuer une adresse Ip au switch il faut entrer les commandes suivantes dans le terminal.

```
> enable
> configure terminal
> interface vlan1
> ip address 192.168.1.2 255.255.255.0
> no shutdown
> exit
> ip default-gateway 192.168.1.1
> exit
> exit
```



On obtient en finalité un réseau dans lequel toutes les machines peuvent être pingée entre elles.

## Objectif 2

Tutoriel:

1. Télécharger la machine virtuel sur https://www.nagios.com/downloads/nagios-xi/vmware

2. double cliquez sur le fichier ova.

3. virtual box ouvre une page de settings, copiez les configurations suivantes.

   ![1544537591081](./img/1544537591081.png)

4. faites un import.
5. Démarrez la vm se nommant "vm"
6. un login localhost est demandé : 

   1. mot de passe : nagiosxi

![1544537996484](./img/1544537996484.png)

7. vérifiez que l'interface réseau de la machine virtuelle VirtualBox est en bridge.

![1544538543475](./img/1544538543475.png)

8. vous pouvez changer la langue de votre clavier en effectuant la commande suivante : 
   `vi etc/sysconfig/keyboard` , ensuite attribuez la valeur "fr_CH" à la variable "KEYTABLE". faites `:wx` pour sauver vos changements.

   1. si le fichier n'existe pas, faites `localectl set-keymap ch-fr`

9. Attribuez une adresse ip fixe à votre machine virtuelle, pour cela :

   1. Lancez la commande suivante afin d'installer l'outil permettant la configuration réseau.

   2. ```
      nmtui
      ```

      3.  allez dans Edit a connection
      4. allez dans wired connection
      5. configurez une adresse ip fixe dans IPv4 CONFIGURATION passez en manual

   ![1544541437377](./img/1544541437377.png)

## Objectif 3

1. Allez sur http://<<monIpNagios>>/nagiosxi/install.php

![1544541732114](./img/1544541732114.png)

(mot de passe changé -> "admin")

2. Loguez vous avec votre username, password.

3. Allez sur configure => configure wizard

4. chechez network switch routeur 

5. configurez.

6. choisir l'ip de du router

   ![photo_2018-12-18_16-20-50](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-50.jpg)

   ![photo_2018-12-18_16-20-48](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-48.jpg)


   ![photo_2018-12-18_16-20-43](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-43.jpg)

7. On fait la même manipe pour le switch

   ![photo_2018-12-18_16-20-36](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-36.jpg)

   ![photo_2018-12-18_16-20-34](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-34.jpg)
   ![photo_2018-12-18_16-20-41](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-41.jpg)

8. On fait la même manipe pour le Dell 9020

   Pour ce faire on va utiliser "windows SNMP"
   Il faut installer un agent disponible en téléchargement depuis la console de nagios.
   ![photo_2018-12-18_16-20-57](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-57.jpg)



On peut maintenant voir les différents hosts dans la consôle.

![photo_2018-12-18_16-20-27](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-27.jpg)

![photo_2018-12-18_16-20-20](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-20.jpg)

#### Question 3

Deux moyens possible pour faire la découverte des hôtes est d'utiliser SNMP ou de faire un simple ping vers toutes les adresses IP.

## Objectif 4

Pour l'auto découverte de la machine windows.

![photo_2018-12-18_16-21-00](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-21-00.jpg)

![photo_2018-12-18_16-21-12](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-21-12.jpg)



![photo_2018-12-18_16-21-05](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-21-05.jpg)



Une fois toutes la configuration faites, nous ne pouvions tout de même pas avoir accès aux données de la machine. Nous avons donc refait la configuration manuellement avec "windwos SNMP".

![photo_2018-12-18_16-20-57](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-20-57.jpg)



#### Question 4

Il est possible de monitorer les services suivant.

![photo_2018-12-18_16-21-25](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-21-25.jpg)



#### Quesiton 5 - 6

Après avoir changé le réseau du serveur nagios sur le réseau de l'école est remis la carte réseau en mode DHCP. On peut faire une découverte de tous les devices du réseau.

![photo_2018-12-18_16-44-51](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-44-51.jpg)

![photo_2018-12-18_16-44-48](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-44-48.jpg)


![photo_2018-12-18_16-44-44](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/03_labo_nagios/img/photo_2018-12-18_16-44-44.jpg)



Vu que les services sont bloqués sur le réseau de l'école, nous ne pouvons pas identifier les services tournant sur les machines détectées. Nous pouvons tout de même supposer le rôle des serveurs :

- DHCP
- code check
- téléinfo

## Objectif 5

- La supervision réseau (SMTP, POP3, HTTP, NNTP, PING)
- La supervision de ressources systèmes (charge processeur, état de disques, nombre d'utilisateurs connectés, process)
- La supervision d'applications.
- La notification par différents moyens de communications (SMS, mail, wap)
- L' exécution de commandes manuelles ou automatiques
- La représentation des états de ressources supervisées, par coloration.
- La cartographie du système d'information supervisé
- Le reporting