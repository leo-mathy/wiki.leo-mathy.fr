---
title: Footprinting
description: 
published: true
date: 2024-12-11T09:47:28.881Z
tags: notes, htb, module
editor: markdown
dateCreated: 2024-12-04T07:54:51.478Z
---

# Footprinting

Date de complétion: [XX/XX/XXXX]

# Notes

## Enumeration Principles

Le principe d'énumération désigne la collecte d'information avec des méthodes active et passive.

l'OSINT est une procédure indépendante de l'énumération. (puisque l'OSINT est basé uniquement sur la collecte d'information passive)

L'énumération est une boucle dans laquelle les informations sont collectées à l'aide des informations possédées ou découvertes.

L'information peut être récupérée depuis les domaines, adresses IP, services accessibles...

Une fois les cibles identifiées dans le système cible, il faut examiner les services et protocoles. ces services permettent la communication aux clients, l'infrastructure, l'administration ou encore les employées.

**le but n'est pas d'atteindre les systèmes mais de trouver tous les moyens d'y arriver**

Les 3 grands principes:

- Il y a toujours plus que ce que l'on voit
- Il faut faire la différence entre ce que l'on voit et ce que l'ont ne voit pas
- Il y à toujours un moyen d'obtenir plus d'informations. Il faut comprendre la cible.

## Enumeration Methodology

Les processus complexes doivent avoir des méthodologies standardisées pour ne pas oublier les aspects.

Parfois la méthodologie n'est pas standardisée mais suit une approche basée sur l'expérience.

Une méthodologie statique est possible, celle-ci se compose de 6 couches, et représente les limites à franchir durant le processus d'énumération.

Le processus peut être divisé en 3 différents niveaux (composés de couches):

- énumération basé sur l'infrastructure (Passerelles/Présence sur Internet)
- énumération basé de l'hôte ( Processus/Services accessibles)
- énumération basé sur le système d'exploitation (Système d'exploitation/Privilèges)

