# Labo 3 Nagios

## Objectif 1

On a fait la même chose que pour les derniers laboratoires.

Tout se ping parfaitement.

## Objectif 2

Tutoriel:

1. Télécharger la machine virtuel sur https://www.nagios.com/downloads/nagios-xi/vmware

2. double cliquez sur le fichier ova.

3. virtual box ouvre une page de settings, copiez les configurations suivantes.

   ![1544537591081](./img/1544537591081.png)

4. faites un import.
5. Démarrez la vm se nommant vm
6. un login localhost est demandé : 
   1. mot de passe : nagiosxi

![1544537996484](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/03_labo_nagios/img/1544537996484.png)

7. vérifiez que l'interface réseau de la machine virtuelle VirtualBox est en bridge.

![1544538543475](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/03_labo_nagios/img/1544538543475.png)

8. vous pouvez changer la langue de votre clavier en effectuant la commande suivante : `vi etc/sysconfig/keyboard` ensuite attribuez la valeur fr_CH à la variable KEYTABLE. faites `:x` pour sauver vos changements.

   1. si le fichier n'existe pas, faites `localectl set-keymap ch-fr`

9. Attribuez une adresse ip fixe à votre machine virtuelle, pour cela :

   1. Lancez la commande suivante afin d'installer l'outil permettant la configuration réseau.

   2. ```
      nmtui
      ```

      3.  allez dans Edit a connection
      4. allez dans wired connection
      5. configurez une adresse ip fixe dans IPv4 CONFIGURATION passez en manual

   ![1544541437377](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/03_labo_nagios/img/1544541437377.png)

## Objectif 3

1. Allez sur http://<<monIpNagios>>/nagiosxi/install.php

![1544541732114](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/03_labo_nagios/img/1544541732114.png)

2. Loguez vous avec votre username, password.
3. Allez sur configure => configure wizard
4. chechez network switch routeur 
5. configurez.
6. 

