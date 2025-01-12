---
title: Footprinting
description: 
published: true
date: 2025-01-12T16:30:50.921Z
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

CIFS est considérée comme une version spécifique du protocole SMB, cette version s'aligne principalement avec SMBv1.

Quand des commandes SMB sont transmises en utilisant Samba vers un service NetBios plus ancien, la connexion va utiliser les ports 137,138 et 138.
En revanche, CIFS utilise le port 445 exclusivement.

Il y a des nouvelles version de SMB comme SMBv2 et SMBv3, ces versions offrent des améliorations et sont préférés dans des environnements plus modernes.

SMBv1 (CIFS) est considéré comme dépassée mais peut encore être utilisée dans des environnements spécifiques.

Avec la version 3 de Samba, le serveur Samba peut être un membre complet d'un Active Directory.
Dans la version 4 de Samba, le serveur Samba peut être un contrôleur de domaine Active Directory.

Pour implémenter le rôle d'Active Directory, le serveur Samba est composé de plusieurs services pour effectuer cette tâche. Le service smbd (service serveur SMB) et le service nmbd (service NetBIOS message Block). Le service SMB contrôle ces deux programmes d'arrières plan.

Samba est donc approprié pour les systèmes Windows et Linux.

Dans un réseau, chaque hôte participe au même workgroup. Un Workgroup est le nom d'un groupe qui identifie une collection arbitraire de systèmes et leurs ressources sur un réseau SMB. Il est possible d'avoir plusieurs workgroups dans un même réseau à n'importe quel moment.

IBM à développé une API appelée NetBIOS (Network Basic Input/Output System), cette API fournie un plan à une application pour se connecter et partager des données entre ordinateurs.

Dans un environnement NetBIOS, quand une machine passe en ligne, elle nécessite un nom, ce qui est fait en passant par la procédure d'enregistrement de nom.

