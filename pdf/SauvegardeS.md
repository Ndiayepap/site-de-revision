#### La Stratégie de Sauvegarde 3-2-1-1-0





🛡️ 

1\. Pourquoi cette stratégie en 2026 ?

Le simple fait de copier ses fichiers sur une clé USB ne suffit plus. Entre les pannes matérielles, les cyberattaques par ransomware (rançongiciels) et les sinistres physiques (vol, incendie), vos données ont besoin d'une protection multicouche.

2\. Le Socle : La règle du 3-2-1

&#x20;\* 3 copies : Conservez toujours vos données en trois exemplaires (l'original + deux sauvegardes).

&#x20;\* 2 supports différents : Utilisez des technologies distinctes (ex: Disque dur 💾 et Cloud ☁️) pour éviter qu'une faille technologique unique ne détruise tout.

&#x20;\* 1 copie hors site : Gardez une sauvegarde géographiquement éloignée de la source (Cloud ou disque chez un tiers).

3\. La Protection Moderne : Le 1-1-0

&#x20;\* 1 copie Hors-ligne (Air-gap) : Un support débranché physiquement de tout réseau. Si le virus ne peut pas atteindre le disque, il ne peut pas le chiffrer. 🔌

&#x20;\* 1 copie Immuable : Un stockage (souvent Cloud) verrouillé logiciellement. Même avec un accès administrateur, les fichiers ne peuvent être supprimés avant un délai défini. 🔒

&#x20;\* 0 erreur : La règle d'or. Une sauvegarde n'est réelle que si elle a été testée. ✅

4\. Ma Check-list de Mise en Place

&#x20;\* Local : Sauvegarder sur un disque externe hebdomadairement, puis le débrancher.

&#x20;\* Cloud : Activer la synchronisation avec option de "versionnage" (historique des fichiers).

&#x20;\* Test : Une fois par mois, tenter de restaurer un fichier au hasard pour vérifier son intégrité.











#### **Mode de Sauvegarde**



Dans ce tutoriel, vous apprendrez à créer des sauvegardes quotidiennes, hebdomadaires et mensuelles sur Ubuntu/Debian à l'aide d'un script. Pour ce faire, nous utiliserons les commandes `tar`, `find` et `rsync`, ainsi que `cron` pour automatiser la tâche.



Sauvegarde quotidienne

La commande tar suivante créera une archive compressée du dossier /var/www/html dans le dossier /home/tony/backup/daily/ . La commande find supprimera toutes les sauvegardes quotidiennes datant de plus de 7 jours.



tar -zcf /home/tony/backup/daily/backup-$ ( date +%Y%m%d ) .tar.gz -C /var/www/html

trouver /home/tony/backup/daily/\* -mtime + 7 -delete

Après les avoir modifiées selon vos besoins, placez ces deux commandes dans un script appelésauvegarde-quotidienne.sh.



Sauvegarde hebdomadaire

La commande tar suivante créera une archive compressée du dossier /var/www/html dans le dossier /home/tony/backup /weekly/ . La commande find supprimera toutes les sauvegardes hebdomadaires datant de plus de 31 jours (ou 1 mois).



tar -zcf /home/tony/backup/weekly/backup-$ ( date +%Y%m%d ) .tar.gz -C /var/www/html

trouver /home/tony/backup/weekly/\* -mtime + 31 -delete

Après les avoir modifiées selon vos besoins, placez ces deux commandes dans un script appelé sauvegarde hebdomadaire.sh.



Sauvegarde mensuelle

La commande tar suivante créera une archive compressée du dossier /var/www/html dans le dossier /home/tony/backup /monthly/ . La commande find supprimera toutes les sauvegardes mensuelles datant de plus de 365 jours (ou 1 an).

tar -zcf /home/tony/backup/monthly/backup-$ ( date +%Y%m%d ) .tar.gz -C /var/www/html

trouver /home/tony/backup/monthly/\* -mtime + 365 -delete

Après les avoir modifiées selon vos besoins, placez ces deux commandes dans un script appelé

sauvegarde mensuelle.sh



Automatisez avec Cron

Vous pouvez créer une tâche cron pour exécuter les scripts de sauvegarde quotidiens, hebdomadaires et mensuels. Ouvrez l'éditeur cron avec le

crontab -e

Saisissez la commande et ajoutez ce qui suit en spécifiant le chemin d'accès complet à vos fichiers de script.

