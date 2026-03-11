Conclusion sur les topologies

Conclusion sur les topologies des réseaux
Les topologies des réseaux ont évolué avec le temps. De nos jours, seules deux topologies subsistent et sont mises en place.

La topologie en étoile est très répandue car elle est facile à configurer, à dépanner et à étendre.

Cependant, on trouve également dans les réseaux devant assurer une qualité de service optimale la topologie maillée. En effet, les réseaux critiques, comme ceux d’entreprises de télécommunications ou d’entreprises devant garantir un service 24 h/24 7 j/7 sont obligés de mettre en place leurs réseaux en redondant le plus possible les liaisons et même les équipements d’interconnexion. Ainsi, elles évitent les interruptions de service.






IP setatique

ncpa.cpl = pour accéder à la configuration d'adresse IP sur Windows.





securité réseau

L’ANSSI (Agence Nationale de la Sécurité des Systèmes d’Information) recommande d’appliquer la politique dite « du pire » et d’autoriser manuellement les connections recensées après analyse.

https://cyber.gouv.fr/sites/default/files/2022/01/anssi-guide-recommandations_securite_architecture_systeme_journalisation.pdf


SNORT : un IDS open source très populaire qui analyse le trafic réseau en temps réel pour détecter des schémas d'attaques connus.
SURICATA : un autre IDS open source capable de surveiller le trafic réseau et de détecter des menaces en utilisant des règles personnalisées.


