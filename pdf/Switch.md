Switch niv. 3


Les étapes de la configuration du switch
Étape 1 : premièrement, allumez chaque interface physique de votre switch (Fa0/1.2.3).
Voici les commandes à effectuer dans le CLI :
Switch >enable (ou « en »)
Switch # conf t (ou configure terminal)
Switch(config) # int fa0/1
Switch(config-if) #no shut (ou no shutdown)
Switch(config-if ) # int fa0/2
Switch(config-if ) # no shut
Switch(config-if )# int fa0/3
Switch(config-if) # no shut
Switch(config-if) # exit
Étape 2 : vous pouvez également renommer le switch.
Commande pour le changement de nom de votre switch dans le CLI :
Switch(config) # hostname commutateur
Complément
Vous observerez, sur l'étape suivante, que le nom est bien changé. Il sera à présent noté « Commutateur » au lieu de « Switch ».
Méthode
Étape 3 : et, enfin, activez le routage sur votre switch.
Commande pour activer le routage de notre switch dans le CLI :
Commutateur(config) # ip routing
Complément
En tapant « ? », vous pouvez facilement retrouver les informations sur les commandes à taper.
Par exemple, pour la commande « ip routing », j'ai tapé « ip ? », et vous pouvez ainsi voir toutes les possibilités de la commande.

Les étapes de la création des VLANs
Étape 1 : mise en place du premier VLAN, le VLAN 10.
Voici les commandes à effectuer dans le CLI :
Commutateur # conf t
Commutateur(config) # vlan 10 (pour le VLAN du PC)
Commutateur(config-vlan) # int fa0/1
Commutateur(config-if) # switchport mode access
Commutateur(config-if) # switchport access vlan 10

Commande pour voir le VLAN mis en place dans le CLI :
Commutateur(config-if) # do show vlan

Étape 2 :
Mise en place du second VLAN, le VLAN 20 :
Voici les commandes à effectuer dans le CLI :
Commutateur(config) # vlan 20 (pour le VLAN du PC)
Commutateur(config-vlan) # int fa0/2
Commutateur(config-if) # switchport mode access
Commutateur(config-if) # switchport access vlan 20

Mise en place du routage inter-VLANs
Les étapes de la mise en place inter-VLANs
Étape 1 : allumez les interfaces de chacun des deux VLANs.
Voici les commandes à effectuer dans le CLI :
Commutateur # conf t
Commutateur(config) # int vlan 10 (et appuyez sur la touche « entrer »)
Puis, pour le VLAN 20, même chose :
Commutateur(config) # int vlan 20 (et appuyez sur la touche « entrer »)

Étape 2 : renseignez ensuite, pour chaque VLAN et interfaces du commutateur niveau 3 (switch), l'adresse IP et le masque sous-réseau pour établir la communication entre les deux VLANs, qui servira donc de passerelle.
Voici les commandes à effectuer :
Commutateur # conf t
Commutateur(config) # int vlan 10 (et appuyez sur la touche « entrer »)
Commutateur(config) # ip address 192.168.10.1 255.255.255.0
(Correspondant à l'adresse réseau du PC qui est en 192.168.10.10 situé sur le VLAN 10).
Puis, pour le VLAN 20, même chose :
Commutateur(config) # int vlan 20 (et appuyez sur la touche « entrer »)
Commutateur(config) # ip address 192.168.20.1 255.255.255.0
(Correspondant à l'adresse réseau du serveur qui est en 192.168.20.10 situé sur le VLAN 20).






[text](switch:%20commande%20%C3%A0%20retenir)

Commandes de base
Un commutateur Cisco possède plusieurs modes d’accès.
Mode utilisateur (>) : consultation seulement.
Mode privilégié (#) : accès aux commandes avancées.
Mode configuration ((config)#) : modification des paramètres.







[text](nfs:%20configurer%20un%20partage%20NFS)

1. Installation du serveur NFS
sudo apt install nfs-kernel-server

2. Configuration des dossiers à partager
sudo nano /etc/exports

/srv/nfs/shared 192.168.1.0/24(rw,sync,no_subtree_check)

3. Démarrage du service NFS
sudo systemctl restart nfs-kernel-server

4. Exportation des partages
sudo exportfs -a

Vérification et Accès Client
sudo mount -t nfsserver_ip:/srv/nfs/shared /mnt/nfs



CONFIGURER UN PARTAGE NFS

sudo apt update
sudo apt install nfs-karnel-server
sudo mkdir -p /mnt/nom_fichier
sudo chown -r nobody:nogroup /mnt/nom_fichier
sudo chmod 777 /mnt/nom_fichier
sudo nano /etc/exports (ajouter [/mnt/nom_fichier 10.221.55.0/24 (rw,sync,no_subtree_check) ] Ctrl x pour enregistrer)
sudo exportfs -ua  -> pour purger
sudo exportfs -a   ->  pour valider la configuration

pour verifier 
sudo showmount -e  10.221.55.7

sur machine client
sudo apt install nfs-common
sudo mkdir /media/nom_repertoir  -> pour creer un repertoir de partage
sudo mount  -t nfs4 10.221.55.7:/mnt/nom_fichier /media/nom_repertoir  -> sans information signifie que tout est bon.
sudo touch test.txt  -> pour tester
sudo ls -l  -> pour verifier






