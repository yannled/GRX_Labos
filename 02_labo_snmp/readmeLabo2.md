



# Laboratoire SNMP

Joel Schär, Yann Lederrey, Yohann Meyer



## Objectif 1 : Construire le réseau et réaliser la configuration de base des équipements



### Configuration des machines

Il faut relier les équipements comme indiqué sur le schéma ci dessous. 
Les liaisons entre l'armoire de brassage et les machines Windows était le **B05LL09** et le **B05LL10**. Le schéma réseau ci dessous, illustre le montage réseau utilisé.

![](/home/joel/Switchdrive/HEIG/S-5/GRX/Labos/GRX_Labos_repo_git/02_labo_snmp/img/schema_resau.jpg)

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



## Objectif 2 : Configurer un *SNMP Manager*

1. Vérification que le localhost existe déjà (Vérifier que le community string est bien public)

![IMG_20181106_151642](./img/IMG_20181106_151642.jpg)



## Objectif 3 : Configurer différents agents SNMP

2. **Activez l'agent SNMP sur le DELL 9010, laissez le *community string* en mode Read Only avec la valeur public**

![IMG_20181106_151642](./img/IMG_20181106_152549.jpg)

3. **A l'aide du browser snmpb, interrogez le localhost :**
   - le nom du pc : PC10BB05

![IMG_20181106_151642](./img/IMG_20181106_152921.jpg)

- la decription système hardware et software

![IMG_20181106_151642](./img/IMG_20181106_153007.jpg)

- le OID système

![IMG_20181106_151642](./img/IMG_20181106_153016.jpg)

- l'UPtime du système

![IMG_20181106_151642](./img/IMG_20181106_153024.jpg)

- le contact et la localisation malheuresement vide les deux.

![IMG_20181106_151642](./img/IMG_20181106_153032.jpg)

![IMG_20181106_151642](./img/IMG_20181106_153045.jpg)

- Activez et configurez l'agent SNMP sur le DELL 9020, laissez community string en mode Read Only et public pour publicD9020.

![IMG_20181106_151642](./img/IMG_20181106_153606.jpg)

![IMG_20181106_151642](./img/IMG_20181106_153648.jpg)

4. **Que faut-il changer sur le DELL 9010 pour que ce dernier soit capable d'interroger l'agent SNMP du Dell 9020 ? **
   - Il faut ajouter un profile pour le dell 9020
   - Il faut définir la Community string.

![IMG_20181106_151642](./img/IMG_20181106_154249.jpg)

5. **A l'aide du browser snmpb, interrogez le DELL 9020 et determinez le nom de l'équipement, le nom du responsable de l'équipement, son nombre d'interfaces et le traffic de chacunes des interfaces.**
   - on retrouve : 
     - le nom de l'équipement : PC10CB05

![IMG_20181106_151642](./img/IMG_20181106_154116.jpg)

- la personne de contact, responsable (vide)

![IMG_20181106_151642](./img/IMG_20181106_154133.jpg)

- le nombre d'interface, 35

![IMG_20181106_151642](./img/IMG_20181106_154328.jpg)

- le trafic de chacune des interfaces.

![IMG_20181106_151642](./img/IMG_20181106_154841.jpg)

6. **A l'aide de Wireshark, capturez et présentez les trames lorsque le DELL 9010 demande le nom de l'equipement du DELL 9020. Commentez !**
   - On peut voir sur les screens suivants, que le 9010 fait un get avec L'OID 1.3.6.1.2.1.1.5.0 afin de connaitre le nom de l'équipement.
   - Dans la réponse on peut voir : variable-binding-string: PC10CB05

![IMG_20181106_151642](./img/IMG_20181106_155117.jpg)

![IMG_20181106_151642](./img/IMG_20181106_155131.jpg)

- Configuration du routeur cisco de manière à pouvoir le gérer via SNMPv2.

![IMG_20181106_151642](./img/IMG_20181106_155624.jpg)

![IMG_20181106_151642](./img/IMG_20181106_155750.jpg)

- Configurez le routeur pour qu'il envoie les traps : 

![IMG_20181106_151642](./img/IMG_20181106_160459.jpg)

![IMG_20181106_151642](./img/IMG_20181106_160504.jpg)

- Créez un nouveau profile dans snmpb pour le routeur :

![IMG_20181106_151642](./img/IMG_20181106_160249.jpg)

- Testez que le manager SNMP peut interroger l'agent SNMP du routeur cisco.

![IMG_20181106_151642](./img/IMG_20181106_160356.jpg)

- Trouvez un moyen de changer le nom du routeur depuis le PC Dell 9010 via SNMP

![IMG_20181106_151642](./img/IMG_20181106_161840.jpg)

- Changez le nom du routeur R1, capturez les trames échangées, ici on a nommé le routeur "coucou".

![IMG_20181106_151642](./img/IMG_20181106_162126.jpg)

![IMG_20181106_151642](./img/IMG_20181106_162136.jpg)

7. **Que pouvez vous dire sur la sécurité du protocole SNMPv2, citez deux moyens d'améliorer la sécurité de notre infrasctructure.**
   - Restreindre la possibilité des requête sur nos équipement, client SNMP afin d'éviter que tous les éléments réseaux puisse effectuer la requête.
   - Chiffrer les requêtes afin d'éviter qu'elle transitent en clair.

- Tout en capturant le trafic réseau, faites un copy run start sur le routeur, vérifiez que vous capturez les traps SNMP.

![IMG_20181106_151642](./img/IMG_20181106_162429.jpg)

8. **Analyez les trames de la capture précédente et décodez la signification des différentes trames SNMP via son OID code.**

   - Malheureusement même avec l'aide de l'assistant nous n'avons pas réussis à retrouver la signification du OID 1.3.6.1.4.1.9.9.43.1.1.6.1.3.10. Nous avons quand même un screen pour prouver que nous avons effectué la recherche.

   ![IMG_20181106_151642](./img/IMG_20181106_164754.jpg)



9. **Quelles commandes supplémentaires faut-il mettre en oeuvre sur le routeur Cisco si on souhaite restreindre l'accès des requêtes à certains hosts.**
   - Pour faire cela nous utilisons la commande : `access-list l permit 102.168.1.3`

![IMG_20181106_151642](./img/IMG_20181106_163219.jpg)

- Configurez le deuxième équipement Cisco (switch) afin de pouvoir l'interroger sur notre manager SNMP.

  Entrez les commandes suivantes dans le terminal du switch

![IMG_20181106_151642](./img/IMG_20181106_163626.jpg)

Une fois le switch configuré, celui-ci en maintenant accessible de puis SNMPb

![IMG_20181106_151642](./img/IMG_20181106_164024.jpg)