15 0 \* \* \* sh /home/tony/backup-daily.sh   

30 0 \* \* 1 sh /home/tony/backup-weekly.sh    

45 0 1 \* \* sh /home/tony/backup-monthly.sh



Si vous n'êtes pas familier avec la syntaxe de cron, voici ce que nous faisons :



Exécutez le script de sauvegarde quotidien tous les jours à 00h15.

Exécutez le script de sauvegarde hebdomadaire tous les lundis à 00h30.

Exécutez le script de sauvegarde mensuel le 1er de chaque mois à 00h45.



Sauvegarde externe

Ensuite, il est conseillé de copier vos fichiers de sauvegarde locaux sur un autre système. Cette précaution est importante car elle permet de se prémunir contre toute perte d'accès à votre système actuel en cas de compromission.



Nous pouvons créer une image miroir de notre répertoire de sauvegarde local et de tout ce qu'il contient grâce à la commande

rsync .



rsync -a --delete /home/tony/backup/ root@161.35.143.122:/chemin/vers/les/sauvegardes/distantes/

Notez l'option `--delete` ci-dessus. Cela nous permettra de ne pas conserver inutilement sur le serveur distant les sauvegardes que nous avons supprimées localement avec la commande `find` . Autrement dit, /home/tony/sauvegarde/sur le système local sera une image miroir de/chemin/vers/les/sauvegardes/distantes/sur le système distant.



Pour exécuter la commande rsync sans mot de passe, vous devez installer la clé publique sur le serveur distant. Si besoin, consultez cette vidéo .



La dernière chose à faire est de créer une tâche cron pour exécuter la commande rsync.



0 2 \* \* \* rsync -a --delete /home/tony/backup/ root@161.35.143.122:/chemin/vers/les/sauvegardes/distantes/   

Nous exécuterons la commande rsync chaque jour à un moment donné après la génération de toutes les sauvegardes.











#### **Sauvegarde**



**Les differents type de sauvegardes:**



**La sauvegarde complète**

**La sauvegarde complète va vous permettre de copier l’ensemble des fichiers des dossiers du système. À chaque fois que cette sauvegarde est effectuée, elle permet de stocker l’entièreté des données point. Si elle est effectuée plusieurs fois d’affilée, les mêmes données seront stockées plusieurs fois.**



**La sauvegarde incrémentale**

**La sauvegarde incrémentale permet d’effectuer d’abord une première copie complète de toutes les données. Les sauvegardes suivantes ne prendront en compte que les modifications apportées depuis la dernière sauvegarde.**



**La sauvegarde différentielle**

**La sauvegarde différentielle va effectuer, tout comme la sauvegarde incrémentale, une première copie complète de tous les fichiers et dossiers. La sauvegarde suivante permettra de stocker tous les changements apportés depuis la dernière sauvegarde complète.**



**La sauvegarde partielle**

**La sauvegarde partielle consiste à enregistrer uniquement les données ciblées.**



**La sauvegarde miroir**

**La sauvegarde miroir permet de réaliser une copie conforme des fichiers d’un système. Elle permet de récupérer l’ensemble des données sources telles qu’elles étaient présentes lors de la dernière sauvegarde.**





**Bonnes pratiques de sauvegarde**

**Automatisation : automatiser les processus de sauvegarde pour garantir qu’aucune donnée importante ne soit oubliée.**

**Chiffrement : utiliser le chiffrement pour protéger les données (sensibles ou non), en particulier lorsqu’elles sont stockées hors site ou dans le cloud.**

**Formation : former le personnel sur les meilleures pratiques de sauvegarde et sur la manière de réagir en cas de perte de données afin de limiter les erreurs humaines.**

**Hiérarchisation des données : classer les données en fonction de leur importance et de leur criticité, en attribuant des niveaux de priorité pour la sauvegarde.**

**Mise à jour : garder les solutions de sauvegarde à jour pour bénéficier des dernières fonctionnalités et des correctifs de sécurité.**

**Surveillance : mettre en place des systèmes de surveillance pour détecter et résoudre rapidement les problèmes liés aux sauvegardes.**





**Essensiel du PCA et du PRA**

**La stratégie de sauvegarde est essentielle pour garantir la disponibilité et la récupération des données dans le cadre de la continuité des activités (PCA) et de la reprise après sinistre (PRA). Elle consiste à planifier, mettre en œuvre et maintenir des mécanismes de sauvegarde appropriés pour protéger les données critiques.**

