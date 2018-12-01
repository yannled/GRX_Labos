# Laboratoire SNMP

Joel Schar, Yann Lederrey, Yohann Meyer



## Objectif 1 : Construire le réseau et réaliser la configuration de base des équipements



## Objectif 2 : Configurer un *SNMP Manager*

1. Vérification que le localhost existe déjà (Vérifier que le community string est bien public)

![IMG_20181106_151642](./img/IMG_20181106_151642.jpg)

## Objectif 3 : Configurer différents agents SNMP

1. Activer l'agent SNMP sur le DELL 9010, laissez le *community string* en mode Read Only avec la valeur public

![IMG_20181106_151642](./img/IMG_20181106_152549.jpg)

2. A l'aide du browser snmpb, interrogez le localhost :

![IMG_20181106_151642](./img/IMG_20181106_152921.jpg)

![IMG_20181106_151642](./img/IMG_20181106_153007.jpg)

![IMG_20181106_151642](./img/IMG_20181106_153016.jpg)

![IMG_20181106_151642](./img/IMG_20181106_153024.jpg)

![IMG_20181106_151642](./img/IMG_20181106_153032.jpg)

![IMG_20181106_151642](./img/IMG_20181106_153045.jpg)

3. Activez et configurez l'agent SNMP sur le DELL 9020, laissez community string en mode Read Only et public pour publicD9020.

![IMG_20181106_151642](./img/IMG_20181106_153606.jpg)

![IMG_20181106_151642](./img/IMG_20181106_153648.jpg)

4. Que faut-il changer sur le DELL 9010 pour que ce dernier soit capable d'interroger l'agent SNMP du Dell 9020 ? 
   - 

![IMG_20181106_151642](./img/IMG_20181106_154249.jpg)

5. A l'aide du browser snmpb, interrogez le DELL 9020 et determinez le nom de l'équipement, le nom du responsable de l'équipement, son nombre d'interfaces et le traffic de chacunes des interfaces.

![IMG_20181106_151642](./img/IMG_20181106_154133.jpg)

![IMG_20181106_151642](./img/IMG_20181106_154328.jpg)

![IMG_20181106_151642](./img/IMG_20181106_154828.jpg)

![IMG_20181106_151642](./img/IMG_20181106_154841.jpg)

6. A l'aide de Wireshark, capturez et présentez les trames lorsque le DELL 9010 demande le nom de l'equipement du DELL 9020. Commentez !
   - On peut voir sur les screens suivants, que le 9010 fait un get avec L'OID 1.3.6.1.2.1.1.5.0 afin de connaitre le nom de l'équipement.
   - Dans la réponse on peut voir : variable-binding-string: PC10CB05

![IMG_20181106_151642](./img/IMG_20181106_155117.jpg)

![IMG_20181106_151642](./img/IMG_20181106_155131.jpg)