Dans GNU/Linux, il y a toujours un équivalent des rôles et services existants dans la famille Microsoft Windows Serveur.
Ex : ADDS sur Microsoft Windows = Samba4 sur Linux, 
DNS sur Microsoft Windows = Bind9 sur Linux, 
DHCP sur Microsoft Windows = ISC-DHCP-SERVER sur Linux, 
Partage de fichiers sur Microsoft Windows = SAMBA sur Linux, 
IIS sur Microsoft Windows = Apache/NGINX sur Linux, etc.

chmod 644 MonFichier : RW pour le proprio, R pour le groupe, R pour les autres concernant le fichier MonFichier.
chmod –R 700 monRepertoire : RWX (contrôle total) pour le proprio, rien pour le groupe et rien pour les autres concernant le répertoire monRepertoire et tout son contenu (sous-répertoires et fichiers).
Nota : la commande setfacl permet de gérer les droits par utilisateur.
La commande chown change le propriétaire du fichier ou répertoire.
Ex : chown autreUtilisateur MonFichier : change le propriétaire du fichier MonFichier en autreUtilisateur. autreUtilisateur devient donc le propriétaire du fichier MonFichier.
La commande chgrp change le groupe propriétaire du fichier ou répertoire.
Ex : chgrp unGroupe MonFichier : change le groupe propriétaire du fichier MonFichier en unGroupe. unGroupe devient donc le le groupe propriétaire du fichier MonFichier.





Créer un utilisateur
sudo useradd -m nom_utilisateur = non interactif
sudo passwd nom_utilisateur

changer d’utilisateur sur une console
su nom_utilisateur

 Créer un nouveau groupe
sudo groupadd nom_du_groupe

Ajout d'utilisateurs : pour ajouter un utilisateur à un groupe
sudo usermod -a -G nom_du_groupe nom_utilisateur

Vérification : lister les membres d'un groupe
getent group [nom_du_groupe]

Pour supprimer un utilisateur
sudo userdel -r nom_utilisateur

Expiration des mots de passe
passwd [nom_utilisateur]

chmod (change mode) : modifie les permissions d'un fichier ou répertoire.
chmod 755 fichier

change le propriétaire d'un fichier
chown utilisateur fichier

chgrp(change group) : change le groupe associé à un fichier
chgrp groupe fichier

Expiration des mots de passe : définissez une expiration régulière des mots de passe pour encourager les utilisateurs à les renouveler fréquemment. Il suffit de mettre une valeur en jour à la variable PASS_MAX_DAYS dans le fichier de configuration.


Gestion des ACL
definir une ACL pour un utilisatur specifique sur un fichier:
setfacl -m u:johne.doe:rwx /path/to/finance/fichier.txt

pour un groupe sur un repertoire:
setfacl -m g:rd_team:rx chemin/du/repertoire

Définir une ACL par défaut sur un dossier :
setfacl -m d:u:pierre:rw /partage

Pour verifier les ACL appliquées:
setfacl chemin/du/repertoire_ou_fichier



Utilisation des clés SSH pour l'authentification
L'authentification par clés SSH est une méthode plus sécurisée que l'utilisation de mots de passe traditionnels, car elle évite la transmission de mots de passe réels sur le réseau.
Pour implémenter cette méthode, commencez par créer une paire de clés, publique et privée, à l'aide de la commande ssh-keygen.
Ensuite, déployez la clé publique sur le serveur distant en l'ajoutant au fichier authorized_keys avec la commande ssh-copy-id utilisateur@serveur.
Enfin, assurez-vous que le fichier sshd_config sur le serveur est configuré pour permettre l'authentification par clé.
Cette configuration renforce la sécurité en minimisant les risques liés à l'interception de mots de passe.