Snort: open source: 
Snort peut fonctionner en mode IDS (Détection d'Intrusion) pour générer des alertes en cas de détection d'une attaque ou en mode IPS (Prévention d'Intrusion) pour bloquer activement le trafic malveillant.
Juniper networks spécialisé en télécommunications




Rappelons que les IDS et les IPS ne sont pas semblables. Les IDS détectent, les IPS contrôlent en acceptant ou en rejetant des paquets.

Pour l’analyse des fichiers de log, il est intéressant de s’appuyer sur des SIEM (systèmes de gestion des événements et des informations de sécurité) qui permettent l’analyse de log. Ces systèmes permettent de collecter, de consulter et de catégoriser les données recensées pour ensuite les analyser et produire un rapport. Il convient de noter ici que l’interface de Suricata (solution que nous avons vue précédemment dans le cours) propose un SIEM.

Une fois que le seuil des alertes a été défini, il convient de définir ensuite des niveaux de gravité et de priorité. Ces niveaux vont permettre à l’administrateur et à ses équipes de jauger si elle doit être traitée immédiatement ou plus tard.

Pour cela, il est intéressant de définir des niveaux de gravité. Prenons l’exemple suivant :
Niveau 1 : incident critique ayant un impact très élevé
Niveau 2 : incident majeur ayant un impact significatif
Niveau 3 : incident mineur ayant un impact faible

Le fait de définir le niveau de gravité va permettre d’établir une hiérarchie des tickets à traiter. Dans le cadre d’une alerte provenant d’un IPS ou d’un IDS, il est important de définir correctement ses niveaux de gravité, car, en lien direct avec la sécurité d’un réseau, il est nécessaire de traiter ses événements très rapidement.



Il convient ici de rappeler l’importance de l’utilisation des IDS et des IPS dans le cadre de la protection des données.

En matière de conformité avec la sécurité informatique, la responsabilité incombe à l’entreprise de fournir des preuves concernant la protection des données au sein du réseau. À cet égard, l’utilisation et la mise en œuvre de systèmes IDS et IPS s’avèrent essentielles pour satisfaire aux divers critères de sécurité obligatoires en informatique. Il est important de souligner qu’une entreprise peut être sujette à un contrôle, nécessitant ainsi la démonstration de sa conformité à un ensemble de critères définis en sécurité informatique. Ces critères, désignés sous le terme de CIS (Critères du Centre pour la Sécurité Internet), représentent le référentiel des normes de sécurité pour la protection des systèmes informatiques et des données. Ces critères sont subdivisés en deux niveaux distincts :

Niveau 1 : englobe les exigences fondamentales en matière de sécurité, applicables à l’ensemble des systèmes
Niveau 2 : comprend les paramètres de sécurité sous forme de recommandations



L'essentiel
Qu’est-ce qu’une signature ? Un processus permettant de vérifier l’authentification de l’émetteur et de contrôler l’intégrité d’un message dans un fichier, un document ou encore un mail.

Quel est le rôle des IDS et IPS ? Les IDS permettent d’analyser l’ensemble du trafic sur un réseau en comparant l’activité sur ce réseau avec une base de données qui recensent les attaques. Cela permet de détecter une menace existante si celle-ci est répertoriée dans la base de données.

Les IPS agissent eux en prévention et permettent de rejeter des paquets de réseaux en cas de menaces.

Il est important que la base de données soit régulièrement mise à jour avec les dernières menaces d’attaques existantes sur un réseau afin que ces systèmes puissent être efficaces. En fonction des solutions utilisées pour surveiller le réseau, des packages de mise à jour des signatures existent, il convient de les télécharger et de les installer pour que la base de données des signatures soit à jour.

L’administrateur devra programmer des notifications d’alerte afin de pouvoir être averti d’une menace détectée par les IDS et/ou IPS. Il aura également la mission de consulter les événements dans les journaux d’événements afin de pouvoir retracer l’historique des événements. D’où l’importance de la journalisation des événements et de leur centralisation pour simplifier l’archivage de l’historique et la consultation des rapports.

Pour finir, si une intrusion a eu lieu, il convient d’organiser une analyse post-mortem afin de pouvoir faire un bilan et mettre en place des mesures correctives.



Les systèmes IDS :
Les IDS ou Intrusion Detection System est un système de détection d'intrusion utilisé en sécurité informatique pour surveiller les activités sur un réseau ou un système informatique concernant des comportements ou des activités qui pourraient indiquer une intrusion ou une violation de sécurité. L'objectif principal d'un IDS est de détecter les menaces et les attaques potentielles, qu'elles soient internes ou externes, en identifiant des schémas d'activité suspects. Il fonctionne sur un système basé sur des signatures ou sur des comportements suspects. Parmi les outils les plus populaires présents sur le marché, on peut distinguer deux outils bien distincts.

SNORT : un IDS open source très populaire qui analyse le trafic réseau en temps réel pour détecter des schémas d'attaques connus.

SURICATA : un autre IDS open source capable de surveiller le trafic réseau et de détecter des menaces en utilisant des règles personnalisées.

Les systèmes IPS :
Un IPS, ou Intrusion Prevention System, est un système de prévention d'intrusion utilisé en sécurité informatique pour détecter, bloquer et répondre aux tentatives d'intrusion ou aux activités malveillantes sur un réseau ou un système informatique. Contrairement à un IDS qui se contente de détecter les intrusions et de générer des alertes, un IPS est conçu pour prendre des mesures actives pour empêcher ou bloquer ces intrusions. Là aussi, plusieurs outils sont mentionnés comme leaders du marché. Parmi eux on peut retenir deux outils :

Cisco Firepower : un IPS de Cisco qui peut détecter et bloquer les attaques en temps réel par le biais de matériel spécifique mais aussi d’une interface intuitive et très performante.

Palo Alto Networks : offre une solution IPS avancée pour la détection et la prévention des attaques. Moins utilisée que la solution précédente, elle est manageable à souhait par l’élaboration de règles spécifiques et personnalisées.

Les systèmes SIEM :
Un SIEM, (Gestion de l'Information et des Événements de Sécurité en Français), est une solution logicielle ou matérielle qui offre une vue centralisée et une gestion intégrée des informations de sécurité et des événements sur un réseau ou un système informatique. Le SIEM combine la gestion de l'information (SIM, Security Information Management) et la gestion des événements (SEM, Security Event Management) pour fournir une solution complète de surveillance, de détection, d'analyse et de réponse aux menaces et aux incidents de sécurité. La combinaison des deux systèmes (SIM et SEM) offre un rendement de protection très important du fait de la combinaison des deux outils. Il est d’ailleurs tout à fait possible de combiner un IDS et un IPS dans un système SIEM pour bénéficier de l’une des protections les plus abouties du marché actuel.



Les outils les plus populaires permettent de centraliser tous les événements survenus. Parmi eux on peut noter l'existence de deux outils :

Graylog, qui est l'un des outils centralisés de collecte et d'analyse de journaux les plus rapides pour votre pile d'applications, vos opérations informatiques et vos opérations de sécurité.

Fusion SIEM (solution de la société EXABEAM offre une combinaison unique de SIEM et d'Extended Detection & Response (XDR) dans une solution moderne pour SecOps. Il s'agit d'une solution cloud qui vous permet de tirer parti d'une investigation, d'une détection et d'une réponse aux menaces de classe mondiale.



Les Indicateurs de Compromission (IoC) utilisés dans l'identification des attaques
Les Indicateurs de Compromission (IoC) sont des éléments spécifiques et tangibles qui peuvent être utilisés pour identifier une compromission de sécurité ou une attaque informatique. Ils sont essentiels pour la détection précoce des incidents de sécurité et la réponse aux incidents.

Comme pour la détection des attaques, il existe plusieurs niveaux d’attaques et de compromissions des attaques informatiques. Il est donc indispensable de pouvoir identifier comment les attaques informatiques sont apparues et surtout comment peut-on bloquer les futures attaques à venir. Pour cela, il est important de collecter certaines informations à l’aide d’indicateurs appelés IoC afin de pouvoir renseigner la base de données.

Les IoC peuvent capter les informations suivantes :

Adresses IP malveillantes :

Les adresses IP utilisées par des attaquants pour accéder à des systèmes ou des réseaux.

Les plages d'adresses IP associées à des pays ou des régions à haut risque peuvent également être considérées comme des IoC.

Noms de domaine malveillants :

Les domaines de site web ou les noms de domaine utilisés par des attaquants pour héberger des sites web malveillants, des serveurs de Commande et de Contrôle (C&C) ou des liens de phishing.

Fichiers malveillants :

Les fichiers exécutables, les scripts, les documents Office, les PDF, etc., qui ont été identifiés comme malveillants à la suite d'une analyse antivirus ou de l'analyse de sable (sandboxing).

Hash de fichiers malveillants :

Les valeurs de hachage (MD5, SHA-256, etc.) de fichiers malveillants connus.

Ces valeurs de hachage peuvent être utilisées pour vérifier l'intégrité des fichiers et pour les identifier rapidement.

Signatures de logiciels malveillants :

Les signatures spécifiques aux logiciels malveillants, y compris les empreintes numériques, les chaînes de caractères ou les comportements associés à des logiciels malveillants connus.

URL malveillantes :

Les URL utilisées pour diriger les utilisateurs vers des sites web malveillants, des sites de phishing ou des sites d'exploitation de vulnérabilités.

Certificats SSL/TLS compromis :

Les certificats SSL/TLS utilisés par des attaquants pour masquer le trafic malveillant ou tromper les utilisateurs.




Stratégies : Anticipation, bonnes pratiques
Prévenir les intrusions : une nécessité de notre ère numérique
La prévention des intrusions est devenue une préoccupation majeure à l’ère où la cybercriminalité est en constante évolution. Les organisations et les individus doivent adopter des stratégies efficaces pour protéger leurs données sensibles et leur intégrité numérique. Au cœur de cette prévention se trouvent des stratégies et des techniques clairement définies.
Anticipation : l'art de prévoir les attaques
L’anticipation est un élément clé de la prévention des intrusions informatiques. Elle permet de surveiller les CVE (Commons Vulnerabilities Exposures) et les menaces sur différents niveaux. Les équipes de sécurité informatique utilisent des techniques de veille et d’anticipation afin de renforcer la sécurité du SI (Système Informatique).
Cette anticipation demande une veille constante ainsi que des recherches, car de nouvelles vulnérabilités sont découvertes et signalées quotidiennement. Des mesures préventives doivent être mises en place très rapidement afin d’éviter une exposition de données, ou des intrusions.
En général, les patching de sécurité, la sensibilisation, ainsi que la transmission d’informations aux équipes sont de rigueur. Mais il ne faut pas non plus négliger la sensibilisation des utilisateurs. Grâce à l’anticipation, mais aussi à des stratégies et techniques de sécurité, le risque est minimisé et les intrusions sont plus complexes.
Le rôle principal de l’anticipation est justement de rendre l’intrusion et le vol de données plus difficiles, tout en assurant le maintien de l’infrastructure et l’augmentation de la protection passive de l’infrastructure contre les attaques malveillantes.
Bonnes pratiques : les fondations d'une sécurité robuste
La mise en place de bonnes pratiques de sécurité est cruciale pour garantir une protection efficace contre les intrusions et les cybermenaces. Voici quelques bonnes pratiques :
Politique concernant les mots de passeGénéralement, les entreprises ont des politiques de sécurité précises telles que le changement des mots de passe tous les 3 mois et l’impossibilité d’utiliser un mot de passe similaire à un ancien mot de passe. De même, l’utilisation obligatoire de mots de passe complexes et d’outils de 2 FA (Authentification à 2 facteurs) est de rigueur.Cependant, les entreprises n’ont pas de politiques prédéfinies, et font un compromis entre sécurité et confort des employés.
Mise à jour régulière des logiciels (patching de sécurité)Les logiciels utilisés sur les machines peuvent devenir obsolètes, et donc contenir des CVE non patchés. Ce genre de logiciels devient donc une cible facile pour les attaquants. C’est pour cela que les entreprises ont une politique globale de maintien à jour des applications sur les machines, à hauteur d’une mise à jour par mois. Elle est, en général, relativement simple à mettre en place et est gérée par l’équipe de sécurité. Celle-ci effectuera des audits réguliers et des recommandations aux équipes de patching (Administrateurs Système ou DevOps généralement).
Segmentation du réseauLa segmentation du réseau consiste à diviser le réseau en différentes zones distinctes, chaque zone a un accès limité aux autres. L’objectif principal de cette technique permet d'éviter la propagation d’une intrusion à des zones plus sensibles. Cette segmentation est généralement pensée par les architectes réseau, mise en place par les équipes de sécurité et configurée par les administrateurs réseau.
Sensibilisation des utilisateursLes utilisateurs sont très souvent la première ligne de défense contre les attaques. Ce qui oblige donc les entreprises à mettre en place des tests, simulations, ou formations de sécurité. Les simulations d’e-mails de phishing sont très fréquentes dans les entreprises, car elles permettent de sensibiliser les utilisateurs. Les formations, quant à elles, sont réalisées par le biais d’outils de formation en ligne gérés par les équipes de sécurité.
Surveillance continueLa surveillance continue de l'activité du réseau et du système pour détecter les comportements suspects est essentielle. Les outils de détection des intrusions et de sécurité des informations peuvent aider à identifier rapidement les activités malveillantes. Par exemple, si un employé tente de se connecter à un grand nombre de comptes sans succès, cela peut indiquer une tentative de compromission et une alerte doit être générée.




L’humain
Humain : maillon faible ou maillon fort ?
L'élément humain est essentiel dans la prévention des intrusions : il peut être soit le maillon faible, soit le maillon fort de la sécurité d'une organisation.
L’humain comme maillon faible
Manque de sensibilisation : les utilisateurs non informés sont plus susceptibles de subir des attaques, telles que le phishing. Par exemple, un employé ignorant les techniques de phishing pourrait ouvrir un e-mail malveillant et révéler des informations sensibles.
Comportement imprudent : les employés qui ne comprennent pas les risques peuvent prendre des décisions imprudentes, comme télécharger des fichiers à partir de sources non fiables ou connecter des appareils personnels non sécurisés au réseau de l'entreprise.
Mauvaise gestion des mots de passe : l'utilisation de mots de passe faibles ou la réutilisation de mots de passe sur plusieurs comptes peut rendre les comptes vulnérables à la compromission. Par exemple, un employé utilisant « password123 » comme mot de passe constitue un maillon faible en matière de sécurité.
L’humain comme maillon fort
Formation à la sécurité : des employés bien formés peuvent reconnaître les signes de danger, tels que les e-mails suspects, et signaler les incidents de sécurité. Par exemple, un employé formé peut détecter les e-mails de phishing en examinant les expéditeurs et le contenu suspect.
Comportement sûr : les employés soucieux de la sécurité appliquent des mesures de sécurité, telles que vérifier la source avant de télécharger des fichiers ou de cliquer sur des liens. Par exemple, un employé compétent vérifie toujours l’authenticité des sites web avant de saisir des informations sensibles.
Collaboration avec des experts en sécurité : les employés travaillent en étroite collaboration avec les équipes de sécurité pour contribuer à renforcer la posture de sécurité globale de l'organisation. Par exemple, le fait que le service informatique signale rapidement les activités suspectes à l'équipe de sécurité permettra une réponse rapide en cas de compromission.
Bref, le facteur humain est l’élément clé de la sécurité, et il peut être à la fois un atout précieux et une faiblesse. En sensibilisant, en formant les employés et en encourageant une culture de sécurité, les organisations peuvent faire de l'élément humain un élément important de leur stratégie de prévention des intrusions, augmentant ainsi la protection contre les menaces numériques.




Outils communs de défense
Il existe de nombreux outils de défense pour renforcer une infrastructure informatique, voici quelques exemples.
Antivirus et anti-malware : ces logiciels sont utilisés pour détecter et supprimer les logiciels malveillants, notamment les virus, les vers informatiques et les trojans.
Système de détection d'intrusion (IDS) : les IDS surveillent le trafic réseau à la recherche de comportements suspects et génèrent des alertes lorsqu'une activité malveillante est détectée.
Pare-feu : les pare-feux sont essentiels pour contrôler le trafic entrant et sortant de votre réseau. Ils permettent de bloquer les connexions non autorisées.
Système de prévention des intrusions (IPS) : l'IPS va au-delà de la détection en bloquant de manière proactive les connexions ou les comportements malveillants.
Système de gestion des journaux (SIEM) : les SIEM collectent, rassemblent et analysent les données des journaux pour détecter les menaces et les incidents de sécurité.



Les bases
Introduction aux outils de défense
Nous allons explorer différents outils de défense que vous pouvez utiliser pour augmenter la sécurité de votre système informatique. Ces outils sont essentiels pour détecter et prévenir les menaces potentielles, ainsi que pour garantir l’intégrité de vos données. Certains des outils que nous examinerons incluent des listes de blocage, des signatures personnalisées et d'autres mécanismes de protection avancés.
Liste de blocage
Les listes de blocage, aussi appelées listes noires, sont des outils utilisés pour prévenir et restreindre l’accès à certaines ressources ou adresses IP spécifiques. Elles sont utilisées pour bloquer les IP suspectes, celles des utilisateurs non autorisés ou de domaines malveillants. Généralement, les IP bloquées sont mises à jour grâce à des systèmes de transmission par les gestionnaires du logiciel. Ces listes de blocages sont aussi mises à jour suivant les conflits géopolitiques mondiaux, cela souligne bien l’importance de la sécurité informatique à tous niveaux.
Aussi, certaines connexions provenant de pays peuvent être complètement bloquées dans les listes. Par exemple, dans le contexte de la guerre Ukraine-Russie, la plupart des entreprises françaises bloquent les connexions provenant de la Russie, mais aussi des pays alliés à la Russie.
Type de listes de blocage : il en existe différents types, listes d’adresses IP, listes d’applications, et listes de domaines. Elles peuvent servir à bloquer des éléments spécifiques.
Mises à jour régulières : pour être efficace, il est essentiel que ces listes soient mises à jour régulièrement pour inclure de nouvelles menaces potentielles.
Intégration avec pare-feu (firewall) : les listes de blocage sont généralement intégrées avec des pare-feux pour bloquer automatiquement les connexions provenant d’adresses IP ou de domaines figurant sur la ou les listes.
Signatures personnalisées
Les signatures personnalisées sont des règles spécifiques créées pour détecter des attaques ou comportements spécifiques. Ces signatures sont généralement utilisées dans les IDS et IPS que vous verrez plus tard dans le cours.
Création des signatures : elles sont généralement créées par les administrateurs système.
Flexibilité : ces signatures sont tellement flexibles qu’elles peuvent détecter des menaces spécifiques à l’environnement et peuvent aussi être adaptées à des besoins uniques.
Maintenance continue : elles doivent aussi être mises à jour de manière régulière pour éviter de devenir obsolètes et rester efficaces contre les menaces.
Outils communs de défense
Il existe de nombreux outils de défense pour renforcer une infrastructure informatique, voici quelques exemples.
Antivirus et anti-malware : ces logiciels sont utilisés pour détecter et supprimer les logiciels malveillants, notamment les virus, les vers informatiques et les trojans.
Système de détection d'intrusion (IDS) : les IDS surveillent le trafic réseau à la recherche de comportements suspects et génèrent des alertes lorsqu'une activité malveillante est détectée.
Pare-feu : les pare-feux sont essentiels pour contrôler le trafic entrant et sortant de votre réseau. Ils permettent de bloquer les connexions non autorisées.
Système de prévention des intrusions (IPS) : l'IPS va au-delà de la détection en bloquant de manière proactive les connexions ou les comportements malveillants.
Système de gestion des journaux (SIEM) : les SIEM collectent, rassemblent et analysent les données des journaux pour détecter les menaces et les incidents de sécurité.





Il existe 2 types de honeypots.

Les honeypots à haute interaction : ils sont très réalistes et imitent avec une précision chirurgicale les systèmes informatiques. Ils sont très complexes à déployer.

Les honeypots à basse interaction : ils simulent des services spécifiques et sont très simples à gérer.

Les honeypots sont déployables à l’intérieur de votre réseau (honeypots internes) ou à l’extérieur de votre réseau dans une zone démilitarisée (ou DMZ) (honeypot externe). Le choix dépend uniquement des choix de sécurité et de la tolérance aux faux positifs.




Quelques éléments sur les IDS

Les IDS
Un IDS est un équipement qui a pour fonction de contrôler l’activité d’un hôte ou d’un réseau afin de détecter toute intrusion ou tentative d’intrusion. IDS signifie Intrusion Detection System, c’est donc un système de détection d’intrusion.

Les différents types d’IDS
Il existe différents types d’IDS qui sont caractérisés en fonction de leur domaine d’intervention.

Tout d’abord, il existe les HIDS qui sont les détections d’intrusion basées sur l’hôte. Ils analysent uniquement les informations concernant un hôte spécifique. Ils sont habituellement bien plus précis, car ils n’ont pas à analyser tout le trafic d’un réseau, mais uniquement les activités de l’hôte. Comme HIDS connus, vous avez : Watch, Tiger, Security Manager, DragonSquire, etc.

Un autre type d’IDS correspond à ceux basés sur les applications. Ces IDS contrôlent les interactions entre un programme et un utilisateur. Pour ce faire, ils ajoutent des fichiers de log pour fournir plus d’informations sur les activités d’une application spécifique. Il est également facile de filtrer les comportements malveillants, car ces IDS opèrent entre l’utilisateur et le programme surveillé. Ils sont utiles, car ils permettent de surveiller et d’empêcher l’utilisateur d’utiliser des commandes dont il pourrait se servir avec le programme surveillé. Ils sont aussi utiles pour surveiller l’activité d’une application sensible.

Les IDS réseau ou NIDS quant à eux, permettent d’analyser des paquets de données circulant sur un réseau. Pour ce faire, des capteurs sont disposés à des endroits stratégiques d’un réseau, ces capteurs génèrent des alertes si une attaque est détectée. Ces attaques sont par la suite envoyées à une console de sécurité qui analyse et traite l’information envoyée. En général, cette console est positionnée sur un réseau isolé. Parmi les HIDS connus, nous retrouvons Dragon, NFR, Snort ou encore NetRanger.

Enfin, vous avez les NNIDS ou Système de Détection d’Intrusion de Nœud de réseau. Ces IDS fonctionnent de la même manière que les NIDS en analysant les paquets du trafic réseau, la seule différence est qu’ils analysent uniquement les paquets qui sont destinés à un nœud du réseau.

Les deux types de fonctionnements d’un IDS
Il est important de distinguer deux éléments dans le fonctionnement d’un IDS : le mode détection et la réponse apportée. Deux types de détection existent, à savoir la détection d’anomalie et la reconnaissance de signature. La détection d’anomalie vise à détecter une anomalie par rapport à une base de trafic habituel. La reconnaissance de signature vise, quant à elle, à analyser et rechercher dans l’activité de l’élément surveillé s’il existe des traces d’attaques connues.

Focus sur les IPS
Un IPS est un système de prévention des intrusions. Il vise donc à anticiper une attaque dès qu’une trace reconnaissable est repérée. Un système IPS examine les paquets entrants et sortants et analyse chaque transaction. Il effectue un ensemble d’analyses de détection sur les paquets à un l’échelle individuelle, mais également sur les conversations et motifs du réseau.

Les éléments constitutifs d’un IPS
Chaque produit IPS, pour qu’il reçoive l’appellation IPS, doit regrouper des fonctionnalités essentielles, lesquelles sont au nombre de 6. Tout d’abord, un IPS doit comprendre les réseaux IP que ce soit les protocoles utilisés, les architectures, etc. Mais, il doit également comprendre les couches Application du modèle OSI.

Deuxièmement, il doit avoir une connaissance des serveurs dédiés et de leur architecture logicielle.

Troisièmement, il doit maitriser les sondes réseau et pouvoir analyser les logs. Ceci pour permettre de détecter les attaques et d’écrire les scripts de commande à destination des pare-feux.

Ensuite, il faut qu’il puisse fonctionner à une certaine vitesse afin de ne pas impacter négativement les performances et la disponibilité du réseau.

Autre élément indispensable : la compréhension des besoins client pour que la politique de défense mise en œuvre soit en fonction de ces derniers.

Enfin, dernier élément, il doit pouvoir fonctionner en mode statefull inspection, ce qui permet de connaître à tous les instants le contexte de l’analyse en cours.