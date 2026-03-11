#### **Proxy et reverse proxy**





🧭 Proxy vs Reverse Proxy : explication simple et efficace



🔹 Proxy (Forward Proxy)

Un proxy est un serveur intermédiaire placé du côté du client.



🎯 Son rôle

\- Il relaie les requêtes du client vers Internet.

\- Il peut filtrer, cacher (cache), anonymiser ou contrôler l’accès.



🧠 Exemple concret

Tu es dans une entreprise :  

→ Tu veux accéder à un site web.  

→ Ta requête passe d’abord par le proxy de l’entreprise.  

→ Le proxy décide si tu as le droit, garde une trace, ou renvoie une version en cache.



📌 Utilisations courantes

\- Contrôle parental / filtrage web  

\- Anonymisation (masquer l’IP du client)  

\- Cache pour accélérer la navigation  

\- Sécurité interne  



\---



🔹 Reverse Proxy

Un reverse proxy est un serveur intermédiaire placé du côté du serveur.



🎯 Son rôle

\- Il reçoit les requêtes des clients à la place du serveur web.

\- Il distribue ensuite les requêtes vers un ou plusieurs serveurs internes.



🧠 Exemple concret

Tu veux accéder à https://mon-site.com.  

→ Tu arrives sur un reverse proxy (ex : Nginx, HAProxy).  

→ Il choisit quel serveur interne va traiter la requête.  

→ Il renvoie la réponse au client.



📌 Utilisations courantes

\- Load balancing (répartition de charge)  

\- Sécurité (masquer l’infrastructure interne)  

\- Terminaison SSL  

\- Cache côté serveur  

\- WAF (Web Application Firewall)  



\---



🔥 Différence essentielle

| Proxy | Reverse Proxy |

|-------|----------------|

| Placé devant le client | Placé devant le serveur |

| Représente le client | Représente le serveur |

| Cache côté client | Cache côté serveur |

| Filtrage utilisateur | Sécurisation de l’infrastructure |

| Masque l’IP du client | Masque l’IP des serveurs internes |



👉 Le proxy protège le client. Le reverse proxy protège le serveur.



\---



🧩 Sur quelle couche OSI agissent-ils ?



Les deux agissent principalement sur :



🟦 Couche 7 – Application

Car ils manipulent :

\- HTTP / HTTPS  

\- DNS  

\- FTP  

\- etc.



Ils peuvent aussi intervenir sur :



🟩 Couche 4 – Transport

Quand ils font du load balancing basé sur :

\- TCP  

\- UDP  



Résumé OSI :

| Type | Couche OSI |

|------|-------------|

| Proxy | Couche 7 (principalement), parfois 4 |

| Reverse Proxy | Couche 7 (principalement), parfois 4 |



\---



🎤 En bref

\- Proxy : intermédiaire côté client.  

\- Reverse Proxy : intermédiaire côté serveur.  

\- OSI : couche 7 (application), parfois 4 (transport).











🧱 1. Proxy (Forward Proxy)



🎯 Rôle

Un proxy est un intermédiaire entre le client et Internet.  

Il agit pour le client.



🔍 Ce qu’il fait

\- Filtrage (contrôle d’accès, blocage de sites)  

\- Cache pour accélérer la navigation  

\- Anonymisation (masque l’IP du client)  

\- Journalisation (logs)  

\- Sécurité interne  



📌 Exemple

Ton PC → Proxy de l’entreprise → Internet



\---



🧱 2. Reverse Proxy



🎯 Rôle

Un reverse proxy est un intermédiaire entre Internet et les serveurs internes.  

Il agit pour le serveur.



🔍 Ce qu’il fait

\- Load balancing (répartition de charge)  

\- Terminaison SSL  

\- Cache côté serveur  

\- Protection de l’infrastructure (masque les serveurs internes)  

\- WAF (Web Application Firewall)  



📌 Exemple

Client → Reverse Proxy (Nginx/HAProxy) → Serveurs web internes



\---



🔥 3. Différence en une phrase

👉 Le proxy protège le client. Le reverse proxy protège le serveur.



\---



🧩 4. Sur quelles couches OSI ils agissent ?



Les deux peuvent agir sur plusieurs couches, mais principalement :



🟦 Couche 7 – Application

Parce qu’ils manipulent des protocoles applicatifs :

\- HTTP / HTTPS  

\- FTP  

\- SMTP  

\- DNS  

\- etc.



🟩 Couche 4 – Transport

Quand ils travaillent au niveau TCP/UDP :

\- Load balancing L4  

\- Filtrage basique  

\- Redirection de ports  



\---



📊 Résumé OSI



| Type | Couche OSI principale | Couche secondaire |

|------|------------------------|-------------------|

| Proxy | Couche 7 | Couche 4 |

| Reverse Proxy | Couche 7 | Couche 4 |



\---



🧠 Schéma ultra simple



`

Proxy (côté client)

CLIENT → PROXY → INTERNET



Reverse Proxy (côté serveur)

INTERNET → REVERSE PROXY → SERVEURS INTERNES

`











Parfait Papa, je te fais trois exemples ultra concrets avec Nginx, Squid et HAProxy, chacun dans les deux rôles : proxy et reverse proxy.  

Comme ça tu vois exactement comment ça marche dans la vraie vie, côté infra.



\---



🟦 1. Exemple concret avec Squid (Proxy classique – côté client)



Squid est LE proxy historique utilisé dans les entreprises.



🎯 Contexte

Tu veux filtrer et contrôler la navigation des postes internes.



🛠️ Configuration simple (proxy HTTP)

Fichier : /etc/squid/squid.conf



