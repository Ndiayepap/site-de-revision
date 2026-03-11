routage: Configuration de routage

Étape 1 : créez les interfaces virtuelles sur le port Fa0 / 0 du routeur. Vous devez en priorité activer l'interface physique afin que les interfaces virtuelles soient opérationnelles.

Voici les commandes à effectuer :

Router>enable

Router#configuration terminal

Router(config)#interface fa0 / 0

Router(config-if)#no shutdown

Router(config-if)#exit

Étape 2 : maintenant, créez l'interface fa0 / 0.1 (interface virtuelle 1 de l'interface physique fa0 / 0), pour la passerelle des postes du VLAN 20.

Voici les commandes à effectuer :
Router(config)#interface fa0 / 0.1
Router(config-subif)#encapsulation dot1Q 20
Router(config-subif)#ip address 192.168.20.254 255.255.255.0
Router(config-subif)#no shutdown
Router(config-subif)#exit


Étape 3 : même manipulation pour l'interface Fa0 / 0.2 et les postes du réseau du VLAN 30.
Voici les commandes à effectuer :
Router(config)#interface fa0 / 0.2
Router(config-subif)#encapsulation dot1Q 30
Router(config-subif)#ip address 192.168.30.254 255.255.255.0
Router(config-subif)#no shutdown
Router(config-subif)#exit
Étape 4 : que faire du switch ?
Mettez le port Fa0 / 24 du Switch1 (faisant le lien avec le routeur) en mode « trunk » pour qu'il puisse acheminer également tous les VLANs vers et depuis le routeur.
Voici les commandes à effectuer :
Switch(config)#interface fa0 / 24
Switch(config-if)#switchport mode trunk
Switch(config-if)#switchport trunk allowed vlan 20,30,99
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)#no shutdown
Switch(config-if)#exit
Étape 5 : une fois nos passerelles renseignées sur les postes (exemple : 192.168.30.254 pour les postes du VLAN 30 selon notre schéma), il nous reste à tester la communication inter-VLANs avec un ping, tout simplement.



Le routage inter-VLANs

Router on a stick
Définition
Dans cette méthode, contrairement à l'ancien routage, un seul port d'interface physique est utilisé pour le routage du trafic entre les segments du réseau. L'administrateur réseau n'a pas besoin de créer des interfaces VLAN séparées.
Au lieu de cela, toutes les interfaces de 1 à 10 sont créées avec une seule interface physique. Cette méthode est simple à mettre en œuvre et est utilisée pour les petits et moyens réseaux.
Cette configuration permet de réaliser des économies sur les interfaces.
Configurations réseau pour la communication inter-VLANs à l'aide de la méthode router on a stick
Dans cette partie, nous allons apprendre à configurer le routage inter-VLANs en utilisant la méthode router on a stick. Cela sera similaire à ce qui a été vu précédemment, avec plus de précision et la mise en place complète des VLANs.
Exemple: La configuration d'un VLAN contenant 4 PC, 1 commutateur et 1 routeur connecté


Méthode: Les étapes de la configuration
Étape 1 : on configure deux VLANs 10 et 20, avec les PC0 et PC1 sur le VLAN 10, et les PC2 et PC3 sur le VLAN 20.
Adresse IP de PC0 - 192.168.1.10
Adresse IP de PC1 - 192.168.1.20
Adresse IP de PC2 - 192.168.2.10
Adresse IP de PC3 - 192.168.2.20
Passerelle par défaut pour VLAN10 - 192.168.1.1
Passerelle par défaut pour VLAN20 - 192.168.2.1
Pour diviser le réseau en 2 sous-réseaux, créez deux VLANS sur le commutateur : VLAN 10 et VLAN 20. Nommez-le VLAN 10 « étudiant » et le VLAN 20 « personnel ».
Pour créer les 2 VLANs, entrez dans le mode de configuration en utilisant la commande de terminal de configuration, puis inscrivez le numéro VLAN avec son nom.
Voici les commandes à effectuer :
Switch>enable
Switch#config terminal
Switch(config)#vlan 10
Switch(config-vlan)#name etudiant
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#name personnel
Switch(config-vlan)#exit

