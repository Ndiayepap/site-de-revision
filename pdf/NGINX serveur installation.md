### **NGINX serveur: installation**



Réputé pour son architecture.

Apres avoir mis a jour le systeme

sudo apt-get istall nginx (-y ou OUI)

cd /etc/nginx -> ls -> pour se deplacer dans ce dossier

cd sites-available

nano default -> pour changer server\_name par notre nom\_domaine

cd -> pour sortir 

on va se deplacer dans /var/www pour configurer la page d'accueille

cd html/ -> pour y acceder

ls et nano index...html pour editer

localhost ou 127.0.0.1 sur la barre de recherche pour afficher la page





### Essentiel ###

Nginx est un serveur web en pleine croissance qui attire de plus en plus de webmasters dans le monde.

Par rapport à Apache et à d'autres serveurs web, Nginx est de loin supérieur en termes de gestion des sessions simultanées, de temps de réponse et d'utilisation des ressources.

Cela est dû à l'architecture et à la gestion intelligente des connexions. L'une des principales fonctions est l'équilibrage des charges, qui permet une mise à l'échelle plus rapide des serveurs http.

L'équilibrage de la charge par Nginx permet de répartir le trafic entre différents serveurs, ce qui permet aux utilisateurs de développer leurs applications et de réaliser des allers-retours http en même temps.









### Création de clés RSA avec OpenSSL



openssl genrsa -out tototo.pem 1024

Cette commande s'occupera du processus de création des fichiers de clés, c'est-à-dire de nos clés privée et publique. Le nom toto va être le nom de notre clef qui est obtenue au format PEM ça veut dire (Privacy Enhanced Mail en format en base 64) et le numéro 1024 va être la taille exprimée en bits



Dans le cas où nous souhaiterions voir l'affichage des clés RSA nous devons utiliser la commande:

openssl rsa -in tototo.pem -text -noout.

Cette commande rsa va permettre de visualiser le contenu d'un fichier au format PEM.



Chiffrement d'un fichier de clés privées RSA

Il n'est pas du tout sûr de laisser les clés à découvert, surtout les clés privées. Ce que nous pouvons faire avec la commande RSA, c'est crypter les clés. Nous avons trois options (-des, -des3 et -idea) qui vont spécifier l'algorithme de cryptage symétrique à utiliser, dans notre cas nous allons utiliser la commande -des3.



La commande à exécuter pour le cryptage d'un fichier de clés privées RSA est la suivante :

openssl rsa -in tototo.pem -des3 -out tototo.pem

Comme vous pouvez le voir dans la capture ci-dessous, une phrase sera demandée afin de générer une clé symétrique qui protégera l'accès à la clé que nous avons créée. La même clé devra être saisie deux fois, car une confirmation de la clé est sollicitée.



Ce que nous allons faire maintenant est l'exportation de notre clé publique afin qu'elle puisse être partagée avec d'autres, et pour cela nous devrons utiliser la commande suivante :

openssl rsa -in tototo.pem -pubout -out tototoPublique.pem

Puis il faudra entrer notre passphrase pour confirmer



Dans ce bloc, nous allons procéder à la vérification de l'exportation de notre clé publique.

openssl rsa -in tototoPublique.pem -pubin