**Dans le PCA, la stratégie de sauvegarde vise à créer des copies régulières et cohérentes des données sur des systèmes redondants. Ces sauvegardes permettent une récupération rapide en cas de panne du système principal. La fréquence des sauvegardes peut varier en fonction des besoins, mais elles doivent être planifiées de manière à minimiser la perte de données.**

**Dans le PRA, la stratégie de sauvegarde élargit la portée pour inclure la protection des données critiques contre des événements de grande ampleur tels que les catastrophes naturelles. Elle peut impliquer la création de sauvegardes hors site ou dans des centres de données distants pour une récupération totale du système en cas de destruction du site principal.**





**Différence d'un PME d'un autre**

**Comme la stratégie de sauvegarde fait partie de ces plans et qu’elle-même est différente d’une PME à l’autre, alors le PCA et le PRA d’une PME seront différents d’une autre PME. Le Plan de Reprise d’Activité (PRA) et le Plan de Continuité d’Activité (PCA) sont deux concepts liés à la gestion de la continuité des activités d’une organisation, mais ils ne sont pas nécessairement les mêmes pour toutes les PME. Les PRA et PCA sont conçus pour répondre aux besoins spécifiques et aux risques particuliers de chaque entreprise, et ils peuvent varier considérablement d’une PME à une autre en fonction de plusieurs facteurs (taille de l’entreprise, hiérarchie complexe, secteurs d’activités, réglementaires, budget, ressources temporelles, ressources humaines, identifications de vulnérabilités et failles).**







**Vérification de la restauration :**

**Comparaison avec les données sources : comparer les données restaurées avec les données sources pour vérifier leur similitude. Vous pouvez utiliser des outils de comparaison de fichiers pour cette étape (exemples d’outils : WinMerge, Beyond Compare, KDiif3, Meld, DiffMerge, Araxis Merge, ExamDiff, FileMerge/openDiff, Diffuse, Guiffy, etc.).**



**Outils de suivi : ces outils peuvent fournir des rapports sur l'état des sauvegardes, tester les procédures de restauration et vérifier les journaux d'activité.(Exemples d’outils (sauf scripts) : Veeam Backup\&Replication, Commvault, Veritas Backup Exec, Bacula Entreprise, Nakivo Backup\&Replication, YouBackup Wooxo, Rubrik, Acronus Cyber Backup, Solarwinds Backup, IBM Spectrum Protect , Dell EMC Data Protection Suite, Cobian Backup@Reflector, etc.)**





**Automatiser les sauvegardes : utiliser des outils d’automatisation (ou scripts avec planificateur = Microsoft Task Scheduler ou Linux Crontab) pour planifier et exécuter les sauvegardes en fonction du calendrier établi. Cela garantit une exécution régulière et fiable des sauvegardes.**









**Exemple concret d’un guide calendaire de sauvegarde**

**Entreprise : PME IT-IT, une entreprise de services informatiques offrant des solutions d’infrastructures pour d’autres entreprises.**

**Types de Données :**

**Données clients : inclut les informations client, les historiques d’achat, les données de facturation, etc.**

**Données financières : comprend les données comptables, les relevés bancaires, les rapports financiers, etc.**

**Données employés : contient les dossiers des employés, les informations de paie, les contrats, etc.**

**Données développement : englobe les codes sources, les bases de données de développement, les versions de logiciels, etc.**

**Données de sauvegardes : les sauvegardes, y compris les fichiers système, de configuration, les logs, etc.**

**Niveaux d’importance :**

**Données clients : critique**

**Données financières : critique**

**Données employés : importante**

**Données développement : importante**

**Données de sauvegardes : essentielle**

**Fréquence de Sauvegarde :**

**Données clients : sauvegarde quotidienne**

**Données financières : sauvegarde quotidienne**

**Données des employés : sauvegarde hebdomadaire**

**Données développement : sauvegarde hebdomadaire**

**Données de sauvegardes : sauvegarde quotidienne**

**Calendrier de sauvegarde :**

**Lundi : sauvegarde des données des employés**

**Mardi : sauvegarde des données des employés et des données de sauvegarde**

**Mercredi : sauvegarde des données des employés**

**Jeudi : sauvegarde des données de développement**

**Vendredi : sauvegarde des données clients et des données financières**

**Samedi : sauvegarde des données de développement et des données de sauvegarde**

**Dimanche : sauvegarde des données de sauvegarde**

