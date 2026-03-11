
Le responsable de la DSI vous demande de configurer un routeur (Router32) dont les interfaces sont fa0/0 (192.168.4.50) et fa0/1 (10.0.0.1) afin de connecter un réseau ayant pour IP 192.168.4.0 à un réseau destination d’IP 192.168.5.0. Sachant que l’adresse IP du prochain saut est 10.0.0.2 et que seules les interfaces de ce routeur ne sont pas activées, quelles commandes devez-vous rentrez dans l’invite de commande pour configurer ce routeur afin que les paquets transitent entre les deux réseaux



Solution
Il faut en premier lieu activer les interfaces du routeur :

Router32>enable

Router32#configure terminal

Router32(config)#interface fa0/0

Router32(config-if)#ip address 192.168.4.50 255.255.255.0

Router32(config-if)#no shutdown

Router32(config-if)#end

Router32#configure terminal

Router32(config)#interface fa0/1

Router32(config-if)#ip address 10.0.0.1 255.0.0.0

Router32(config-if)#no shutdown

Router32(config-if)#end

Ensuite, il faut configurer la nouvelle route dans la table de routage :

Router32#configure terminal

Router32(config)#ip route 192.168.5.0 255.255.255.0 10.0.0.2

Router32(config)#end

Router32#write

Pour vérifier que le routeur est bien configuré, nous pouvons alors faire un ping d’un ordinateur du réseau 192.168.4.0 vers un ordinateur du réseau 192.168.5.0.


Réseau sans fil (Wi-Fi);
Un système de distribution sans fil (WDS): permet l'interconnexion sans fil de points d'accès dans un réseau IEEE 802.11 . Il permet d'étendre un réseau sans fil à l'aide de plusieurs points d'accès sans nécessiter de réseau dorsal câblé traditionnel pour les relier.





Router entre 2 routeurs

Qu'est-ce que le routage ?
En réseau, le routage est le processus qui permet de définir le chemin que va emprunter un paquet de données émis par une source pour se rendre vers sa destination.

Voici un exemple pratique pour appliquer tout ce qui a été vu précédemment. Vous apprendrez à configurer deux routeurs pour connecter deux réseaux locaux distincts en utilisant le routage statique dans Packet Tracer.
Topologie :
Deux routeurs connectés via un réseau intermédiaire.
Chaque routeur est connecté à son propre réseau local.
Configuration des réseaux :
Réseau 1 (connecté au routeur A) : 192.168.1.0/24
Réseau 2 (connecté au routeur B) : 192.168.2.0/24
Réseau intermédiaire (entre routeur A et B) : 10.0.0.0/30

Étape 1 : configurer les interfaces des routeurs
Routeur A :
Configurez les interfaces via CLI ou l’interface graphique :
interface GigabitEthernet0/0ip address 192.168.1.1 255.255.255.0
no shutdown
exit 
interface GigabitEthernet0/1
ip address 10.0.0.1 255.255.255.252
no shutdownexit
Vérifiez que les interfaces sont actives avec :show ip interfac
Routeur B :
Configurez les interfaces :
interface GigabitEthernet0/0
ip address 192.168.2.1 255.255.255.0
no shutdownexit 
interface GigabitEthernet0/1
ip address 10.0.0.2 255.255.255.252
no shutdownexit

Étape 2 : ajouter des routes statiques
Sur le routeur A :
Configurez une route pour atteindre le réseau 192.168.2.0/24 via le routeur B :
ip route 192.168.2.0 255.255.255.0 10.0.0.2
Sur le routeur B :
Configurez une route pour atteindre le réseau 192.168.1.0/24 via le routeur A :
ip route 192.168.1.0 255.255.255.0 10.0.0.1