Étape 2 : indiquez maintenant les ports de commutation aux VLANS. Les ports fa0 / 1 et fa0 / 2 servent de ports d'accès au VLAN 10 et les ports fa0 / 3 et fa0 / 4 servent de ports d'accès au VLAN 20. Utilisez le port fa0 / 5 en port « trunk » pour transporter le trafic entre les deux VLANS via le routeur.
Voici les commandes à effectuer :
Switch>enable
Switch#config terminal
Switch(config)#int fa 0 / 1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#exit
Puis :
Switch(config)#int fa 0 / 2
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#exit

Complément
« fa » (fast ethernet) se réfère aux ports Ethernet rapides utilisés pour connecter les hôtes réseau au commutateur ou au routeur.
Dans la configuration que l'on vient d'effectuer, fa0 / 1 et fa0 / 2 sont configurés comme des ports d'accès avec la commande switchport mode access.
Comme ils appartiennent au VLAN 10, la commande « switchport access vlan 10 » est utilisée pour les configurer en tant que ports d'accès dans le VLAN 10.
Méthode
Étape 3 : nous allons effectuer la configuration pour les ports d'accès fa0 / 3 et fa0 / 4.
Voici les commandes à effectuer :
Switch(config)#int fa 0 / 3
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 20
Switch(config-if)#exit
Switch(config)#int fa 0 / 4
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 20
Switch(config-if)#exit

Complément
Les interfaces fa0 / 3 et fa0 / 4 sont configurées comme des ports d'accès à l'aide de la commande switchport mode access. Appartenant au VLAN 20, la commande « switchport access vlan 20 » est utilisée pour les configurer en tant que ports d'accès dans le VLAN 20.
Méthode
Étape 4 : nous allons effectuer la configuration pour le port « trunk » fa0 / 5.
Voici les commandes à effectuer :
Switch(config)#int fa 0 / 5
Switch(config-if)#switchport mode trunk
Switch(config-if)#do write

Complément
L'interface fa0 / 5 sert de port « trunk ». Pour le configurer comme un port « trunk » et non un port d'accès, on a utilisé la commande « switchport mode trunk » pour la totalité de l'interface.
Méthode
Étape 5 : renseignez les adresses IP en statique sur chaque PC se trouvant sur le réseau.


Étape 6 : nous allons configurer le routeur pour permettre au trafic de passer du VLAN 10 au VLAN 20. Pour que les PC communiquent, divisez l'interface unique en plusieurs sous-interfaces, où chaque sous-interface fera office de passerelle par défaut pour chacun des VLANs. Cela permettra au 2 sous-réseaux de communiquer avec l'interface unique.
Voici les commandes à effectuer :
Router>enable
Router#config terminal
Router(config)#int g0 / 0
Router(config-if)#no shutdown
Router(config-if)#int g0 / 0.10
Router(config-subif)#encapsulation dot1q 10
Router(config-subif)#ip add 192.168.1.1 255.255.255.0
Router(config-subif)#exit

Puis :
Router(config)#int g0 / 0
Router(config-if)#no shutdown
Router(config-if)#int g0 / 0.20
Router(config-subif)#encapsulation dot1q 20
Router(config-subif)#ip add 192.168.2.1 255.255.255.0
Router(config-subif)#exit
Router(config)#do write
Router(config)#exit

Complément
L'interface g0 / 0 est subdivisée en deux sous-interfaces : g0 / 0.10 pour le VLAN 10 et g0 / 0.20 pour le VLAN 20.
Les deux sous-interfaces ont des adresses IP attitrées et servent de ports principaux pour transporter le trafic.
Méthode
Étape 7 : testez à présent la connectivité inter-VLANs en utilisant le ping sur les différents PC. Si on ping le PC2 du VLAN 20 à partir du PC0 du VLAN 10, il doit être réussi.