Chaque hôte réserve son nom sur le réseau ou bien le serveur de nom NetBIOS est utilisé. Cela à été amélioré avec [le Service de noms Internet Windows](https://networkencyclopedia.com/windows-internet-name-service-wins/)

Samba offre de nombreux paramètres que l'on peut configurer grâce au [fichier de configuration](https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html)

En regardant les paramètres du service il faut se demander ce que les employés et attaquants peuvent gagner de l'activation de ces paramètres.

Certains paramètres peuvent être sensibles voir dangereux, par exemple `browseable = yes` permet de lister les partages disponibles, `guest ok = yes` autorise les connexions sans mot de passe ou encore `create mask = 0777 `qui défini les permissions des nouveaux fichiers.

`smbclient -N -L //<ip>` permet de lister les partages du serveur en utilisant une session nulle (accès anonyme), donc sans utiliser de mots de passe ou d'utilisateur.

Il est possible de faire `!<commande>` pour exécuter une commande sur le client dans une session avec smbclient.

Sur le serveur Samba, il est possible d'utiliser smbstatus pour voir les connexions, l'hôte et le partage auxquels le client est connecté.

Nmap peut être utilisé énumérer le service. Il est cependant recommandé d'effectuer une énumération manuelle.

Pour interagir manuellement avec le service SMB et envoyer des requêtes spécifiques il est possible d'utiliser rpcclient. Cet outil effectue des fonctions MS-RPC.

rpcclient offre de nombreuses requêtes qui exécutent des fonctions spécifiques sur le serveur SMB.

Ces fonctions sont disponibles [ici](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html).

Parmi ces fonctions, il est possible de lister les partages(`netshareenumall`), d'énumérer les utilisateurs(`enumdomusers`/`queryuser <RID>`)...

Il est aussi possible de brute-force les RID des utilisateurs (si la liste des utilisateurs n'est pas possible par exemple). Un outil permettant cela est [samrdump.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/samrdump.py).

Des alternatives à rpcclient peuvent être [smbmap](https://github.com/ShawnDEvans/smbmap), [CrackMapExec](/Outils/Linux/CrackMapExec) ou encore [enum4linux-ng](https://github.com/cddmp/enum4linux-ng).

Il est nécessaire d'utiliser des outils variés pour l'énumération puisque certains outils peuvent ne pas retourner les mêmes résultats (différence lié à la programmation de l'outil). Dans ce cas une vérification manuelle est nécessaire.

Il est déconseillé de se baser sur un outil automatisé dont on ignore comment il a été écrit.

## NFS

NFS (Network File System) est un système de fichier en réseau développé par Sun Microsystems et a le même but que SMB. Le but est l'accès aux fichiers depuis un réseau comme si ils étaient en local. Cependant il utilise un protocole complètement différent. NFS est utilisé pour la communication entre les systèmes Linux/Unix. Cela veut dire que les clients NFS ne peuvent pas directement communiquer avec des serveurs SMB. NFS est un standard Internet qui gouverne les procédures dans un environnement de fichiers distribués.

Tandis que NFSv3 authentifie l'ordinateur client, avec NFSv4, le système est désormais pareil que SMB avec une authentification utilisateur.

- NFSv2 est plus ancien mais supporté par beaucoup de systèmes, il fonctionnait originellement entièrement avec UDP.
- NFSv3 à plus de fonctionnalités comme la taille des fichiers variable et un meilleur rapport des erreurs. Mais il n'est pas compatible entièrement avec NFSv2.
- NFSv4 inclus Kerberos, fonctionne sur Internet et a travers les pares-feu, supporte les ACL, fournit des performances supplémentaires et un niveau de sécurité accru. C'est la première version à implémenter un protocole à état.

NFSv4 vise à implémenter un support pour le protocole, pour l'utilisation dans les clusters de serveurs. cela inclut la fonctionnalité d'accès distribué à travers de multiples serveurs (pNFS). De plus, cette version ajoute un mécanisme "session trunking", aussi connu sous le nom de NFS multipathing.

De plus, avec la version 4, un seul port est utilisé par le service, le port 2049 TCP ou UDP, ce qui simplifie son utilisation à travers les pares-feu.

NFS est basé sur le protocole ONC-RPC/SUN-RPC, exposé sur le port TCP et UDP 111. ce protocole utilise la représentation externe des données (XDR), ce qui permet un échange des données indépendant du système.

Le protocole NFS n'a pas de mécanisme d'authentification ou d'autorisation, l'authentification est gérée au niveau du protocole RPC et l'autorisation est dérivée du système de fichiers.

Le serveur est responsable de la traduction des informations utilisateur du client dans le format du système de fichier et de la conversion des autorisations dans le format UNIX.

La méthode la plus commune d'authentification est via les UID/GUID et l'appartenance aux groupes.

La NFS Export Table contient une table des systèmes de fichiers physiques accessibles par le client ainsi que les options.

Certaines options comme rw,insecure,nohide... sont dangereuses.

Par exemple:
`/mnt/nfs  10.129.14.0/24(sync,rw,no_subtree_check)`
permet le partage de /mnt/nfs en lecture et écriture à tous les systèmes dans le réseau 10.129.14.0/24.

Pour énumérer le service NFS, les ports 111 et 2049 sont essentiels.

Le script nmap NSE rpcinfo peut récupérer la liste de tous les services RPC en cours d'exécution.

Affiche la liste des partages NFS disponibles sur un serveur:
`showmount -e <ip>`

Monte le partage NFS 10.129.14.128:/ dans le dossier cible ./target-NFS/
`sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock`

Démonte le partage
`umount ./target-NFS`

## DNS

Domain Name System (DNS) est une grande partie d'Internet. C'est un système de résolution de noms en adresses IP. Ce système ne possède pas une base de données centrale. L'information est distribuée vers des serveurs DNS.

Il y a de nombreux types de serveurs DNS utilisés dans le monde.
| Type | Description|
| -- | -- |
| DNS Root Server (Serveur racine DNS) | Les serveurs racine DNS sont responsables des domaines de premier niveau (TLD). En dernière instance, ils sont uniquement interrogés si le serveur de noms de réponds pas. C'est l'interface centrale entre les utilisateurs et le contenu sur Internet. C'est l'ICANN qui coordonne les serveurs racines. Il y a 13 serveur racines dans le monde. |
| Authoritative Nameserver (serveur de noms faisant autorité) | Les serveurs de noms faisant autorité sont responsables d'une zone particulière, ils répondent uniquement aux requêtes dans leurs zone. Si un serveur de noms faisant autorité ne peut pas répondre à une requête, le Root Server s'en occupe. |
| Non-authoritative Nameserver (Serveur de noms ne faisant pas autorité) | Les serveurs de noms ne faisant pas autorité ne sont pas responsables d'une zone particulière, ils collectent l'information de zones DNS spécifiques. Cela est fait en utilisant des requêtes DNS itératives ou récursives. |
| Caching DNS Server (Serveur DNS Cache) | Les serveurs DNS Cache stockent les informations d'autres serveurs de noms pour une certaine période (la période est définie par les serveurs de noms faisant autorité). |
| Forwarding Server (Serveur de transfert) | Les serveurs de transfert ont une fonction unique, ils redirigent les requêtes DNS vers un autre serveur DNS|
| Resolver (Résolveur) | Les résolveurs effectuent une résolution de nom localement sur le système. |

Le protocole DNS est en grande partie non chiffré, cela pose des problèmes de confidentialité (les FAI/appareils sur le réseau local peuvent voir en clair les requêtes).

Pour chiffrer ces requêtes, il est possible d'utiliser DNS over TLS (DoT) ou DNS over HTTP (DoH). Il est aussi possible d'utiliser DNSCrypt pour chiffrer la communication entre le serveur de nom et le client.

Le DNS ne traduit pas uniquement des noms en adresses IP. Il permet aussi de stocker et publier des informations supplémentaires sur les services associés à un domaine (par exemple pour indiquer l'adresse du serveur de messagerie).

Différents enregistrements DNS avec plusieurs fonctions associés sont utilisables.

| Type d'enregistrement DNS | Fonction                                                                                     |
| ------------------------- | -------------------------------------------------------------------------------------------- |
| A                         | Retourne l'adresse IPv4 du domaine demandé.                                                  |
| AAAA                      | Retourne l'adresse IPv6 du domaine demandé.                                                  |
| MX                        | Retourne le serveur de messagerie responsable du domaine demandé.                            |
| NS                        | Retourne les serveurs DNS (NameServers) du domaine.                                          |
| TXT                       | Retourne des informations diverses (DMARC,DKIM,SPF...)                                       |
| CNAME                     | Est utilisé comme alias pour un autre nom de domaine.                                        |
| PTR                       | Associe une adresse IP à un nom de domaine.                                                  |
| SOA                       | Donne des informations sur la zone DNS correspondante et l'adresse du contact administratif. |

Tous les serveurs DNS utilisent 3 types différents de fichiers de configuration:

- fichiers de configuration locale du serveur DNS
- fichiers de zones
- fichiers de résolution de nom inverse

Sur les serveurs Linux, le serveur DNS Blind9 est souvent utilisé. Son fichier de configuration named.conf est divisé en deux sections, la configuration générale et les entrées de zone.

Les options globales affectent toutes les zones et une option de zone affecte uniquement une zone. Les options de zone sont prioritaires sur les options globales.

Les zones définies dans le fichier sont divisés dans des fichiers individuels, les fichiers de zone.
Un fichier de zone décrit une zone DNS dans le format BIND.
Un fichier de zone est composé au minimum d'un enregistrement NS et SOA.

Si le fichier est considéré comme inutilisable (par exemple à cause d'une erreur de syntaxe), la réponse du serveur lors des requêtes vers cette zone sera un message SERVERFAIL.

Pour traduire les adresses IP en FQDN, le serveur DNS doit avoir un fichier de résolution de nom inverse. Dans ce fichier le FQDN est assigné à la partie hôte de l'adresse IP grâce à un enregistrement PTR.

Il y a de nombreux paramètres dangereux sur un serveur Bind9, comme `allow-recursion` (défini les hôtes qui ont le droit d'effectuer des requêtes récursives), `allow-transfer` (défini les hôtes qui ont le droit de recevoir des transferts de zone) ou encore `allow-query` (défini les hôtes qui peuvent faire des requêtes au serveur).

L'énumération d'un serveur DNS se base sur les réponses aux requêtes envoyées.

Il est possible de récupérer les enregistrements NS pour savoir quels autres serveurs de noms sont connus.

Avec dig, pour spécifier un résolveur de nom, il faut utiliser le caractère "@". Par défaut, le résolveur précisé dans le système sera utilisé.

Récupère les enregistrements ns de la zone mydomain.tld en interrogeant un serveur spécifique.
`dig ns mydomain.tld @<ip du résolveur>`

Parfois il est aussi possible de récupérer la version du serveur DNS en récupérant un enregistrement TXT de classe CHAOS.
`dig CH TXT version.bind <ip du résolveur>`

Pour récupérer toutes les zones DNS d'un résolveur avec Dig, il faut utiliser l'option ANY.
`dig any mydomain.tld @<ip du résolveur>`

Le Transfer de zone représente le transfère de zones vers un autre serveur DNS, cela se produit généralement sur le port TCP 53. La procédure pour effectuer cela se nomme Asynchronous Full Transfer Zone (AXFR).

Les transfères de zone utilisent une clé secrète appelle rndc-key (présente dans le fichier de configuration global sur Bind9).

Le transfère de zone transfère des fichiers ou enregistrements et détecte les écarts dans les jeux de données des serveurs.

Les données originales d'une zone sont présentes sur le serveur DNS Primaire pour la zone (Primary). Les serveurs où les zone sont transférés sont appelés serveurs DNS secondaires pour la zone (Secondary).

Un serveur DNS qui sert de source directe pour la synchronisation d'un fichier de zone est appelé Maître (Master).
Un serveur DNS qui obtient les données d'une zone depuis un Master est appelé Esclave (Slave).

Une serveur DNS Primaire pour une zone est toujours un Maître alors qu'un serveur DNS Secondaire peut être un Maître ou un Esclave.

Les esclaves récupèrent l'enregistrement SOA de la zone à certaines intervalles (refresh time), et compare les numéros de série. Si le numéro de série de l'enregistrement SOA du Maître est plus grand que celui de l'esclave alors les données ne sont plus égales.

Si l'option allow-transfer est définie sur un sous-réseau ou sur any, alors n'importe qui peut récupérer le fichier de zone, ce qui peut autoriser la récupération d'autres zones ou encore la possibilité de récupérer des noms et adresse IP internes.

Pour récupérer les transfères de zones avec Dig:
`dig axfr <domaine> @<ip du résolveur>`

Il est possible aussi de brute-force les sous-domaines, un outils parmi d'autres pour cela est [dnsenum](https://github.com/fwaeytens/dnsenum).

## SMTP

Le protocole SMTP (Simple Mail Transfer Protocol) est un protocole d'envoi de mail dans un réseau IP.

Il peut être utilisé entre un client mail et un serveur mail ou entre deux serveurs SMTP (Si la communication s'effectue entre deux serveurs, alors un des deux est client et l'autre serveur).

Le protocole SMTP est souvent utilisé avec les protocoles IMAP ou POP3, pour l'envoi et la récupération des mails.

Les serveurs SMTP servent uniquement à envoyer et rediriger des mails.

Par défaut les serveurs SMTP écoutent sur le port 25. Cependant les serveurs plus récents écoutent aussi sur le port 587 pour la réception des mails depuis des serveurs/utilisateurs authentifiés, normalement en utilisant la commande STARTTLS (pour passer d'une connexion en clair à une connexion chiffrée).

Au début de la connexion, l'authentification se produit lorsque le client confirme son identité (avec un nom d'utilisateur et un mot de passe). Les mails peuvent ensuite être transmis.

Pour transmettre un mail, le client transmet au serveur l'adresse du serveur d'origine et du/des destinataire(s), le contenu du mail et d'autres informations/paramètres. Après la transmission du mail, la connexion se termine et le serveur envoi le mail à un autre serveur SMTP.

Par défaut, SMTP fonctionne sans chiffrement et transmet les commandes,données ou encore informations d'authentification en clair.

Pour palier à cela, SMTP peut être utilisé avec un chiffrement SSL/TLS. Le serveur peut utiliser un port différent du port 25 pour cela, par exemple le port 465.

- avec le port 587, la connexion démarre en clair, puis le client demande au serveur de passer en mode chiffré avec la commande STARTTLS.
- avec le port 465, la connexion est chiffrée dès le premier échange entre le client et le serveur.

Cependant il est conseillé d'utiliser le port 587 avec STARTTLS puisqu'il permet aux clients et serveurs qui ne supportent pas le chiffrement de fonctionner en mode "fallback" et que le port 465 à été déprécié.

Une fonctionnalité essentielle d'un serveur SMTP est la prévention du spam en utilisant des mécanismes d'authentification qui permettent uniquement aux utilisateurs autorisés d'envoyer des mails.
Pour cela, la plupart des serveurs SMTP modernes supportent l'extension du protocole SMTP, ESMTP (Extended SMTP) avec SMTP-Auth.

- Lors de l'envoi d'un mail, le **client SMTP** aussi connu sous le nom **Mail User Agent (MUA)** **convertit le mail en un header et un body**, puis **envoi les deux** au serveur SMTP.
- Sur le serveur SMTP, le **Mail Transfer Agent (MTA)**, est **responsable de l'envoi et de la réception des mails**. Le MTA vérifie ensuite la taille et si le mail est un spam ou non puis le stocke. Le MTA va ensuite **récupérer l'adresse IP du serveur de réception** depuis le DNS.
- Occasionnellement, cette tâche de vérification peut être **déléguée à l'avance** au Mail Submission Agent (MSA). Le MSA va vérifier la validité de l'email (origine du mail). Le MSA est **aussi appelé serveur Relais** (Relay Server). Une attaque de type "Open Relay Attack" est souvent disponible sur de nombreux serveurs SMTP à cause de configurations incorrectes.
- Une fois le mail reçu par le **serveur SMTP de destination**, les paquets sont réassemblés pour former un mail complet.
- Le **Mail delivery agent (MDA)** transfère le mail **vers la boite aux lettres** de destination.

Mail User Agent (MUA) 🡆 Mail Submission Agent (MSA) 🡆 Mail Transfer Agent (MTA) 🡆 Mail delivery agent (MDA) 🡆 Boite aux lettres

SMTP à deux désavantages inhérents au protocole réseau:

- L'envoi des mails en utilisant SMTP ne retourne pas d'information concernant la confirmation de livraison. Bien que les spécifications du protocole prévoient ce type de notification, son format n'est pas spécifié par défaut, de sorte que généralement seul un message d'erreur en anglais, comprenant l'en-tête du message non remis, est renvoyé.
- Les utilisateurs ne sont pas authentifiés lorsqu'une connexion est établie, l'expéditeur du mail est donc peu fiable. C'est pour cela que les relais SMTP sont souvent utilisés pour l'envoi de spam en masse, souvent à l'aide de mail spoofing. Pour prévenir cela, de nombreuses techniques sont disponibles, comme par exemple le rejet de mails ou la mise en quarantaine grâce protocole SPF ( Sender Policy Framework) et [DKIM](http://dkim.org/) (DomainKeys).

C'est pour cela que l'extension à SMTP, ESMTP (Extended SMTP) à été développé. En général c'est cette extension qui est désignée lorsque le protocole SMTP est abordé.
ESMTP utilise TLS, ce qui est fait après la commande EHLO en envoyant STARTTLS. Ce qui initialise la connexion SMTP chiffrée. Après cela, les extensions d'authentification en clair (AUTH PLAIN) peuvent être utilisés de manière sécurisée.

Pour communiquer avec le serveur SMTP (via un client de messagerie par exemple), il est nécessaire d'utiliser des commandes spéciales.
Suite à l'envoi d'une commande, le serveur va répondre sous forme de codes retour (un peu comme le protocole HTTP).
Ces codes sont consultables [ici](https://serversmtp.com/smtp-error/).

| Commande    | Description                                                                                                                                                                                                                                                          |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AUTH PLAIN  | AUTH est une commande provenant de l'extension SMTP, ESMTP (Extended SMTP). Permet d'authentifier le client.                                                                                                                                                         |
| HELO / EHLO | Le client se connecte en utilisant le nom de son ordinateur et démarre la session. EHLO est utilisé avec les extensions de SMTP (ESMTP par exemple) et retourne la liste des fonctionnalités supportés par le serveur.                                               |
| MAIL FROM   | Le client spécifie l'expéditeur de l'e-mail.                                                                                                                                                                                                                         |
| RCPT TO     | Le client spécifie le destinataire de l'e-mail.                                                                                                                                                                                                                      |
| DATA        | Le client initie la transmission de l'e-mail.                                                                                                                                                                                                                        |
| RSET        | Le client interrompt la transmission en cours mais maintient la connexion avec le serveur.                                                                                                                                                                           |
| VRFY        | Le client vérifie si une boîte aux lettres est disponible pour le transfert de messages. Peut aussi être utilisé pour l'énumération les utilisateurs (en fonction de la configuration serveur, celui-ci pourrait confirmer l'existence d'un utilisateur inexistant). |
| EXPN        | Le client vérifie également si une boîte aux lettres est disponible pour le messagerie.                                                                                                                                                                              |
| NOOP        | Le client demande une réponse du serveur pour éviter la déconnexion due à un time-out.                                                                                                                                                                               |
| QUIT        | Le client termine la session.                                                                                                                                                                                                                                        |

Pour interagir avec le serveur SMTP, il est possible d'utiliser telnet pour initialiser une connexion TCP avec le serveur.

`telnet [adresse IP] 25`

Il est possible de communiquer vers un serveur mail au travers un proxy web, (possiblement avec la version HTTP/1.0 )

Le header d'un mail comporte de nombreuses informations utiles, comme l'horaire d'expédition, le format ou encore les serveurs qui ont redirigés le mail. Cependant **le header du mail ne contient aucune information nécessaire à la livraison technique**. Les informations nécessaires à la livraison technique sont transmises dans une partie du protocole de transmission.

Pour éviter le filtrage des mails (et donc la non réception des mails par le destinataire), l'expéditeur peut utiliser un serveur relais en qui le destinataire a confiance.

Le relais est un serveur SMTP connu et vérifié par tous les autres. Lors de la connexion au serveur relais, l'expéditeur doit s'authentifier avant de l'utiliser sauf dans certains cas où des adresses IP ou plages d'adresses spécifiques sont préautorisées.

Dans Postfix, le paramètre suivant peut être utilisé pour indiquer les adresses IP ou les plages d'adresses qui sont autorisées à utiliser le serveur comme relais sans authentification.
`mynetworks = [adresses IP / les plages d'adresses]`

Un relais ouvert correspond à un relais SMTP ou tout le monde est autorisé à utiliser le serveur comme relais sans authentification.

Sur Nmap, les scripts par défaut (-sC) incluent le script **smtp-commands**, ce script va utiliser la commande EHLO pour afficher toutes les commandes qui peuvent être exécutés sur le serveur SMTP.
`nmap [adresse IP] -sC -p25`

Il est aussi possible d'utiliser le script [smtp-open-relay](https://nmap.org/nsedoc/scripts/smtp-open-relay.html) pour vérifier si le serveur est un relais ouvert grâce à 16 tests.
`nmap [adresse IP] -p25 --script smtp-open-relay -v`

Enumérer les utilisateurs du serveur SMTP avec une liste et un timeout de 30secondes.
`smtp-user-enum -M VRFY -U [fichier utilisateurs] -t [IP] -v -w 30`

## IMAP / POP3

Le protocole IMAP (Internet Message Access Protocol) permet l'accès aux mails depuis un serveur. Contrairement à POP, IMAP de manager des mails directement sur le serveur et supporte les structures sous forme de dossier.
IMAP est donc un protocole client-serveur de management en ligne (les modifications sont opérés sur le serveur) de mails sur un serveur distant et permet de synchroniser un client mail local avec la boite aux lettres sur le serveur. IMAP peut être vu comme une sorte de protocole de système de fichier en réseau pour mails.
Cela permet une synchronisation à travers de nombreux clients indépendants.

Au niveau de POP3, celui-ci peut uniquement lister,récupérer et supprimer des mails du serveur. IMAP doit donc être utilisé pour des fonctionnalités additionnelles (dossiers sur le serveur, accès à de multiples boites aux lettres durant la même session, présélection des mails (synchronise uniquement les e-mails spécifiques en fonction de critères tels que la date, les indicateurs, la taille ou les dossiers pour optimiser les performances et l'utilisation des ressources)...)

Les clients peuvent donc avoir accès à ces structures en ligne et créer des copies locales.

IMAP est basé sur du texte (commandes et réponses lisible par l'homme) et possède des fonctionnalités avancées (parcourir les mails directement sur le serveur, accès en simultané au serveur...)

Sans connexion active au serveur mail, manager les mails devient impossible. C'est pour cela que certains clients offrent un mode hors-ligne avec une copie locale de la boite aux lettres. Le client synchronise ensuite tous les changements quand la connexion est rétablie.

Le client établi la connexion au serveur via le port 143. Pour communiquer, le client utilise des commandes lisible par l'homme encodés en ASCII.

Plusieurs commandes peuvent être envoyés à la suite sans attendre la confirmation du serveur pour chacune.
Les confirmations reçues par la suite, peuvent être associées aux commandes envoyées, en utilisant les identifiants envoyés lors de la commande. Cela permet d'associer la confirmation reçue à la commande envoyée.

Au début de chaque connexion, l'utilisateur est authentifié sur le serveur avec un nom d'utilisateur et un mot de passe. L'accès aux boites aux lettres désirées est uniquement possible après une authentification.

En copiant les mails envoyés vers un dossier IMAP, tous les clients ont accès aux mails envoyés depuis la boite aux lettres. Sans prendre en compte depuis quel poste le mail à été envoyé.

Par défaut, la communication avec IMAP entre un client et un serveur n'est pas chiffrée (transmission des mails,noms d'utilisateurs, mots de passe en clair). Beaucoup de serveurs requièrent l'établissement d'une session IMAP chiffrée, c'est SSL/TLS qui est normalement utilisé pour cela.
La connexion IMAP utilise le port 143 par défaut, ou le port 993 ou un port alternatif, en fonction de la méthode et de l'implémentation utilisée.

Pour tester/examiner ces protocoles, il est possible d'utiliser les paquets (apt) dovecot-imapd et dovecot-pop3d.

**Le terme boite aux lettres (au sens IMAP) correspond a un dossier (au sens de la plupart des clients de messagerie).** Le numéro précédant la commande correspond à l'identifiant à utiliser lors de la réponse du serveur.
**Les commandes IMAP sont les suivantes:**

| Commande                                               | Description                                                                                   |
| ------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| `1 LOGIN <nom d'utilisateur> <mot de passe>`           | S'authentifie au serveur avec un nom d'utilisateur et un mot de passe.                        |
| `1 LIST "" *`                                          | Lister tous les répertoires.                                                                  |
| `1 CREATE "<boite aux lettres>"`                       | Créer une boite aux lettres.                                                                  |
| `1 DELETE "<boite aux lettres>"`                       | Supprimer une boite aux lettres.                                                              |
| `1 RENAME "<boite aux lettres>" "<boite aux lettres>"` | Renommer une boite aux lettres.                                                               |
| `1 LSUB "" *`                                          | Retourne le nom des boites aux lettres que l'utilisateur à déclaré comme actives ou abonnées. |
| `1 SELECT <boite aux lettres>`                         | Sélectionne une boite aux lettres pour accéder aux mails contenus dans celle-ci.              |
| `1 UNSELECT <boite aux lettres>`                       | Quitte la boite aux lettres sélectionnée.                                                     |
| `1 FETCH <ID> all`                                     | Récupère les données associés à un message.                                                   |
| `1 CLOSE`                                              | Supprime tous les messages avec le flag "Deleted".                                            |
| `1 LOGOUT`                                             | Termine la connexion avec le serveur.                                                         |

**Les commandes POP3 sont les suivantes:**

| Commande                   | Description                                                                   |
| -------------------------- | ----------------------------------------------------------------------------- |
| `USER <nom d'utilisateur>` | S'identifie au serveur avec un nom d'utilisateur.                             |
| `PASS <mot de passe>`      | S'authentifie au serveur avec un mot de passe.                                |
| `STAT`                     | Récupère le nombre de mails sur le serveur.                                   |
| `LIST`                     | Récupère le nombre et la taille des mails sur le serveur.                     |
| `RETR <id>`                | Demande au serveur l'envoi du mail par son ID.                                |
| `DELE <id>`                | Demande au serveur la suppression du mail par son ID.                         |
| `CAPA`                     | Demande au serveur d'afficher ses fonctionnalités.                            |
| `RSET`                     | Demande au serveur d'annuler les modifications effectuées dans cette session. |
| `QUIT`                     | Termine la connexion avec le serveur.                                         |

**Certains paramètres présents sur les serveurs de messagerie peuvent être dangereux. En voici quelques-uns:**

| Setting                   | Description                                                                                                                                      |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `auth_debug`              | Active les logs de debug pour l'authentification.                                                                                                |
| `auth_debug_passwords`    | Ajuste la verbosité des logs. Peut enregistrer les mots de passe, la méthode d'authentification.                                                 |
| `auth_verbose`            | Log les tentatives d'authentifications ratés et leurs raison.                                                                                    |
| `auth_verbose_passwords`  | Les mots de passe pour l'authentification sont loggés, ils peuvent être tronqués.                                                                |
| `auth_anonymous_username` | Spécifie le nom d'utilisateur pour la connexion anonyme sans authentification avec le mécanisme SASL (Simple Authentication and Security Layer). |

Voici un tableau des ports par défaut utilisé par les deux protocoles:

| Port  | Description                                                             |
| ----- | ----------------------------------------------------------------------- |
| `143` | Port utilisé par IMAP.                                                  |
| `993` | Port utilisé par IMAP, basé sur SSL/TLS pour chiffrer la communication. |
| `110` | Port utilisé par POP3.                                                  |
| `995` | Port utilisé par POP3, basé sur SSL/TLS pour chiffrer la communication. |

Pour interagir avec un serveur IMAP(S)/POP3(S), il est possible d'utiliser curl, openssl, ou netcat:
`curl -k 'imaps://<Adresse IP>' --user <utilisateur>:<mot de passe> -v`
`openssl s_client -connect <Adresse IP>:imaps`
`openssl s_client -connect <Adresse IP>:pop3s`

# SNMP

SNMP (Simple Network Management Protocol) est un protocole qui permet de surveiller/gérer les appareils réseau, gérer les tâches de configuration et changer les paramètres à distance.

SNMP peut être entre autres, utilisé sur des serveurs,routeurs,switchs,appareils IoT...

La dernière de ce protocole est SNMPv3.

En plus de l'échange d'information, le client SNMP peut aussi transmettre des commandes de contrôle en utilisant des agents sur le port UDP 161.

De plus, dans une communication classique, le client effectue les requètes vers le serveur. En plus de cette communication classique, le protocole SNMP prend en charge les traps via le port UDP 162. C'est à dire que le serveur va envoyer des paquets au client sans que celui-ci ne les demande explicitement (notifications d'évenements). Si l'appareil est configuré pour l'utilisation de traps, alors une trap SNMP est envoyée au client une fois qu'un évenement spécifique se produit sur le serveur.

Pour que l'échange d'information se produise entre un client et un serveur SNMP, les objets SNMP doivent avoir une adresse unique connue de chaque côté. Ce méchanisme d'adresse est impératif pour transmettre des données avec SNMP.

Pour s'assurer que le protocole fonctionne à travers de multiples fabricants et combinaisons de client/Serveur, le MIB (Management Information Base) a été créer. MIB est un format indépendant pour le stockage d'information d'appareils.
Le MIB est un fichier texte qui contient la liste (ordonée sous forme arborescence) des objets SNMP pouvant être récupérés.
Le fichier MIB contient au moins un identifieur d'objet (Object Identifier)(OID), qui en plus de l'adresse unique et le nom, fournit les informations concernant le type,les droits d'accès et la description de l'objet.
Les fichiers MIB sont écrits dans le format ASN.1 (Abstract Syntax Notation One), ce format est basé sur l'encodage ASCII.
Le MIB ne contient donc aucune donnée mais il défini où la trouver et à quoi cette donnée ressemble (ce qui correspond aux valeurs de l'oid).

Un OID représente un noeud dans un espace de nom hiérarchique. Une séquence de nombres unique identifie chaque noeud, ce qui permet à la position du noeud dans l'arboréscence d'être déterminé. Plus la séquence de nombres est longue plus l'information est spécifique. Beaucoups de noeuds dans l'arboréscence OID contiennent uniquement des références aux noeuds enfants..
Les OID sont composés de nombres entiers et sont le plus souvent concaténé par une notation en points. 
Il est possible de voir les MIB associés aux OID dans l'[Object Identifier Registry (OIR)](https://www.alvestrand.no/objectid/)

La version 1 de SNMP (SNMPv1), est la première version du protocole et est toujours utilisée dans des petits réseaux. Cette version supporte la récupération d'information depuis des appareils, la configuration des appareils et les traps.
En revanche, SNMPv1 n'a pas de système d'authentification embarqué. Cela signifie que n'importe qui ayant accès au réseau peut lire/modifier les données. De plus, SNMPv1 ne supporte pas le chiffrement de la communication.

SNMPv2 existe en plusieurs version. La version qui éxiste toujours est la version v2c ("c" pour community-based). Au niveau de la sécurité, SNMPv2 est pareil que SNMPv1 et à été etendu avec des fonctionnalités additionnelles tiers qui ne sont plus utilisées. Le problème le plus important de cette version est que la "community string" qui permet une authentification basique, est transmise en clair. 

Avec SNMPv3, la sécurité à été grandement améliorée, avec des mesures de sécurité comme une authentification avec un nom d'utilisateur et un mot de passe ou encore le chiffrement de la communication avec une clé partagée. Cependant la compléxité augmente aussi avec de nombreuses options supplémentaires disponibles par rapport à SNMPv2c.