Étape 3 : tester la connectivité
Vérifiez la table de routage
Sur chaque routeur, utilisez la commande suivante pour vous assurer que les routes statiques sont bien configurées :
show ip route
Les routes doivent apparaître avec le préfixe S (Static).
Testez avec un PC dans chaque réseau.
Ajoutez un PC dans le réseau 192.168.1.0/24 et un autre dans le réseau 192.168.2.0/24.
Configurez les adresses IP des PCs et les passerelles correspondantes :
Cliquez sur le PC que vous souhaitez configurer (par exemple, PC1 dans le réseau 192.168.1.0/24).
Une fenêtre s’ouvre, affichant plusieurs onglets. Sélectionnez l’onglet « Desktop ».
Ouvrir l’utilitaire de configuration IP.
Dans l’onglet « Desktop », cliquez sur « IP Configuration ».
Attribuez une adresse IP et une passerelle.
Remplissez les champs comme suit pour PC1 :
IP Address : 192.168.1.10
Subnet Mask : 255.255.255.0 (automatiquement généré après avoir saisi l’adresse IP)
Default Gateway : 192.168.1.1
Fermez la fenêtre une fois les informations saisies.
Répéter pour PC2
Cliquez sur PC2 (dans le réseau 192.168.2.0/24).
Allez dans « Desktop » → « IP Configuration » et configurez :
IP Address : 192.168.2.10
Subnet Mask : 255.255.255.0
Default Gateway : 192.168.2.1
Fermez la fenêtre une fois les informations saisies.

Étape 4 : tester la communication entre PC1 et PC2
Ouvrir le terminal ou l’invite de commande sur PC1.
Dans l’onglet « Desktop » de PC1, cliquez sur « Command Prompt ».
Utiliser la commande ping.
Testez la communication avec PC2 en tapant :ping 192.168.2.10
Résultat attendu : si tout est configuré correctement, vous verrez des messages indiquant que les paquets ont été envoyés et reçus avec succès :
Reply from 192.168.2.10: bytes=32 time<1ms TTL=128
Répéter le test depuis PC2.
Accédez à « Command Prompt » sur PC2.
Testez la communication avec PC1 en tapant :ping 192.168.1.10

Étape 5 : diagnostiquer et corriger les erreurs éventuelles
Problème : aucun ping ne passe entre les réseaux
Vérifiez que les interfaces des routeurs sont activées avec :show ip interface brief
Vérifiez la configuration des routes statiques avec :show running-config
Problème : mauvaise configuration des PCs
Assurez-vous que l’adresse IP et la passerelle des PCs sont correctes.


Rappel
Les protocoles de routage dynamique tels que RIP, OSPF et EIGRP offrent des solutions adaptées à différents types de réseaux. RIP est idéal pour les petits réseaux simples, tandis qu’OSPF est conçu pour les grandes infrastructures. EIGRP, quant à lui, allie rapidité et efficacité, mais est limité aux environnements Cisco. Le choix du protocole dépend de la taille et des exigences du réseau, ainsi que de l’équipement utilisé. Les prochaines sections se concentreront sur leur configuration pratique dans Packet Tracer.

Exercice
Une entreprise, Net Solutions, possède deux succursales : site A et Site B.
Site A est connecté au réseau 192.168.10.0/24, avec le routeur R1 pour gérer le trafic.
Site B est connecté au réseau 192.168.20.0/24, avec le routeur R2 pour gérer le trafic.
Les deux sites sont reliés via une liaison réseau intermédiaire 10.0.0.0/30.
Votre rôle en tant que technicien réseau est de :
Configurer le routage statique entre les deux sites pour assurer la connectivité.
Migrer cette configuration vers le routage dynamique en utilisant RIP.
Vérifier la table de routage et tester la communication entre les deux sites.
Les collaborateurs sur chaque site comptent sur vous pour garantir que les équipements des deux réseaux puissent communiquer sans problème.

Question
Expliquez les étapes nécessaires pour configurer le routage statique sur les routeurs R1 et R2 afin d’interconnecter les réseaux 192.168.10.0/24 et 192.168.20.0/24.