Fondamental
Le routage inter-VLANs est un concept essentiel. C'est la meilleure façon de diviser un grand réseau local et de permettre la communication entre les hôtes du réseau.

Il existe différentes sortes d'adresses MAC sécurisées :
Sécurisées statiques
Sécurisées dynamiques
Sécurisées rémanentes



Les principales commandes et configurations possible sur un commutateur Cisco sont disponibles ici :
https://www.numelion.com/commandes-commutateurs-cisco.html



La configuration de la sécurité des ports d'un commutateur (switch)
Dans la console du switch (CLI) :
S1 en (enable)
S1# configure terminal (ou conf t)
S1(config)# interface fastEthernet 0/18


Configuration avancée de l'adresse MAC statique
L'adresse MAC sécurisée statique se configure de façon manuelle avec l'aide de la commande de configuration d'interface.

Dans la console du switch (CLI) :
S1 enable
S1 conf t (configure terminal)
S1(config)# interface fa 0/1-5
S1(config-if)# switchport mode access
S1(config-if)# switchport port-security
S1(config-if)# switchport port-security mac-address [votre_MAC_address]
S1(config-if)# end
L'adresse MAC est de ce fait stockée dans la table d'adresses MAC et elle est ajoutée dans le running-config.

Configuration avancée de l'adresse MAC dynamique
L'adresse MAC sécurisée dynamique va être récupérée dynamiquement et stockée seulement dans la table d'adresses MAC. Au nouveau démarrage du switch, l'adresse est supprimée.

Dans la console du switchd :
S1 enable
S1 conf t
S1(config)# interface fa 0/1-5
S1(config-if)# switchport mode access
S1(config-if)# switchport port-security ?
S1(config-if)# end

Configuration avancée de l'adresse MAC sécurisé rémanente
L'adresse MAC sécurisée rémanente sera récupérée dynamiquement et enregistrée dans le running-config.

Dans la console du switch :
S1 enable
S1 conf t
S1(config)# interface fa0/1-5
S1(config-if)# switchport mode access
S1(config-if)# switchport port-security
S1(config-if)# switchport port-security maximum 10
S1(config-if)# switchport port-security mac-address sticky
S1(config-if)# end

Si elles ne sont pas enregistrées, les adresses MAC sécurisées rémanentes auront disparu.
Si l'apprentissage rémanent est désactivé et que l'on entre la commande de configuration d'interface « switchport port-security mac-address sticky adresse_mac », on verra un message d'erreur et l'adresse MAC sécurisée rémanente ne sera pas ajoutée dans la configuration en cours.

Il est possible de vérifier la sécurité des ports, voici comment procéder.
Pour l'affichage des paramètres de sécurité des ports du commutateur ou de l'interface que l'on souhaite :
switch# show port-security [ici mettre : interface id_interface]
Pour la vérification de toute les adresses MAC sécurisées configurées dans l'ensemble des interfaces de commutation, ou bien sur l'une des interfaces que l'on veut :
switch# show port-security [ici mettre : interface id_interface]

Pour désactiver les ports qui ne sont pas utilisés, utilisez les commandes 
« shutdown » et « interface range ».
S1 enable
S1 conf t
S1(config)# interface fa0/6-10
S1(config-if)# shutdown
S1(config-if)# end



Remarque:     IOS ≠ iOS
IOS Cisco signifie Internetwork Operating System
iOS Apple signifie iPhone Operating System



Type d’équipement       |        Type de câble

PC à Commutateur         ->  Câble droit (Ethernet)
Commutateur à Routeur  ->  Câble croisé
Routeur à Routeur           ->   Câble série

