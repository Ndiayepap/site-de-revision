#### **RSYNC Sauvegarde automatique**





rsync -e ssh -avz /home/chemin\_dossier NomCompte@ipServ2:/home/chemin\_dossier



Explications :

rsync : commande Rsync.

\-e ssh : utilise le protocole SSH pour sécuriser la connexion et le transfert des données.

\-a : mode archivage (préserve l’intégrité des fichiers : permissions, dates, structure de répertoires, etc.).

\-v : mode verbose (affiche les détails du processus).

\-z : compression des données pour réduire le temps de transfert.

/home/Directeur/Travail : chemin du dossier source.



NomCompte@ipServ2:/home/Sauvegarde/Travail :

NomCompte : nom de l’utilisateur SSH qui se connecte au serveur distant.

@ipServ2 : adresse IP du serveur distant.

/home/Sauvegarde/Travail : chemin du dossier de destination sur le serveur Serv2.





Planifié avec Crontab

Avant toute configuration, vérifiez si le service cron est actif :

systemctl status cron

Si le service n'est pas actif, démarrez-le avec :

systemctl start cron



modification du fichier crontab

crontab -e

Ensuite, redémarrez le service cron pour appliquer les changements :

systemctl restart cron.service

Vérifiez que le service redémarre correctement :

systemctl status cron.service

Vérifier les logs

tail -f /var/log/cron.log



Pour un envoi de mail

MTA (Mail Transfer Agent)









### **heartbeat**



continuité des services, 

Heartbeat peut être intégré à des solutions de virtualisation, de stockage, de sauvegarde, etc., pour créer des environnements informatiques hautement disponibles et résilients.



HeartBeat ou LinuxHA (High Availability) est un service permettant la mise en cluster de plusieurs serveurs. Ce service permet l’implémentation de la haute disponibilité du système ou de services permettant à plusieurs serveurs GNU/Linux d’effectuer entre eux un processus de failover (basculement ou tolérance aux pannes).



installation d’Heartbeat

Étape 1 : apt update \&\& apt upgrade -y

Étape 2 : apt install heartbeat -y

Étape 3 : apt install apache2 -y //pour tester réellement la tolérance aux pannes d’un site web

nano /etc/hosts -> pour vérifier le nom des 2 PC

nano /etc/hostname -> vérifier si le nom de la machine est bien le même sur les 2PC

nano /var/www/html/index.html -> ajouter le nom du PC avant Apache2 sur les 2PC



3 fichiers nécessaires à Heartbeat

/etc/heartbeat/ha.cf

Ce fichier est le fichier de configuration principal de Heartbeat. Il définit les paramètres de configuration essentiels pour le fonctionnement de Heartbeat, tels que les délais, les adresses IP, les interfaces réseau, les scripts d’arrêt et de démarrage, etc. Il contient également des informations sur les nœuds du cluster, tels que leurs noms et leurs adresses IP.

/etc/heartbeat/haresources

Ce fichier indique à Heartbeat quels services ou ressources doivent être surveillés et gérés en haute disponibilité. Il répertorie les ressources du cluster, telles que les adresses IP virtuelles, les serveurs, les services, etc. Chaque ligne de ce fichier indique quelle ressource doit être surveillée et à quel nœud elle est actuellement attribuée. En cas de panne du nœud actif, Heartbeat bascule la ressource vers un autre nœud en fonction de cette configuration.

/etc/heartbeat/authkeys

Ce fichier contient les clés d’authentification nécessaires associées à un groupe pour sécuriser les communications entre les nœuds du cluster Heartbeat. Il s’agit d’un élément sécuritaire d’établissement de confiance entre les membres du cluster.



Étapes de configuration d’Heartbeat

Étape 1 : vérifiez l’existence des 3 fichiers précédents.

Étape 2 : s’ils existent, alors étape 4. S’ils n’existent pas, alors étape 3.

Étape 3 : touch /etc/heartbeat/ha.cf /etc/heartbeat/haresources /etc/heartbeat/authkeys

Étape 4 : protégez l’accès (en lecture/écriture) au propriétaire du fichier authkeys, avec la commande : chmod 600 /etc/heartbeat/authkeys