Solution
Configurer les interfaces sur R1 :
Entrez en mode privilégié :
enable
Passez en mode configuration globale :
configure terminal
Configurez l’interface GigabitEthernet connectée au réseau local 192.168.10.0/24 :
interface GigabitEthernet0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit
Configurez l’interface connectée au réseau intermédiaire 10.0.0.0/30 :
interface GigabitEthernet0/1
ip address 10.0.0.1 255.255.255.252
no shutdown
exit

Configurer les interfaces sur R2 :
Entrez en mode privilégié :
enable
Passez en mode configuration globale :
configure terminal
Configurez l’interface GigabitEthernet connectée au réseau local 192.168.20.0/24 :
interface GigabitEthernet0/0
ip address 192.168.20.1 255.255.255.0
no shutdown
exit
Configurez l’interface connectée au réseau intermédiaire 10.0.0.0/30 :
interface GigabitEthernet0/1
ip address 10.0.0.2 255.255.255.252
no shutdown
exit
Ajouter des routes statiques :
Sur R1, ajoutez une route vers le réseau 192.168.20.0/24 via 10.0.0.2 :
ip route 192.168.20.0 255.255.255.0 10.0.0.2
Sur R2, ajoutez une route vers le réseau 192.168.10.0/24 via 10.0.0.1 :
ip route 192.168.10.0 255.255.255.0 10.0.0.1
Vérifier la configuration :Sur R1 et R2, vérifiez que les routes statiques sont bien configurées avec la commande suivante :
show ip route
Testez la connectivité avec la commande ping :
Depuis un PC du réseau 192.168.10.0/24, testez la connectivité avec une machine du réseau 192.168.20.0/24 :
ping 192.168.20.1

Question
Indiquez toutes les commandes nécessaires pour migrer vers un routage dynamique avec RIP et validez que les routes sont apprises dynamiquement.

Solution
Activer RIP sur R1 et R2 :
Sur chaque routeur, entrez en mode privilégié :
enable
Passez en mode configuration globale :
configure terminal
Activez RIP avec un numéro de processus :
router rip
Configurez RIP pour utiliser la version 2 (compatible avec les masques de sous-réseaux) :
version 2
Ajouter les réseaux à RIP :
Sur R1, ajoutez les réseaux connectés directement au routeur :
network 192.168.10.0
network 10.0.0.0
Sur R2, ajoutez les réseaux connectés directement au routeur :
network 192.168.20.0
network 10.0.0.0

Vérifier les routes apprises dynamiquement :
Sur chaque routeur, utilisez la commande suivante pour afficher la table de routage et vérifier les routes RIP :
show ip route
Les routes apprises via RIP apparaîtront avec le préfixe R.

Vérifier les voisins RIP : 
Sur chaque routeur, utilisez la commande suivante pour afficher les voisins RIP :
show ip rip database

Tester la connectivité : 
Depuis un PC du réseau 192.168.10.0/24, testez la connectivité avec un PC du réseau 192.168.20.0/24 :
ping 192.168.20.1



Gère les tables de routage réseau.
ROUTE [-f] [-p] [-4|-6] commande [destination]
                  [MASK masque_réseau]  [passerelle] [METRIC métrique]
                  [IF interface]
  -f             Efface les tables de routage de toutes les entrées
                 de passerelle. Si ceci est utilisé en combinaison avec une
                 des commandes, les tables sont effacées avant l'exécution
                 de la commande.
  -p             Utilisé avec la commande ADD, établit un itinéraire
                 persistant à travers les démarrages du système. Par défaut,
                 les itinéraires ne sont pas conservés quand le système est
                 redémarré. Ignoré pour toutes les autres commandes, qui
                 affectent toujours les itinéraires persistants appropriés.
  -4             Force l'utilisation de IPv4.
  -6             Force l'utilisation de IPv6.

  commande       Une des commandes suivantes :
                   PRINT     Imprime un itinéraire
                   ADD       Ajoute un itinéraire
                   DELETE    Supprime un itinéraire
                   CHANGE    Modifie un itinéraire existant

Exemple> route ADD 192.168.1.1 MASK 255.255.255.0 157.55.80.1 IF 1