Astuces
Si les voyants sont rouges, le lien n’est pas actif (erreur de câblage ou interface désactivée).
Utilisez la commande show ip interface brief pour voir l’état des connexions.



Mode de configuration globale et configuration des interfaces
1. Accès au mode de configuration globale
Le mode de configuration globale permet de modifier les paramètres du routeur.
Commande pour accéder au mode de configuration globale
Router# configure terminal 
Router(config)#

2. Commande pour sortir du mode de configuration
Router(config)# exit
Router#

3. Mode de configuration des interfaces
Le mode de configuration des interfaces est utilisé pour gérer les interfaces réseau du routeur.
Commande pour entrer dans la configuration d’une interface :
Router(config)# interface GigabitEthernet0/0
Router(config-if)#

Exemple de configuration d’une interface avec une adresse IP
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)#




Accès aux modes Enable et Config Mode
Pour des raisons de sécurité, Cisco impose un contrôle d’accès aux modes avancés.
1. Sécurisation de l’accès au mode Enable
Par défaut, tout utilisateur peut entrer en mode Enable. Pour éviter cela, il est recommandé d’ajouter un mot de passe.
Définition d’un mot de passe pour le mode Enable
Router(config)# enable password cisco123
Mais attention !
Le mot de passe défini avec enable password est stocké en clair.
Solution recommandée : utiliser enable secret qui chiffre le mot de passe.
Router(config)# enable secret Cisco2024
2. Sécurisation de l’accès aux interfaces de configuration
Il est possible de restreindre l’accès aux lignes de commande (console, SSH, Telnet).
Configuration d’un mot de passe sur la console
Router(config)# line console 0
Router(config-line)# password admin123
Router(config-line)# login
Router(config-line)# exit
Configuration d’un accès distant (Telnet/SSH) sécurisé
Router(config)# line vty 0 4
Router(config-line)# password network123
Router(config-line)# login
Router(config-line)# exit
Pourquoi sécuriser ces accès ?
Évite les accès non autorisés
Protège contre les attaques distantes



Configurer les modes d’accès et les sécuriser
1. Matériel requis
1 routeur Cisco
1 PC connecté au routeur via console
2. Étapes de configuration
Passer en mode Enable et définir un mot de passeRouter> enableRouter# configure terminalRouter(config)# enable secret securepass
Sécuriser l’accès console
Router(config)# line console 0
Router(config-line)# password admin123
Router(config-line)# login
Router(config-line)# exit

Sécuriser l’accès distant via SSH :
Router(config)# hostname Secure
Router
Router(config)# ip domain-name example.com
Router(config)# crypto key generate rsa
Router(config)# line vty 0 4
Router(config-line)# transport input ssh
Router(config-line)# password sshaccess
Router(config-line)# login
Router(config-line)# exit

Sauvegarder la configurationSecure
Router# copy running-config startup-config

Résultat attendu :
Le routeur est configuré et sécurisé,
L’accès via console et SSH demande un mot de passe.


Commande pour définir une bannière de connexion :
RouterParis(config)# banner motd #Attention! Accès réservé aux administrateurs réseau.#
Explication
banner motd : définit un Message of the Day (MOTD)
# : délimiteur du message
Le message s’affiche avant l’authentification

Astuce
Vérifiez toujours l’état des interfaces avec show ip interface brief.




Segmentation du réseau avec les VLANs
1. Qu’est-ce qu’un VLAN ?
Un VLAN (Virtual Local Area Network) est un réseau logique qui permet de segmenter les périphériques sur un même réseau physique.
Avantages des VLANs
Réduction du trafic de diffusion
Meilleure sécurité
Optimisation des performances réseau
Commande pour créer un VLAN :Switch(config)# vlan 10Switch(config-vlan)# name ComptabilitéSwitch(config-vlan)# exit
Commande pour affecter un port à un VLAN :Switch(config)# interface FastEthernet0/1Switch(config-if)# switchport mode accessSwitch(config-if)# switchport access vlan 10Switch(config-if)# exit
Explication
Vlan 10 → Création du VLAN 10
Switchport access vlan 10 → Associe l’interface au VLAN
                              Segmentation des VLANs et routage inter-VLAN