Il est possible de directement passer a un niveau différent théoriquement (atteindre directement l'hôte par exemple) avec beaucoup d'efforts. Mais cela n'apporte pas grand chose puisqu'il est possible de ne pas pouvoir aller plus loin (bloqué à un niveau) si la méthodologie n'est pas suivie.

Il faut garder à l'esprit que toutes les failles ne peuvent pas être découvertes et qu'il restera toujours un moyen pour rentrer à l'intérieur du système. Il est impossible d'affirmer à 100% qu'il n'y à plus de failles.

De plus, toutes les failles trouvées au cours de l'énumération ne permettent pas forcément de rentrer à l'intérieur du système.

| Couche                    | Description                                                                                                     | Catégories                                                                                                                                             | but                                                                                                                                                           |
| ------------------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Présence sur Internet  | Identifier la présence sur Internet et de l'infrastructure accessible extérieurement.                           | Domaines, sous-domaines, virtual hosts, cloud, adresses IP, mesures de sécurité, ASN, blocs de réseau...                                               | Identifier tous les systèmes et interfaces cibles qui peuvent être testés                                                                                     |
| 2. Passerelles            | Identifier les possibles mesures de sécurités pour protéger l'infrastructure externe et interne à l'entreprise. | Pares-feu, DMZ, IPS/IDS, EDR, proxies, NAC, segmentation réseau, VPN...                                                                                | Comprendre avec quoi nous avons affaire et ce qu'il faut regarder.                                                                                            |
| 3. Services accessibles   | Identifier les interfaces et services hébergés internes ou externes.                                            | type de service, fonctionnalités, configuration, ports, version, interface...                                                                          | Comprendre la raison de la présence et les fonctionnalités du système cible, obtenir les connaissances pour communiquer et exploiter efficacement le système. |
| 4. Processus              | Identifier les processus internes, ainsi que les sources et destinations.                                       | PID, données traitées, tâches, source, destination...                                                                                                  | Identifier les facteurs et les dépendances entre les processus.                                                                                               |
| 5. Privilèges             | Identifier les permissions et privilèges au niveau des services accessibles.                                    | groupes, utilisateurs, permissions, restrictions, environnement...                                                                                     | Identifier les privilèges et comprendre ce qu'il est possible de faire avec.                                                                                  |
| 6. Système d'exploitation | Identifier les composants internes et la configuration des systèmes.                                            | Type de système d'exploitation, niveau de patch, configuration réseau, environnement du système d'exploitation, fichiers de configuration, fichiers... | Voir comment les administrateurs gèrent les systèmes et quelles informations sensibles l'on peut récupérer.                                                   |

**Une méthodologie est un résumé des procédures systématiques.** Ce n'est pas un guide pas à pas.

Dans notre cas, ce sont les procédures systématiques à appliquer pour explorer une cible donnée.

## Domain Information

Présence sur Internet de l'organisation.

Ce type d'information est récupérée de manière passive. (navigation en tant que client/visiteur). Il faut éviter les connections directes pour limiter l'exposition.

La partie OSINT présentée dans ce module est juste une petite partie de ce qu'il est possible de faire en utilisant ces techniques.

En utilisant une méthode passive il est possible d'utiliser des outils tiers pour mieux comprendre l'organisation.

Lors de l'inspection du site web de l'organisation il faut garder à l'esprit quelles technologies et structures sont nécessaires pour ces services.

Les services peuvent être liés à un secteur spécifique, il est possible de rencontrer un service que l'on ne connait pas, dans ce cas il est nécessaire de le comprendre et de trouver les opportunités qui sont disponibles. Ces services peuvent aussi indiquer comment l'organisation est structurée.

Une fois que l'on a une compréhension basique de l'organisation et de la structure, il est possible d'obtenir une première impression de sa présence sur Internet.

Le premier point de présence sur Internet peut être le certificat SLL. Celui-ci peut contenir plusieurs SAN (Subject Alternative Name), ce qui peut indiquer d'autres domaines (probablement actifs).

Un autre moyen est de récupérer les logs de Transparence de certificat (Certificate Transparency). Ces logs contiennent tous les certificats émis par une autorité de certification à des fins de contrôle (certificats émis à des fins malveillantes pour un domaine).

Les autorités de certifications partages ces informations avec l'interface web crt.sh, qui stocke ces informations pour une récupération ultérieure.

Il est possible de récupérer ces informations sous format json avec la commande suivante:
`curl -s https://crt.sh/\?q\=<domaine>\&output\=json | jq .`

Il est possible de filtrer ces informations pour retirer les domaines tiers (les domaines tiers de pouvant pas être testés sans l'accord du tiers).

Il possible de générer les adresses IP de chaque domaine par la suite.

Shodan est utilisé pour trouver les appareils et systèmes connectés en permanence à Internet. Il scan Internet à la recherche de ports TCP/IP et filtre les découvertes en fonction de critères et de termes.
Cela permet de trouver des appareils comme des caméras IP, des serveurs, des appareils de domotique...

Utiliser Shodan permet de rester en mode passif sans scan actif de notre part.

Rechercher un hôte avec une adresse IP sur Shodan:
`shodan host [IP]`

Après les certificats, il est possible d'afficher les entrées et champs dans le DNS publique.

Récupérer tous les champs DNS pour le domaine spécifié:
`dig any <domaine>`

Les enregistrements de type A contiennent les adresses du domaine donnée,
les enregistrements de type MX contiennent les adresses du serveur mail,
les enregistrements de type NS contiennent les adresses des serveurs DNS qui font autorités pour le domaine,
les enregistrements TXT contiennent des informations en tout genre (SPF,DKIM,DMARC...)

## Cloud Resources

L'utilisation du cloud (GCP, AWS, Azure...) est devenu un composant essentiel de multiples organisations.

Les fournisseurs de services cloud sécurisent leurs infrastructure de manière centralisée, cependant les configurations des administrateurs peuvent mettre en danger les ressources cloud.

Par exemples les S3 Buckets (AWS), Blobs (Azure) et Cloud Storage (GCP) peuvent être accessibles sans authentification si ils sont mal configurés.

Souvent les stockages cloud sont ajoutés à la zone DNS pour faciliter les tâches d'administration.

Il est possible d'utiliser les Google Dorks (inurl,intext...) pour trouver ces ressources cloud de l'organisation, ou encore de regarder le code source des pages web pour voir la source des fichiers (qui peut être stockée sur le cloud).

Domain.glass (https://domain.glass/) permet d'obtenir d'autres informations de manière passive.

buckets.grayhatwarfare (https://buckets.grayhatwarfare.com/) permet d'effectuer une recherche des stockages cloud et de découvrir passivement les fichiers présent sur celui-ci.

Certaines organisations utilisent des abréviations de leurs nom pour le stockage cloud. Il est important de prendre en compte cela lors de la recherche.

Parfois des fichiers sensibles (données,clés privées, certificats...) sont accessibles en libre-accès.

## Staff

Rechercher et identifier les employés sur les réseaux sociaux (LinkedIn,Facebook...) peut révéler de nombreuses informations sur la disposition des équipes et la structure de l'organisation.
Cela peut conduire à la découverte des technologies, langages de programmation ou encore logiciels qui sont utilisées.

En regardant les compétences des personnes sur LinkedIn, leurs post, il est possible de connaitre les travaux actuels de la personne.
De plus, les fiches de recherches de postes des organisations peuvent aussi révéler des informations ou donner des indices.
(ex: Expérience avec la suite Atlassian)
Il est possible de regarder les projets des employés (Github/StackOverflow...) pour obtenir une idée des connaissances de celui-ci.

Les bonnes pratiques des logiciels peuvent indiquer où trouver ce que l'on cherche. (failles...)

Les projets des employés peuvent êtres disponibles sur des plateformes de collaboration de code (github,gitlab...) pour de multiples raisons (partage, portfolio...).
Ces projets peuvent contenir des données sensibles (tokens,clés,emails,adresses...).

LinkedIn est une bonne source d'information puisque ce site regroupe les connections,écoles,compétences,industries,langues,services,noms,titres,entreprises...

Par exemple, en recherchant les personnes dans la sécurité informatique de l'entreprise, il est possible de déterminer les technologies utilisées.

## FTP

Le protocole FTP (File Transfer Protocol) est l'un des protocoles les plus anciens sur Internet. Il opère à la couche TCP/IP (pareil que HTTP).
Il y a aussi des programmes spécifiques pour le protocole FTP (comme par exemples les navigateurs pour le protocole HTTP).

Lors de la communication, le client établi un canal de contrôle avec le serveur sur le port TCP 21. Ensuite le client envoi des commandes au serveur via ce canal et le serveur réponds avec des codes de statut. Ensuite les deux participants établissent un canal de données sur le port TCP 20. Ce canal est utilisé uniquement pour la transmission des données. Si une connexion est interrompue pendant la transmission, le transfert peut recommencer après avoir rétabli le contact.

Il existe une version passive et active de ce protocole,
dans la version active, le client établi la connexion avec un canal de contrôle et indique le port (du client) sur lequel le serveur doit envoyer les réponses (établir le canal de données). Cela pose un problème si le port de réponse défini par le client est bloqué par un pare-feu.
Pour remédier à ce problème, le mode passif à été développé, dans ce mode, le serveur indique au client le port à utiliser pour le canal de données. Comme cette fois c'est le client qui initie la connexion, le pare-feu ne pose pas de problème.

le serveur FTP implémente plusieurs [commandes](https://web.archive.org/web/20230326204635/https://www.smartfile.com/blog/the-ultimate-ftp-commands-list/) et codes [codes](https://en.wikipedia.org/wiki/List_of_FTP_server_return_codes) de statut.

Toutes les commandes de la norme ne sont pas forcements implémentés de manière constante sur les serveur FTP.

**Le Protocole FTP communique en clair, c'est à dire qu'il peut être écouté si les conditions sont présentes.**

Il est possible que le serveur offre la fonction de FTP Anonyme. C'est à dire que le serveur autorise le téléchargement et l'envoi de fichiers sans l'utilisation d'un mot de passe.

Les risques associés au protocole FTP sur un serveur public sont grands et les possibilités limitées.

Le protocole TFTP (Trivial File Transfer Protocol) est plus simple que le protocole FTP, Cependant il ne met pas en place toutes les fonctionnalités du protocole FTP, et ne prend pas en charge l'authentification. De plus TFTP utilise UPD et non TCP, ce qui en fait un protocole peu fiable et donc dépendant de l'implémentation d'un système de récupération au niveau de l'application.

Comme TFTP ne prend pas en charge l'authentification, il défini les limites de l'accès au fichiers seulement en se basant sur les permissions lecture/écriture des fichiers sur le système d'exploitation.

Cela veut dire que TFTP est destiné uniquement aux répertoires avec des fichiers qui sont partagées à tous les utilisateurs.

Du fait du manque de sécurité, TFTP peut être utilisé uniquement sur les réseaux locaux protégés.

Contrairement à FTP, TFTP ne prend pas en charge la fonctionnalité de listage des répertoires.

Quelques commandes TFTP:

| Commande | Description                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------- |
| connect  | Défini l'hôte et optionnellement le port.                                                                   |
| get      | Transfère un ou plusieurs fichiers vers le client.                                                          |
| put      | Transfère un ou plusieurs fichiers vers le serveur.                                                         |
| quit     | Se déconnecte.                                                                                              |
| status   | Affiche le mode de transfère(ASCII/binaire), le statut de la connexion, la valeur de time-out...            |
| verbose  | Active le mode verbose, ce qui affiche des informations supplémentaires pendant les transfères de fichiers. |

L'un des serveurs FTP les plus utilisés est [vsFTPd](https://security.appspot.com/vsftpd.html).

Le fichier de configuration est `/etc/vsftpd.conf`
Le fichier pour refuser certains utilisateurs de l'accès au service FTP est `/etc/ftpusers`

Le fichier de configuration peut être modifié pour l'activation de paramètres dangereux (Connection anonyme...)

Une fois la connexion effectuée, la bannière s'affiche, elle contient la version et la description du service et le type du système.

Les commandes debug,trace et status peuvent être utiles pour obtenir des informations supplémentaires ou voir le fonctionnement détaillé des interactions.

Il est possible de cacher les UID et GUID des fichiers et répertoires avec le paramètre `hide_ids=YES`, cela rend difficile l'identification des droits. Cela est utile lorsque l'on souhaite ne pas afficher quels utilisateurs peuvent télécharger/modifier ces éléments et cacher le nom des utilisateurs locaux.

Si un attaquant récupère le nom des utilisateurs locaux, il peut ensuite effectuer un brute-force à l'aide de ces noms. Cependant les mesures de sécurités comme Fail2ban bloquent les nouvelles tentatives après un certain nombre de tentatives effectuées.

Il y a aussi le paramètre `ls_recurse_enable=YES` qui permet de lister récursivement (avec `ls -R`)les fichiers et répertoires. Cela est utile pour avoir une vue d'ensemble.

L'upload de fichiers sur le serveur FTP (avec `put`)peut aussi rendre vulnérable la machine aux vulnérabilités LFI (Local File Inclusion).

Il est possible de télécharger un fichier avec la commande `get`,
et de télécharger tous les fichiers auxquels l'utilisateur à accès avec la commande `wget -m --no-passive ftp://<utilisateur>@:[mot de passe]@<ip>`
Cependant, il est important de noter que le téléchargement de nombreux fichiers et inhabituel et pourrait déclencher des alarmes.

Le footprinting est possible avec différents outils de scans réseaux. Ces outils permettent d'identifier différents services, même s'ils sont sur des ports différents de ceux par défaut. L'outil le plus utilisé étant Nmap.

Sur ParotOS, les scripts nmap (NSE) sont stockés à l'emplacement `/usr/share/nmap/scripts/`

Par exemple, le script ftp-anon vérifie si le serveur FTP accepte l'accès anonyme. Si c'est le cas, le contenu de la racine FTP est affichée.

Il est possible d'interagir avec le serveur FTP à l'aide de netcat, telnet ou encore openssl si le serveur utilise le chiffrement SSL/TLS.

Interaction avec openssl (permet aussi la récupération des certificats):
`openssl s_client -connect <adresse>:21 -starttls ftp`

## SMB

Le protocole SMB (Server Message Block) permet aux clients de communiquer avec d'autres participants dans le même réseau pour accéder à des fichiers ou des services partagés sur le réseau.
De l'autre côté, le système doit aussi avoir implémenté le protocole et traité la requête en utilisant une application serveur SMB.

Avant cela, les deux parties doivent établir une connexion. C'est pour cela qu'ils s'échangent des messages.

Dans les réseaux IP, SMB utilise le protocole TCP pour cette raison. Il effectue ensuite un three-way-handshake entre le serveur et le client avant que la connexion soit établie. Les spécifications du protocole SMB gouvernent aussi la couche suivante du transport de données.

Le protocole SMB fournit une partie de son système de fichiers local en tant que partages. La visibilité de la hiérarchie visible au niveau du client est partiellement indépendante de la structure sur le serveur.

Les droits d'accès aux partages sont définis par les ACL (Acess Control List). Ces droits peuvent être contrôlés de manière plus granuleuse grâce à des attributs comme "execute","read","full access" définis pour des utilisateurs et groupes.

Les ACL sont basées sur les partages et peuvent ne pas correspondre aux droits assignés localement sur le serveur.

Il y a une implémentation alternative de serveur SMB appelée Samba.
Samba est développé pour les systèmes Unix et implémente le protocole CIFS (un dialecte de SMB).
CIFS est une implémentation spécifique du protocole SMB originellement créée par Microsoft.
Cela permet à Samba de communiquer avec les dernières versions des systèmes Windows.

L'implémentation moderne de ce protocole est souvent référée comme SMB/CIFS.
