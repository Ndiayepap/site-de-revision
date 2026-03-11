#### Sécurité AD DS

Bonnes pratiques

Lorsque vous envisagez de créer une infrastructure Active Directory, il est bon de connaître quelques conseils pour éviter les problèmes de sécurité et de configuration :



Renommer l'administrateur de domaine. Le premier utilisateur utilisé pour lancer une attaque est l'administrateur ; votre première étape consiste donc à changer le nom d'administrateur de domaine par défaut. Utilisez un nom complètement différent des normes, comme AdminContosoAD.



Mot de passe fort pour l'administrateur de domaine. Sécurité, sûreté, sécurité ! L'administrateur du domaine doit avoir un mot de passe fort et les informations d'identification doivent être réservées.



Informations d'identification dédiées pour l'informatique. L'une des premières règles consiste à séparer les informations d'identification par défaut de la direction pour empêcher une escalade de la sécurité en cas d'attaque externe.



Attribuer la bonne autorisation. Si vous avez plusieurs administrateurs dans votre infrastructure, il est fondamental d'attribuer la bonne autorisation et les bonnes informations d'identification pour chaque utilisateur. Personne ne doit être au-dessus des administrateurs de domaine pour éviter la possibilité de changer le schéma AD ou de modifier le modèle de forêt.



Configurer GPO. Configurer les stratégies de groupe par utilisateurs et ordinateurs, cela permet une granularité parfaite. N'oubliez pas d'éviter trop d'objets de stratégie de groupe, mais également de regrouper de nombreux paramètres dans un seul objet de stratégie de groupe. N'utilisez pas l'objet « stratégie de groupe » en tant que stratégie de domaine par défaut !



Mot de passe fort pour les utilisateurs. L'administrateur de domaine, mais aussi tous les utilisateurs doivent répondre aux exigences de complexité du mot de passe. Si vous utilisez Windows 10, une idée consiste à configurer Windows Hello Entreprise pour simplifier la méthode d'authentification, sans réduire la sécurité.



Activer la corbeille. La corbeille a été introduite dans Windows Server 2008 R2 et constitue le moyen idéal pour restaurer un élément en quelques secondes, sans avoir à exécuter AD Restore.



Au moins deux contrôleurs de domaine. Peu importe si votre infrastructure n'est pas une entreprise, vous devez avoir deux contrôleurs de domaine pour éviter les pannes critiques.



Supprimer les éléments obsolètes. N'oubliez pas de nettoyer votre infrastructure d'utilisateurs et d'ordinateurs là où ils ne sont plus présents ou nécessaires. Ceci afin d'éviter des problèmes ou des problèmes de sécurité.



Un contrôleur de domaine n'est pas un ordinateur. N'installez rien à l'intérieur d'un contrôleur de domaine ! Pas de logiciel, pas d'applications tierces, pas de rôles, rien !



Règle de convention de nommage. Définissez une convention de nommage avant de créer votre infrastructure, utilisateurs, clients, serveurs, appareils et ressources (groupes, partages, etc.). Cela vous aidera à simplifier la gestion et l'évolutivité.



Patcher vos contrôleurs de domaine. Les attaquants exploitent rapidement les vulnérabilités connues, ce qui signifie que vous devez toujours maintenir votre machine à jour. Planifiez le bon moment pour installer les mises à jour Windows.



Audit. Déployez une solution d'audit pour savoir qui effectue les modifications. Ce n'est pas une exigence du RGPD, mais un moyen d'éviter les problèmes de sécurité









ADDS: Le rôle Active Directory Domain Service (ADDS) est un service qui permet la gestion des comptes utilisateurs (identités) et authentifications, des droits d’accès, etc. pour des ressources réseaux.



DNS: Le rôle Domain Name Service (DNS) est un service qui permet de résoudre des noms d’hôtes en fonction d’adresses IP (et inversement), de centraliser des informations de noms, etc.



DHCP: Le rôle Dynamic Host Configuration Protocol (DHCP) est un service qui permet d’attribuer, aux périphériques réseaux, des paramètres TCP/IP (Adresse IP, masque, passerelle, IP du serveur DNS, etc.).







#### DHCP



La première étape est le DHCP discover.Un client sur lequel nous connecterions un câble réseau (ou lors d’une connexion à un réseau wifi) va envoyer une requête pour trouver un serveur DHCP et demander une adresse IP à celui-ci. Le port 67 est utilisé par les serveurs DHCP pour recevoir les demandes, tandis que le port 68 est utilisé par les clients DHCP pour envoyer leurs demandes aux serveurs.

Vient ensuite le DHCP offer. Un serveur DHCP sur le réseau répond favorablement à la requête de notre client et lui propose une adresse IP.

Le DHCP request est le retour du client. Il acquiesce l’acceptation de l’adresse IP fournie à l’étape précédente et demande aux serveurs DHCP de ne plus se manifester.

Pour finir, on retrouve le DHCP ACK. Cette dernière étape met fin à la demande du client : le serveur formalise l’acceptation du client.

Toutes ces étapes aboutissent à l’obtention d’une adresse IP pour le poste client



Voir votre interface réseau et le modifier (désactiver DHCP, changer IP, etc...)

cat /etc/network/interfaces

Pour éditer:

Nano /etc/network/interfaces

iface enpos3 inet static

address 192.168.56.10

netmask 255.255.255.0

gateway 192.168.56.1

dns-nameservers 8.8.8.8

Installer le server DHCP

Sudo apt install isc-dhcp-server

Configuration 

nano /etc/default/isc-dhcp-serve

Définir plage IP DHCP

nano /etc/dhcp/dhcpd.conf

Redémarrez le service 

systemctl restart isc-dhcp-server.service





Les classes sont définies ci-dessous :

Classe A : 10.0.0.0 à 10.255.255.255

Classe B : 172.16.0.0 à 172.31.255.255

Classe C : 192.168.0.0 à 192.168.255.255



Pour éviter que les non-clients ne  puissent pas se connecter 

deny-unknown-clients