« Le schéma ci-dessus représente une infrastructure segmentée en VLANs. Chaque PC appartient à un VLAN spécifique (VLAN 10, VLAN 20, VLAN 30), et est connecté à un commutateur central. Le routage entre VLANs est assuré par un routeur connecté au commutateur via un lien trunk (802.1Q). Ce modèle est utilisé pour améliorer la sécurité, la performance et la gestion du réseau. »





Interconnexion des VLANs avec Trunk et VTP

Les VLANs sur différents commutateurs ne peuvent pas communiquer sans trunk et VTP.
1. Configuration d’un port trunk
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,30
Switch(config-if)# exit
Explication
Switchport mode trunk → Configure le port en mode trunk
Switchport trunk allowed vlan 10,20,30 → Autorise seulement certains VLANs
2. Configuration du VTP (VLAN Trunking Protocol)
Le VTP permet de synchroniser les VLANs sur plusieurs commutateurs.
                  Schéma : interconnexion des VLANs avec Trunk et VTP
Le schéma ci-dessous représente une infrastructure VLAN segmentée sur deux commutateurs Cisco connectés via un lien Trunk 802.1Q.
Switch 1 est configuré en VTP Serveur : il gère et distribue la base des VLANs.
Switch 2 est en mode VTP Client : il synchronise automatiquement ses VLANs avec le serveur VTP.
Chaque PC est assigné à un VLAN spécifique (VLAN 10, VLAN 20, VLAN 30) et est relié à un commutateur.
Le Trunk (802.1Q) permet aux VLANs de communiquer entre les deux switches tout en conservant l’isolation de chaque VLAN.
Configuration d’un switch en mode VTP serveur
Switch(config)# vtp domain MonReseau
Switch(config)# vtp mode server
Switch(config)# vtp password secret123
Explication
Vtp domain MonReseau → Définit le nom du domaine VTP
Vtp mode server → Configure le switch en mode serveur
Vtp password secret123 → Définit un mot de passe VTP



Configuration des protocoles de redondance (HSRP, VRRP, GLBP)
Les protocoles de redondance permettent d’éviter une panne du réseau en assurant la haute disponibilité des routeurs.
Schéma : configuration de HSRP pour la redondance réseau
Le schéma ci-dessous illustre le fonctionnement du protocole HSRP (Hot Standby Router Protocol) dans un réseau d'entreprise.
Routeur 1 est actif avec une priorité plus élevée et gère le trafic réseau.
Routeur 2 est en mode veille et prend automatiquement la relève en cas de panne du Routeur 1.
Une adresse IP virtuelle partagée (192.168.1.254) est utilisée pour assurer la continuité du service.
Les PC sont connectés à un commutateur central, qui maintient la liaison entre les routeurs et le réseau local.
Une liaison redondante assure une continuité de service fluide en cas de basculement.
Ce modèle garantit la haute disponibilité du réseau et évite toute interruption de service.
Les trois principaux protocoles de redondance :
HSRP (Hot Standby Router Protocol - Cisco)
VRRP (Virtual Router Redundancy Protocol - Standard)
GLBP (Gateway Load Balancing Protocol - Cisco, avec équilibrage de charge)
1. Configuration HSRP (Cisco)
Router(config)# interface GigabitEthernet0/1
Router(config-if)# standby 1 ip 192.168.1.254
Router(config-if)# standby 1 priority 110
Router(config-if)# standby 1 preempt
Explication
Standby 1 ip 192.168.1.254 → Définit l’IP virtuelle du groupe HSRP
Standby 1 priority 110 → Définit la priorité (plus haute = routeur actif)
Standby 1 preempt → Active le basculement automatique