**Nota :**

**Les sauvegardes quotidiennes sont effectuées en dehors des heures de bureau pour minimiser l’impact sur les opérations en cours.**

**Les sauvegardes hebdomadaires sont programmées pour les jours où l’entreprise est moins active.**

**Les données de sauvegarde système sont essentielles pour garantir la récupération du système en cas de sinistre.**

**Le calendrier est documenté et régulièrement révisé pour s’assurer qu’il répond toujours aux besoins.**

**Cet exemple illustre comment une PME peut établir un calendrier de sauvegardes en fonction des exigences spécifiques pour chaque type de donnée, en tenant compte de leur importance et de la fréquence nécessaire pour minimiser, voire éviter les risques de perte de données.**









**Exemple concret d’un plan de tests de restauration selon les priorités et les contraintes de l’entreprise IT-IT**

**Entreprise : la PME IT-IT est une entreprise de services informatiques offrant des solutions d’infrastructures pour d’autres entreprises.**

**Objectif des tests : assurer que les données critiques de l’entreprise peuvent être restaurées avec succès en cas de sinistre ou de perte de données.**

**Priorités des Données : IT-IT a identifié trois catégories de données critiques : finances, clients et développement.**

**Fréquence des tests (peu importe les ressources attribuées) :**

**Données financières (priorité haute) : test mensuel, le premier vendredi de chaque mois**

**Données clients (priorité moyenne) : test trimestriel, le premier lundi de chaque trimestre**

**Données de développement (priorité basse) : test semestriel, le premier mercredi de chaque semestre**

**Calendrier des tests :**

**Janvier : test des données financières**

**Février : test des données de développement**

**Avril : test des données clients**

**Juillet : test des données financières**

**Août : test des données de développement**

**Octobre : test des données clients**

**Automatisation : les tests de restauration seront effectués et automatisés à l’aide de CRONTAB et de scripts BASH incluant au moins la commande tar -xvzf.**

**Documentation : les résultats de chaque test seront soigneusement documentés et intégrés dans un tableau de type Excel.**

**Formation : le personnel responsable des tests de restauration sera formé en interne par l’ingénieur système (ressource interne).**

**Révision : en janvier de chaque année, le calendrier des tests est révisé pour rester en phrase avec les attentes/besoins.**

**Communication : les fichiers Excel représentant les tableaux de bord sont communiqués à tous les employés et la direction. Une anonymisation et/ou une pseudonymisation des données sont implémentées.**

**En suivant ce plan de programmation des tests de restauration, l’entreprise IT-IT peut permettre à ses données d’être récupérées en cas de besoin, tout en tenant compte de la priorité des données et des contraintes de ressources.**







**Anonymisation et pseudonymisation**

**L’anonymisation rend les données irrécupérables, tandis que la pseudonymisation les masque partiellement**

**Explications**

**L’anonymisation rend les données totalement non identifiables, tandis que la pseudonymisation masque partiellement les données, mais permet potentiellement de les restaurer.**







**Exemple:**

**Création du journal : Fichier texte concernant uniquement la sauvegarde du dossier « Commercial ».**

**Enregistrement des activités :**

**L’horodatage de l'activité : Commencement au 22 septembre 2023 à 22 h 00 et fini le 22 septembre 2023 à 22 h 05**

**Le type de données sauvegardées : 127 001 fichiers Excels (devis, tableau de bord ventes, suivi des entreprises).**

**L'emplacement source et de destination des données :**

**Source : //SUPERMAN/Commercial (superman est le nom d’hôte d’un serveur de fichiers).**

**Destination : //SUPERWOMAN/Commercial (superwoman est le nom d’hôte d’un serveur de sauvegardes de fichiers).**

**Le nom de la personne ou de l'équipe responsable de l'activité : Jean CONNAISPAS**

**Toute remarque pertinente sur l'activité :**

**Fréquence : 1 fois par jour**

**Poids total : 34 927 275 Ko soit 33,26 Go**

**Durée : 272,63 secondes, soit environ 4,54 minutes**

**Identification des incidents : aucun**

**Suivi des modifications : aucune modification.**

**Révision et audit : vérification des sauvegardes précédentes, 1 fois par semaine, le lundi.**

**Conservation des journaux : stocker sur le serveur de fichiers initial : poid actuel du journal = 106,74 Ko au 22 septembre 2023**

**Accès restreint : les employés du service informatique côté équipe système.**









