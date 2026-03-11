


sudo apt-get install apache2
systemctl status apache2 -> vérifier si le serveur web est bien actif.
le IP sur le navigateur pour voir s'il est fonctionnel

Installation de PHP, mariaDB et MySQL
sudo apt-get install php
sudo apt-get install curl
sudo apt-get install mariadb-server
mysql_secure_installation -> entree et encore entree puis y pour configurer un mot de passe
repondre tout Y et renseigner 2 fois le mot_passe.

Se connecter au serveur mariaDB
mysql -u root -p  puis  tapper le mot_passe
create database STUDITEST -> créer une base de donnee.
use STUDITEST -> se connecter à la base de donnee créer. maintenant le server est connecter à la base de donnee.

Création et mise en pratique des tables
create table test (msg text) -> pour créer une autre table.
insert into test values ('coucou') -> pour y inserer un message.
select * from test -> pour contrôler si le message s'affiche.
quit -> pour quitter mariaDB.

Module PHP et vérification de versions
cd /var/www/html -> ls -> on doit voir index.php
touch test.php  -> pour créer un fichier test.php
nano test.php -> pour éditer le fichier.

1 <?php
2 phpinfo() ;    -> pour afficher version de php utilisée.
3 ?>    ctrl + x  -> O -> pour enregistrer et quitter.
Tapper le IP/test.php dans le navigateur pour le verifier.