Configuration des VLANs avec Routage OSPF et DHCP
Objectif
Mettre en place une infrastructure réseau segmentée en VLANs, assurer le routage entre VLANs avec OSPF, et attribuer dynamiquement des adresses IP avec DHCP.
Équipements nécessaires :
1 Routeur Cisco
1 Commutateur Cisco
3 PC
Packet Tracer ou équipement réel
2. Configuration des VLANs sur le commutateur
Les VLANs permettent de segmenter le réseau pour améliorer la sécurité et les performances.
Création des VLANs
Switch(config)# vlan 10
Switch(config-vlan)# name Vlan_RH
Switch(config-vlan)# exit
 
Switch(config)# vlan 20
Switch(config-vlan)# name Vlan_IT
Switch(config-vlan)# exit
Affectation des interfaces aux VLANs
Switch(config)# interface FastEthernet0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
 
Switch(config)# interface FastEthernet0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit
3. Configuration du routage inter-VLAN avec OSPF
Le routage inter-VLAN permet aux VLANs de communiquer entre eux via un routeur.
Activation du routage sur le routeur
Router(config)# interface GigabitEthernet0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# no shutdown
 
Router(config)# interface GigabitEthernet0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# no shutdown
Activation et configuration du protocole OSPF
Router(config)# router ospf 1
Router(config-router)# network 192.168.10.0 0.0.0.255 area 0
Router(config-router)# network 192.168.20.0 0.0.0.255 area 0
Router(config-router)# exit
4. Configuration d'un serveur DHCP sur le routeur
Le serveur DHCP attribuera automatiquement des adresses IP aux PC dans les VLANs.
Création des pools DHCP
Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.10
Router(config)# ip dhcp excluded-address 192.168.20.1 192.168.20.10
 
Router(config)# ip dhcp pool VLAN10
Router(dhcp-config)# network 192.168.10.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.10.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
 
Router(config)# ip dhcp pool VLAN20
Router(dhcp-config)# network 192.168.20.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.20.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
5. Vérification et tests
Sur les PC : obtenir une adresse IP automatique
PC> ipconfig /renew
Vérifier les VLANs sur le switch
Switch# show vlan brief
Vérifier les interfaces configurées sur le routeur
Router# show ip interface brief
Vérifier le routage OSPF
Router# show ip route ospf
Résultat attendu
Les VLANs sont segmentés et configurés
Le routage entre VLANs est assuré par OSPF
Les PC reçoivent leurs adresses IP automatiquement via DHCP




Sécurisation du réseau avec les ACLs (Listes de Contrôle d’Accès)
Les ACLs permettent de filtrer le trafic réseau pour renforcer la sécurité.
Le schéma ci-dessous illustre comment une Liste de Contrôle d’Accès (ACL) est appliquée sur un routeur Cisco.
PC1 est autorisé à envoyer du trafic au routeur, alors que.
PC2 est bloqué par l’ACL, empêchant l’accès au réseau.
L’ACL permet ainsi de contrôler le trafic réseau en bloquant les flux indésirables tout en laissant passer le trafic autorisé.
1. Création d’une ACL standard (Filtrage basé sur l’adresse IP source)
Router(config)# access-list 10 permit 192.168.1.0 0.0.0.255
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip access-group 10 in
Explication
Access-list 10 permit 192.168.1.0 0.0.0.255 → Autorise tout le sous-réseau 192.168.1.x
Ip access-group 10 in → Applique l’ACL à l’interface
2. Création d’une ACL étendue (Filtrage par protocole, IP source et destination)
Router(config)# access-list 101 deny tcp any host 192.168.1.100 eq 23
Router(config)# access-list 101 permit ip any any
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip access-group 101 in
Explication
Deny tcp any host 192.168.1.100 eq 23 → Bloque Telnet vers l’IP 192.168.1.100
Permit ip any any → Autorise tout le reste