setuid, setgid et sticky bitRéduire
Ces permissions spéciales modifient le comportement des fichiers et répertoires :
setuid : le fichier s'exécute avec les permissions de son propriétaire, et non de l'utilisateur qui l'exécute.
-rwsr-xr-x 1 root root 12345 Jan 10 10:00 /usr/bin/passwd
setgid : les fichiers créés dans un répertoire héritent le groupe du répertoire plutôt que le groupe de l'utilisateur qui les crée.
drwxr-sr-x 2 root developers 4096 Jan 10 10:00 /projects
sticky bit : utilisé principalement sur des répertoires pour permettre aux utilisateurs de supprimer uniquement les fichiers qu'ils possèdent.
drwxrwxrwt 3 admin staff 4096 Jan 10 10:00 /shared/docs




&& => Permet de passer les commandes dans l'ordre
; => Permet d'exécuter la deuxième commande après la première
& => Permet d'exécuter la deuxième commande après la première.
| => Renvoie la sortie de la première commande vers la deuxième.
|| => Permet d'exécuter la deuxième commande seulement si la première a échoué
-y => Permet de tout valider
apt update => Ces commandes servent à la mise à jour Linux
apt upgrade =^
apt full-upgrade =^
apt dist-upgrade =^
hostname -i => Permet de trouver son IP sur Linux rapidement
uname -a => Indique le nom, le type et le système d'exploitation du PC
-a => Supprime tous les droits
a+ => Attribue les droits
vim => Est un éditeur de texte
nano => Est un éditeur de texte simplifié pour les débutants
rm => Supprime le dossier sélectionné
chown => Remplace le propriétaire du fichier ou du répertoire
ged it => Change de fichier en mode simplifié
mkdir => Permet de créer un nouveau répertoire
cd => Permet de revenir en arrière (home)
pwd => Print Working Directory trouve le chemin d'accès au répertoire de travail actuel (dossier) dans lequel vous vous trouvez
rm => Permet de supprimer les répertoires ainsi que leurs contenus
rmdir => Permet de supprimer un répertoire vide
sudo rm -rf /* => Commande de la mort (met tout à zéro)
sudo passwd => Permet de modifier le mot de passe de l'utilisateur et root
sudo passwd root =^
free -h => Permet d'afficher le RAM disponible
lscpu => Permet d'afficher toutes les caractéristiques CPU
lshw => Permet d'afficher toutes les caractéristiques hardware
sudo apt install terminator => Permet l'installation Terminator
sudo root => Permet de se connecter en mode admin
sudo apt install => Permet d'installer des paquets -y
rm -rf => Sert à forcer l'élimination d'un dossier
mkdir -p => Sert à créer un répertoire entre deux répertoires déjà existants




Aide-mémoire des commandes Linux
🔹 Bases
pwd
affiche le chemin courant
Exemple : pwd

ls
liste les fichiers
Exemple : ls
ls -l : lister avec détails (droits, taille, date)
ls -a : inclure les fichiers cachés

--help
aide rapide intégrée à une commande
Exemple : ls --help

man
manuel complet d’une commande (souvent en anglais)
Installation : sudo apt install man-db (souvent déjà installé)
Exemple : man ls

🔹 Droits & exécution

sudo
exécuter une commande avec les droits administrateur
Exemple : sudo apt update

🔹 Gestion des paquets (Debian/Ubuntu/Mint)

apt update && apt upgrade
mettre à jour la liste des paquets et les logiciels installés
Exemple : sudo apt update && sudo apt upgrade

apt install
installe un paquet logiciel
Exemple : sudo apt install manpages-fr

apt remove
désinstaller un paquet logiciel
Exemple : sudo apt remove manpages-fr

📌 Autres distributions (exemple pour installer htop) :

Fedora/Red Hat → sudo dnf install htop
Arch Linux/Manjaro → sudo pacman -S htop
openSUSE → sudo zypper install htop

🔹 Navigation & aide

cd
changer de dossier
Exemple : cd Documents

cd ..
remonter d’un dossier

clear
effacer l’écran du terminal
Exemple : clear

history
afficher l’historique des commandes

history -c
effacer l’historique des commandes

🔹 Fichiers & dossiers

touch
crée un fichier vide ou change la date de dernière modification d’un fichier existant
Exemple : touch fichier.txt

cat
afficher le contenu d’un fichier
Exemple : cat fichier.txt

less
lire un fichier page par page
Exemple : less /etc/passwd

head
affiche le début d’un fichier
Exemple : head -n 10 fichier.txt

tail
affiche la fin d’un fichier
Exemple : tail -n 10 fichier.txt

nano
éditeur de texte simple en terminal
Installation : sudo apt install nano
Exemple : nano fichier.txt

mkdir
crée un dossier
Exemple : mkdir test

rmdir
supprime un dossier vide
Exemple : rmdir test

rm
supprime un fichier
Exemple : rm fichier.txt

cp
copie un fichier
Exemple : cp fichier.txt copie.txt

mv
déplace ou renomme un fichier
Exemple : mv fichier.txt nouveau.txt

find
recherche dans les fichiers/dossiers
Exemple : find . -name "*.txt"

🔹 Système & ressources

uname -a
affiche infos système et noyau
Exemple : uname -a

df -h
affiche l’espace disque utilisé
Exemple : df -h

du -sh
affiche la taille d’un dossier
Exemple : du -sh Documents

top
surveille les processus en temps réel

htop
version améliorée de top
Installation : sudo apt install htop

ps -e
liste les processus en mémoire

grep
recherche du texte
Exemple : ps -e | grep cinnamon

free -h
affiche la mémoire utilisée

uptime
affiche le temps depuis le démarrage

whoami
affiche l’utilisateur courant

id
affiche infos utilisateur et groupes

🔹 Droits & utilisateurs

chmod
change les droits d’accès
Exemple : chmod 755 script.sh

chown
change le propriétaire d’un fichier/dossier
Exemple : chown david fichier.txt

adduser
crée un utilisateur (Debian/Ubuntu/Mint)
Distribution : Debian/Ubuntu/Mint (useradd ailleurs)
Exemple : sudo adduser alice

passwd
change le mot de passe d’un utilisateur
Exemple : sudo passwd alice

deluser
supprime un utilisateur (Debian/Ubuntu/Mint)
Distribution : Debian/Ubuntu/Mint (userdel ailleurs)
Exemple : sudo deluser alice

su
se connecter en tant qu’autre utilisateur (root par défaut)
Exemple : su puis exit

🔹 Réseau

ping
tester une connexion réseau
Exemple : ping google.com

curl
télécharger une page ou un fichier
Installation : sudo apt install curl
Exemple : curl   example.com  ​

wget
télécharger un fichier
Installation : sudo apt install wget
Exemple : wget   example.com/fichier.zip  ​

ip a (remplace ifconfig)
afficher les interfaces réseau
Exemple : ip a

🔹 Archivage & compression

tar -cvf archive.tar dossier/
créer une archive tar
Exemple : tar -cvf sauvegarde.tar Documents/

tar -xvf archive.tar
extraire une archive tar
Exemple : tar -xvf sauvegarde.tar

gzip/gunzip

compresse/décompresse un fichier zip
Installation : sudo apt install gzip
Exemple : gzip fichier.txt
Exemple : gunzip fichier.txt.gz

zip/unzip
compresse/décompresse en zip
Installation : sudo apt install zip unzip
Exemple : zip archive.zip fichier.txt
Exemple : unzip archive.zip

🔹 Divers utiles

echo
affiche du texte à l’écran
Exemple : echo "Bonjour Linux"

date
affiche la date et l’heure

cal
affiche un calendrier
Installation : sudo apt install bsdmainutils

shutdown -h now
éteint immédiatement la machine
Exemple : sudo shutdown -h now

reboot
redémarre la machine
Exemple : sudo reboot