Étape 5 : configurez le fichier /etc/heartbeat/ha.cf avec la commande : nano /etc/heartbeat/ha.cf et les éléments suivants :



nano /etc/heartbeat/ha.cf -> modifier avec:

\[   logfile /var/log/heartbeat.log -> fichier de log

logfacility daemon -> identification des logs (daemon)

node debian debian-PC2 -> le nom des machines

keepalive 1 -> contrôle tous les x secondes

deadtime 10 -> déclarer mort après x secondes

ucast ens160 192.168.64.130 -> carte réseau et IP de la machine 2

auto\_failback yes   ]



nano /etc/heartbeat/authkeys -> modifier par:

\[    auth 1

1 sha1 password ->   ]



&#x20;nano /etc/heartbeat/haresources -> modifier par:

\[   nom\_machine1 IPaddr::192.168.64.200/ens160:0 -> IP virtuelle qui pointe sur les 2 machines et specifier un service si non il prend en charge tous les services.  ]



systemctl restart heartbeat.service -> pour redémarrer le service.

systemctl status heartbeat.service -> vérification s'il est actif.



FAIRE LA MÊME CHOSE SUR LA MACHINE 2 en pointant sur machine 1









### 

### **SAMBA: Installation et configuration d'un systeme de partage**



**sudo apt update**

**sudo apt install samba samba-common-bin** 

**sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.back -> faire une copie avant de le modifier.**

**sudo mkdir /home/shared/sharedsmb  -> pour creer le dossier**

**sudo nano /etc/samba/smb.conf**

**Et copier / coller \[**

**\[chemin\_dossier2]**

**path = /home/chared/sharedsmb**

**readonly = no**

**browseable = yes ]**

**sudo systemctl restart smbd -> redemarrer samba**

**sudo systemctl status smbd -> pour verifier si tout est ok**



**valid user -> limite l'acces au partage aux utilisateurs specifiques**



**Configuration avancée** 

**Création d'un utilisateur Linux (si l'utilisateur n'existe pas déjà) :**

**sudo adduser nom\_utilisateur**

**Ajout de l'utilisateur à Samba :**

**sudo smbpasswd -a nom\_utilisateur**



**chmod : permet de définir qui peut lire, écrire ou exécuter un fichier ou un dossier. Par exemple, chmod 755 /dossier donne au propriétaire tous les droits, tandis que les autres utilisateurs et le groupe peuvent seulement lire et exécuter.**

**chown : change le propriétaire (et/ou groupe) d'un fichier. Par exemple, chown utilisateur:group /dossier attribue la propriété du dossier à « utilisateur » et l'associe au « groupe ».**



**Au niveau de Samba**

**Vous pouvez spécifier qui peut voir le partage, qui peut lire les données, et qui peut écrire ou modifier les fichiers.**

**read only : un partage configuré avec read only = yes interdit l'écriture à tous les utilisateurs, les limitant à la lecture des fichiers.**

**write list : spécifie les utilisateurs ou groupes qui ont le droit d'écriture sur un partage, même si read only = yes. Par exemple, write list = user1 user2 permet à user1 et user2 d'écrire dans le partage.**

**valid users : limite l'accès au partage aux utilisateurs et groupes énumérés. Si un utilisateur n'est pas listé**





**Pour créer un partage de fichiers, vous devez ajouter une nouvelle entrée dans le fichier smb.conf. Voici un exemple de configuration pour un partage sécurisé :**

**1 \[PartageSecurise]**

**2 path = /chemin/vers/dossier/partage**

**3 valid users = nom\_utilisateur**

**4 read only = no**

**5 browseable = yes**



**Activation de l'héritage des permissions**

**inherit permissions = yes**

**En activant inherit permissions, vous vous assurez que toute la hiérarchie de fichiers et dossiers au sein de ce partage maintient une cohérence dans les permissions, facilitant la gestion des accès et renforçant la sécurité du partage.**





**Consulter les journaux de Samba :**

**/var/log/samba/**



**Sécurité et performance des partages Samba**

**Activez le chiffrement pour les transferts de données en définissant smb encrypt = mandatory dans smb.conf**