`

http\_port 3128



Autoriser ton réseau interne

acl reseau\_local src 192.168.1.0/24

httpaccess allow reseaulocal



Bloquer Facebook

acl facebook dstdomain .facebook.com

http\_access deny facebook

`



🔍 Résultat

\- Les clients configurent leur navigateur pour utiliser http://proxy:3128

\- Squid filtre, log, met en cache, bloque des sites



👉 C’est un proxy forward : il agit pour le client.



\---



🟩 2. Exemple concret avec Nginx (Reverse Proxy – côté serveur)



Nginx est très utilisé pour exposer des applications web.



🎯 Contexte

Tu as une appli interne sur http://10.0.0.10:8080  

Tu veux l’exposer proprement via https://app.mondomaine.com



🛠️ Configuration reverse proxy

Fichier : /etc/nginx/sites-enabled/app.conf



`

server {

&#x20;   listen 80;

&#x20;   server\_name app.mondomaine.com;



&#x20;   location / {

&#x20;       proxy\_pass http://10.0.0.10:8080;

&#x20;       proxysetheader Host $host;

&#x20;       proxysetheader X-Real-IP $remote\_addr;

&#x20;   }

}

`



🔍 Résultat

\- Le client ne voit jamais l’IP interne

\- Nginx peut ajouter SSL, cache, WAF, load balancing…



👉 C’est un reverse proxy : il agit pour le serveur.



\---



🟥 3. Exemple concret avec HAProxy (Load Balancer + Reverse Proxy)



HAProxy est parfait pour répartir la charge entre plusieurs serveurs.



🎯 Contexte

Tu as 3 serveurs web internes :

\- 10.0.0.11  

\- 10.0.0.12  

\- 10.0.0.13  



Tu veux un point d’entrée unique : https://www.monsite.com



🛠️ Configuration HAProxy

Fichier : /etc/haproxy/haproxy.cfg



`

frontend http\_in

&#x20;   bind \*:80

&#x20;   defaultbackend webservers



backend web\_servers

&#x20;   balance roundrobin

&#x20;   server web1 10.0.0.11:80 check

&#x20;   server web2 10.0.0.12:80 check

&#x20;   server web3 10.0.0.13:80 check

`



🔍 Résultat

\- HAProxy reçoit toutes les requêtes

\- Il les répartit entre les 3 serveurs

\- Il vérifie leur état (check)



👉 Reverse proxy + load balancer (couche 4 ou 7 selon config).



\---



🧩 Résumé visuel



`

CLIENT → Squid (Proxy) → Internet



Internet → Nginx (Reverse Proxy) → Serveur Web



Internet → HAProxy (Reverse Proxy + LB) → Plusieurs serveurs Web

`



\---



🔥 Tu veux aller plus loin ?

Je peux te faire :



\- un schéma ASCII détaillé  

\- une comparaison Nginx vs HAProxy vs Squid  

\- un exemple avec SSL termination  

\- un exemple avec authentification LDAP  

\- un exemple avec cache côté reverse proxy  

\- un exemple avec load balancing L4 vs L7  



Dis-moi ce que tu veux explorer en premier.









#### **Exemple de réalisation pour un chiffrement asymétrique (ou chiffrement à clé publique)**



Étape 1 : installation du paquet pour « gnupg »

sudo apt-get install gpg



Étape 2 : pour commencer à générer une clé :

sudo gpg --full-gen-key



Étape 3 : répondez aux questions

N'hésitez pas à noter les informations que vous saisissez, dans un premier temps.



Étape 4 : confirmation de saisie



Étape 5 : récapitulatif



Étape 6 : recherche du dossier « .gnupg »

ls -al



Étape 7 : exportation de la clé publique

sudo gpg --armor --output pubkey.txt --export \[uid] (\[uid] est à remplacer par le nom de votre certificat, ici c'est « Geoff »)

Étape 8 : visualisation du fichier « pubkey.txt »

Si vous souhaitez voir l'intérieur de votre « pubkey.txt », faites ceci :

cat pubkey.txt



Ici, vous avez deux possibilités :

Celle de l'uploader sur ce que l'on appelle des « keyservers ».

Partager ce fichier « pubkey.txt » avec une autre personne qui va s'en servir pour chiffrer un message. C'est ce que nous allons faire dans le cadre de la démonstration du cours.

Étape 9 : importation du fichier « pubkey.txt » vers le trousseau « gpg ».

Une fois le fichier « pubkey.txt » réceptionné sur une machine tierce, nous allons importer le fichier « pubkey » dans le trousseau « gpg ».

Pour cela, vous allez taper la commande suivante :

sudo gpg –import pubkey.txt



Étape 10 : nous allons procéder au chiffrement d'une courte expression

sudo gpg –encrypt –recipient Geoff Bonjour

« Bonjour.gpg » qui est chiffré.



Étape 11 : envoi du fichier « Bonjour.gpg »



Étape 12 : déchiffrement

sudo gpg –output Bonjour.txt –decrypt Bonjour.gpg

Une fenêtre va s'ouvrir pour vous demander votre « phrase secrète »

Étape 13 : confirmation du bon déchiffrement du message

sudo nano Bonjour.txt



En faisant cet exercice, vous voyez directement comment est chiffré un message. C'est la même chose lors d'une connectivité sécurisée par certificat. La clé publique sert de confirmation pour la connexion : si elle correspond avec la clé privée, vous aurez l'autorisation de vous logger. Si, par contre, il y a une différence, la connectivité sera automatiquement rejetée.







SSL : Secure Socket Layer, plusieurs versions sont sorties de 1994 à 1996, après le SSL 3.0. Celui-ci fût remplacé par le protocole TLS en 1999.



