---
title: Footprinting
description: 
published: true
date: 2025-01-18T15:49:08.149Z
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

## SNMP

SNMP (Simple Network Management Protocol) est un protocole qui permet de surveiller/gérer les appareils réseau, gérer les tâches de configuration et changer les paramètres à distance.

SNMP peut être entre autres, utilisé sur des serveurs,routeurs,switchs,appareils IoT...

La dernière de ce protocole est SNMPv3.

En plus de l'échange d'information, le client SNMP peut aussi transmettre des commandes de contrôle en utilisant des agents sur le port UDP 161.

De plus, dans une communication classique, le client effectue les requêtes vers le serveur. En plus de cette communication classique, le protocole SNMP prend en charge les traps via le port UDP 162. C'est à dire que le serveur va envoyer des paquets au client sans que celui-ci ne les demande explicitement (notifications d'évènements). Si l'appareil est configuré pour l'utilisation de traps, alors une trap SNMP est envoyée au client une fois qu'un évènement spécifique se produit sur le serveur.

Pour que l'échange d'information se produise entre un client et un serveur SNMP, les objets SNMP doivent avoir une adresse unique connue de chaque côté. Ce mécanisme d'adresse est impératif pour transmettre des données avec SNMP.

Pour s'assurer que le protocole fonctionne à travers de multiples fabricants et combinaisons de client/Serveur, le MIB (Management Information Base) a été créer. MIB est un format indépendant pour le stockage d'information d'appareils.
Le MIB est un fichier texte qui contient la liste (ordonnée sous forme arborescence) des objets SNMP pouvant être récupérés.
Le fichier MIB contient des identifiants d'objet (OID) et fournit des informations essentielles sur chaque objet, telles que son adresse unique, son nom, son type de données, ses droits d'accès et une description détaillée.
Les fichiers MIB sont écrits dans le format ASN.1 (Abstract Syntax Notation One), ce format est basé sur l'encodage ASCII.
Le MIB ne contient donc aucune donnée mais il défini où la trouver et à quoi cette donnée ressemble (ce qui correspond aux valeurs de l'oid).

Un OID représente un nœud dans un espace de nom hiérarchique. Une séquence de nombres unique identifie chaque nœud, ce qui permet à la position du nœud dans l'arborescence d'être déterminé. Plus la séquence de nombres est longue plus l'information est spécifique. Beaucoup de nœuds dans l'arborescence OID contiennent uniquement des références aux nœuds enfants.
Les OID sont composés de nombres entiers et sont le plus souvent concaténé par une notation en points.
Il est possible de voir les MIB associés aux OID dans l'[Object Identifier Registry (OIR)](https://www.alvestrand.no/objectid/)

**La version 1 de SNMP (SNMPv1)**, est la première version du protocole et est toujours utilisée dans des petits réseaux. Cette version supporte la récupération d'information depuis des appareils, la configuration des appareils et les traps.
En revanche, SNMPv1 n'a pas de système d'authentification embarqué. Cela signifie que n'importe qui ayant accès au réseau peut lire/modifier les données. De plus, SNMPv1 ne supporte pas le chiffrement de la communication.
**SNMPv2** existe en plusieurs version. La version qui existe toujours est la version v2c ("c" pour community-based). Au niveau de la sécurité, SNMPv2 est pareil que SNMPv1 et à été étendu avec des fonctionnalités additionnelles tiers qui ne sont plus utilisées. Le problème le plus important de cette version est que la "community string" qui permet une authentification basique, est transmise en clair.
Avec **SNMPv3**, la sécurité à été grandement améliorée, avec des mesures de sécurité comme une authentification avec un nom d'utilisateur et un mot de passe ou encore le chiffrement de la communication avec une clé partagée. Cependant la complexité augmente aussi avec de nombreuses options supplémentaires disponibles par rapport à SNMPv2c. C'est pour cela que de nombreuses organisations utilisent encore SNMPv2.

Les "community string" peuvent être vues comme des mots de passe, qui déterminent si les informations demandés sont accessibles.

Pour tester et voir le fonctionnement en détails de SNMP, il est possible d'utiliser [snmpd](http://www.net-snmp.org/docs/man/snmpd.conf.html).

Certains paramètres SNMP sont dangereux, en voici quelque-uns:

| Command                                          | Description                                                                          |
| ------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `rwuser noauth`                                  | Autorise un accès complet à l'arborescence OID sans authentification.                |
| `rwcommunity <community string> <adresse IPv4>`  | Autorise un accès complet à l'arborescence OID en fonction d'où la requête provient. |
| `rwcommunity6 <community string> <adresse IPv6>` | Autorise un accès complet à l'arborescence OID en fonction d'où la requête provient. |

Pour analyser le protocole SNMP, il est possible d'utiliser entre autres, les outils snmpwalk, Onesixtyone et braa.
snmpwalk est utilisé pour envoyer des requêtes pour récupérer les informations de l'OID.

Onesixtyone pour réaliser des attaques par force brute sur les noms des "community string":
`onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt <adresse IP>`

Braa pour réaliser des attaques par force brute sur les OID individuelles et énumérer les informations derrières celles-ci:
`braa <community string>@<adresse IP>:<OID>`

## MySQL

MySQL est un RDBMNS (Relational Database Management System) open-source développé et supporté par Oracle. Une base de données est une collection structurée de données organisées pour un usage et une récupération facile. Le système de gestion de base de données peut rapidement et avec performance, traiter un grand volume de données.

La base de données est contrôlée en utilisant le langage SQL. MySQL fonctionne sur une architecture client-serveur, le serveur étant le DBMS.
Les données sont stockés dans des tables, contenant des colonnes, des lignes et des types de données. Ces bases de données sont souvent stockés dans un fichier unique avec une extension ".sql".

Les clients MySQL peuvent récupérer et éditer les données en utilisant des requêtes vers le moteur de base de données. L'insertion, la suppression, la modification et la récupération des données se fait avec le langage SQL.

MySQL peut être utilisé pour l'administration de multiples bases de données, vers lesquelles les clients peuvent envoyer de multiples requêtes simultanément. En fonction de l'usage de la base de données, l'accès est possible via un réseau interne ou depuis Internet.

MySQL convient pour les applications où une syntaxe efficiente et des hautes vitesses de réponses sont essentielles.

MySQL est souvent utilisé avec un OS Linux, PHP et un serveur web Apache, cette combinaison est connue sous le nom de [LAMP](<https://en.wikipedia.org/wiki/LAMP_(software_bundle)>) (Linux, Apache, MySQL, PHP), ou avec Nginx, [LEMP](https://lemp.io/) (Linux, Nginx, MySQL, PHP).
L'utilisation d'une base de données MySQL pour l'hébergement web, permet aux scripts PHP de stocker leurs données (mots de passe, permissions, liens, utilisateurs, emails, clients...).
Les données sensibles ( par exemple les mots de passe) peuvent être stockés en texte clair dans la base de données, cependant ces données sont généralement chiffrés par le script PHP avant l'insertion dans la base avec une méthode sécurisée comme le chiffrement à sens unique (hash).

La base de données MySQL traduit les commandes en internes, en code exécutable et effectue les actions demandés. L'application peut en informer l'utilisateur (ce qui peut arriver avec de l'injection SQL) en cas d'erreur.
Ces messages peuvent apporter des informations importantes et confirmer que l'application web interagi avec la base de données dans un sens différent imaginé du développeur.

SQL peut aussi être utilisé pour la gestion des utilisateurs et le changement de la structure des tables.

MariaDB est un fork du code original de MySQL. Cela est du au développeur en chef de MySQL qui quitta l'entreprise MySQL AB après son acquisition par Oracle, pour développer un autre DBMS basé sur le code source de MySQL.

L'administration des bases de données est un vaste sujet, les structures peuvent devenir très grandes rapidement et leur planification peut devenir compliquée. C'est pour cela que des professions à part entière y sont destinées, comme le métier d'administrateur de bases de données. C'est donc une compétence primaire pour les développeurs logiciels et aussi les analystes en sécurité de l'information.

Les possibilités de configuration de MySQL sont vastes, les options principales avec un impact sur la sécurité sont les suivantes:

| Paramètre        | Description                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------- |
| user             | Défini l'utilisateur pour l'exécution du service MySQL.                                                 |
| password         | Défini le mot de passe associé à l'utilisateur pour l'exécution du service MySQL.                       |
| admin_address    | Spécifie l'adresse IP sur laquelle écouter les connexions TCP/IP sur l'interface réseau administrative. |
| debug            | Spécifie les paramètres du débug.                                                                       |
| sql_warnings     | Spécifie si en cas d'erreur au niveau de l'insertion d'une ligne unique, une information est retournée. |
| secure_file_priv | Spécifie le paramètre pour limiter l'effet des opérations d'importation et d'exportation de données.    |

Les paramètres debug et sql_warnings sont utilisés pour retourner des informations en cas d'erreur. Ces messages d'erreurs sont sensibles et sont souvent affichés sur le navigateur en retour.

Toutes les informations entrées dans le fichier de configuration sont en texte clair.
Si il y a un moyen de voir le contenu du fichier (par exemple avec des droits mal configurés sur le fichier), alors il est possible, à partir du paramètre user et password, de récupérer les données de la base.

Le serveur MySQL écoute par défaut sur le port 3306.
Le port MySQL peut être scanné avec Nmap (Il est nécessaire de vérifier les informations manuellement, puisque certaines peuvent être des faux positif):
`nmap <adresse IP> -sV -sC -p3306 --script mysql*`

Il est possible de avec la commande suivante:

Les bases de données les plus importantes sur un serveur MySQL sont la [base système](https://dev.mysql.com/doc/refman/8.0/en/system-schema.html#:~:text=The%20mysql%20schema%20is%20the,used%20for%20other%20operational%20purposes) ("sys") et la base de schéma d'information ("information_schema").
La base système contient les tables, informations et métadonnées nécessaires à l'administration du serveur.
La base de schéma d'information est également une base contenant des métadonnées, mais ces métadonnées sont principalement récupérées depuis la base système. L'existence de ces deux bases repose sur le respect du standard ANSI/ISO.
Contrairement à SQL Server, où le catalogue système est spécifique à Microsoft et fournit des informations plus détaillées, sur MySQL, la base système et la base de schéma d'information remplissent des rôles distincts mais complémentaires.

Voici les commandes utiles principales pour interagir avec MySQL:

| Command                                                            | Description                                                     |
| ------------------------------------------------------------------ | --------------------------------------------------------------- |
| `mysql -u <utilisateur> -p <mot de passe> -h <adresse IP>`         | se connecter au serveur MySQL.                                  |
| `show databases;`                                                  | Afficher toutes les bases de données.                           |
| `use <base de données>;`                                           | Sélectionner une base de données existante.                     |
| `show tables;`                                                     | Afficher toutes les tables disponibles dans la base de données. |
| `show columns from <table>;`                                       | Afficher toutes les colonnes de la table spécifiée.             |
| `select * from <table>;`                                           | Afficher la table spécifiée.                                    |
| `select * from <table> where <colone> = "<chaîne de caractères>";` | Rechercher une chaîne de caractères dans la table spécifiée.    |

Retrouver les [bonnes pratiques MySQL](https://dev.mysql.com/doc/refman/8.0/en/general-security-issues.html)

## MSSQL

Microsoft SQL est un RDBMNS (Relational Database Management System) Microsoft développé pour les environnements Windows, contrairement à MySQL, il n'est pas open-source.
MSSQL est populaire parmi les administrateurs et développeurs pour le développement d'applications dotnet puisqu'il supporte nativement ce langage.
Il est tout de même possible de rencontrer rarement MSSQL dans des environnements Linux/Unix.

[SQL Server Management Studio (SSMS)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15) est une fonctionnalité qui peut être installée avec le paquet d'installation MSSQL ou installée séparément. Cette application est souvent installé sur les serveurs MSSQL pour la configuration initiale et l'administration sur le long terme des bases de données.

SSMS est une application client qui permet la gestion des bases de données, elle n'existe donc pas uniquement sur les serveurs, cela signifie qu'il est possible de rencontrer des systèmes avec SSMS d'installé et stockant des identifiants et mots de passe enregistrés.

D'autres clients sont utilisables pour accéder à une base de données présente sur MSSQL:

- [mssql-cli](https://docs.microsoft.com/en-us/sql/tools/mssql-cli?view=sql-server-ver15)
- [SQL Server PowerShell](https://docs.microsoft.com/en-us/sql/powershell/sql-server-powershell?view=sql-server-ver15)
- [HeidiSQL](https://www.heidisql.com/)
- [SQLPro](https://www.macsqlclient.com/)
- [Script Impacket mssqlclient.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/mssqlclient.py)

Le client le plus souvent utilisé pas les pentesters est le script Impacket `mssqlclient.py`. Effectivement, la suite Impacket est présente sur de nombreuses distributions nativement.

Pour trouver l'emplacement du client sur l'hôte Linux:
`locate mssqlclient`

Comme MySQL, MSSQL a des [bases de données par défaut](https://docs.microsoft.com/en-us/sql/relational-databases/databases/system-databases?view=sql-server-ver15):

| Base de données | Description                                                                                                                                                                   |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| master          | Comporte toutes les informations systèmes pour une instance d'un serveur SQL.                                                                                                 |
| model           | Modèle utilisé comme structure pour la création des nouvelles bases de données. Tout changement effectué sur cette base est répliqué pour toute création d'une nouvelle base. |
| msdb            | L'agent SQL serveur utilise cette base pour planifier les tâches et alertes.                                                                                                  |
| tempdb          | Stocke les objets temporaires.                                                                                                                                                |
| resource        | Base de données en lecture seule contenant les objets systèmes inclus avec SQL Server.                                                                                        |

Lors de la configuration initiale, lorsqu'un administrateur initie et configure MSSQL pour être accessible en réseau, le service SQL tournera avec l'utilisateur `NT SERVICE\MSSQLSERVER`. Se connecter à MSSQL via un client est possible via l'authentification Windows, par défaut le chiffrement n'est pas obligatoire lors d'une tentative de connexion.

Si l'authentification utilise l'authentification Windows, alors c'est le système d'exploitation qui traitera la demande et utilisera soit la base locale SAM ou le contrôleur de domaine avant d'autoriser la connexion au système de gestion de base de données (DBMNS).

L'utilisation d'un Active Directory est idéal pour l'audit des activités et le contrôle d'accès dans les environnements Windows, mais cela pose aussi un problème si un compte est compromis, alors il pourrait être utilisé pour se déplacer latéralement ou causer une élévation de privilèges.

Certains paramètres sont dangereux, en voici certains:

- Les connexions non chiffrées.
- L'utilisation de certificats autosignés (peut être utilisé pour du spoofing).
- L'utilisation des canaux nommés.
- Identifiants et mot de passe par défaut. (pour le compte "sa", qui parfois n'est pas désactivé).

Par défaut, MSSQL utilise le port 1433.
Nmap peut aider à la reconnaissance du service (nom d'hôte, versions, canaux nommés actifs...).

Voici un exemple, en utilisant des scripts pour MSSQL et avec l'utilisateur "sa":
`nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 <adresse IP>`

Metasploit dispose aussi de modules MSSQL, pour le scan il est possible d'utiliser le module `scanner/mssql/mssql_ping`.

Pour interagir avec les bases de données sur le systèmes MSSQL, il faut utiliser le langage T-SQL (Transact-SQL)

L'authentification avec MSSQL nous permet d'interagir directement avec les bases de données via le moteur de base de données SQL.

Se connecter en utilisant `Mssqlclient.py` et l'authentification Windows:
`python3 mssqlclient.py <utilisateur>@<adresse IP> -windows-auth`

Une fois connecté il est conseillé de lister les bases de données présentes sur le système:
`select name from sys.databases`

## Oracle TNS

Oracle Transparent Network Substrate (TNS) est un protocole de communication qui facilite la communication entre les bases de données Oracle et les applications réseau.

TNS à été introduit comme partie de la suite logicielle [Oracle Net Services](https://docs.oracle.com/en/database/oracle/oracle-database/18/netag/introducing-oracle-net-services.html). TNS supporte de nombreux protocoles réseau entre les bases Oracle et les applications clients, comme IPX/SPX et TCP/IP. C'est une solution largement utilisée pour la gestion de larges bases de données complexes dans les domaines de la santé, de la finance et de la distribution. De plus, ce protocole comporte un mécanisme de chiffrement natif.

Plus tard, TNS à été mis à jour pour supporter de nouvelles technologies comme IPv6 et le chiffrement SSL/TLS. SSL/TLS offre un niveau additionnel de protection via la couche TCP/IP.

TNS fournit des outils et fonctionnalités avancées pour les administrateurs et les développeurs, il offre une surveillance, des performances compréhensive, des outils d'analyse, des outils de rapports d'erreurs, des capacités de journalisation, la gestion de la charge de travail et de la tolérance aux pannes.

Par défaut, TNS écoute sur le port TCP 1521. Il est configuré pour le support de nombreux protocoles réseau (incluant TCP/IP, UDP, IPX/SPX, et AppleTalk) et peut écouter sur une ou plusieurs cartes réseau, et sur des adresses spécifiques ou non.

**Par défaut**, Oracle TNS peut être administré à distance dans Oracle 8i/9i mais pas dans Oracle 10g/11g.

Par défaut, le listener TNS comporte des mesures de sécurités comme accepter les connexions depuis des hôtes spécifiques uniquement ou encore une authentification basique.
De plus, le listener utilisera les services réseau Oracle (Oracle Net Services) pour chiffrer la communication entre le client et le serveur. Les fichiers de configuration pour Oracle TNS sont nommés `tnsnames.ora` et `listener.ora` et sont normalement situés dans le répertoire `$ORACLE_HOME/network/admin`. Ces fichiers sont en texte clair et contiennent les informations de configuration pour les instances de bases de données Oracle et les autres services réseau utilisant le protocole TNS.

Oracle TNS est souvent utilisé avec d'autres services Oracle comme Oracle DBSNMP, Oracle Databases, Oracle Application Server, Oracle Enterprise Manager, Oracle Fusion Middleware, des serveurs web...

Des différences entres les versions des services Oracle sont à prendre en compte, par exemple Oracle 9 à un mot de passe par défaut ("CHANGE_ON_INSTALL") alors que Oracle 10 n'a pas de mot de passe par défaut.

Le service Oracle DBSNMP utilise aussi un mot de passe par défaut ("dbsnmp").

De plus, si le service "finger" est utilisé avec Oracle, alors cela rend le service Oracle vulnérable. (divulgation des répertoires home...)

Chaque base de données ou service utilisant Oracle TNS a une entrée dans [tnsnames.ora](https://docs.oracle.com/cd/E11882_01/network.112/e10835/tnsnames.htm#NETRF007), ce fichier contient les informations nécessaires aux clients pour se connecter au service. Les entrées sont composés d'un nom pour le service, l'emplacement réseau du service et le nom de la base de données ou du service que les clients doivent utiliser pour se connecter au service.

Voici un exemple simple du fichier `tnsnames.ora`:

```
  ORCL=
 (DESCRIPTION=
   (ADDRESS=(PROTOCOL = TCP)(HOST = 192.168.1.1)(PORT = 1521))
   (CONNECT_DATA=
     (SERVICE_NAME=orcl)))
```

Ce fichier peut aussi comporter des informations additionnelles comme la configuration de l'authentification, les paramètres du pool de connexion et la configuration du load balancing.

Le fichier `listener.ora`, est un fichier de configuration côté serveur qui défini les propriétés et paramètres du processus listener. Le processus listener est responsable de la réception des requètes client entrantes et de leurs redirection vers la bonne instance de base de données Oracle.

En résumé, les services réseau Oracle (Oracle Net Services) utilisent `tnsnames.ora` pour résoudre les noms des services en adresses réseau tandis que le processus listener utilise `listener.ora` pour déterminer les services qu'il doit écouter et le comportement du listener.

Les bases de données Oracle peuvent être protégés en utilisant la liste d'exclusion PL/SQL (PlsqlExclusionList). Cette liste est un fichier créée par l'utilisateur qui doit être placé dans le répertoire `$ORACLE_HOME/sqldeveloper`. Ce fichier contient les nom des paquets PL/SQL ou les types qui doivent être exclus de l'exécution. Une fois le fichier créer, il peut être chargé dans l'instance de la base de données. Il sert de liste noire qui ne peut pas être accessible depuis le serveur applicatif Oracle.

Avant d'énumérer le listener TNS et interagir avec, il faut avoir certains outils. Voici un script pour installer tout cela automatiquement:

```
#!/bin/bash

sudo apt-get install libaio1 python3-dev alien -y
git clone https://github.com/quentinhardy/odat.git
cd odat/
git submodule init
git submodule update
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
export LD_LIBRARY_PATH=instantclient_21_12:$LD_LIBRARY_PATH
export PATH=$LD_LIBRARY_PATH:$PATH
pip3 install cx_Oracle
sudo apt-get install python3-scapy -y
sudo pip3 install colorlog termcolor passlib python-libnmap
sudo apt-get install build-essential libgmp-dev -y
pip3 install pycryptodome
```

Oracle Database Attacking Tool (ODAT) est un outil open-source de pentest écrit en Python et créé pour énumérer et exploiter les vulnérabilités présentes dans les bases de données Oracle. Les vulnérabilités prises en charges sont vastes, de l'injection SQL, au RCE en passant par l'élévation de privilèges.

Pour vérifier que ODAT est bien installé:
`./odat.py -h`

Scan nmap pour Oracle TNS:
`nmap -p1521 -sV <adresse IP>`

Dans le DBMNS Oracle, un SID (System Identifier) est un nom unique qui identifie une instance de base de données particulière.

Une instance est un panel de processus et de structures mémoire qui interagissent pour administrer les données de la base de données.

Quand un client se connecte à une base de données Oracle, il peut spécifier le SID de la base de données en plus de la chaîne de connexion. Si aucun SID n'est précisé, alors la valeur par défaut contenue dans le fichier `tnsnames.ora` sera utilisée.

Le SID peut être utilisé par les administrateurs pour contrôler et administrer les différentes instances d'une base de données. Par exemple, ils peuvent démarrer, arrêter ou redémarrer une instance, ajuster l'allocation mémoire ou les autres paramètres de configuration. Les performances peuvent être visualisés avec un outil comme Oracle Entreprise Manager.

Il est possible d'utiliser de nombreux outils pour trouver les SID. (nmap,hydra,odat...)

Avec nmap:
`nmap -p1521 -sV <adresse IP> --open --script oracle-sid-brute`

Avec `odat.py` (avec le flag "all" pour récupérer le noms de bases, versions, comptes, vulnérabilités, mauvaises configurations...)
`./odat.py all -s <adresse IP>`

Pour se connecter et interagir avec la base de données Oracle, il est possible d'utiliser sqlplus:
`sqlplus <utilisateur>/<mot de passe>@<adresse IP>[/<SID>]`

Si jamais l'erreur suivante apparait "`sqlplus: error while loading shared libraries: libsqlplus.so: cannot open shared object file: No such file or directory`",
la commande suivante peut résoudre le problème:
`sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig`

La liste des commandes sqlplus sont disponibles [ici](https://docs.oracle.com/cd/E11882_01/server.112/e41085/sqlqraa001.htm#SQLQR985).

Voici la requête pour lister les tables dans la base actuelle:
`select table_name from all_tables;`

Voici la requête pour afficher les permissions de l'utilisateur actuel:
`select * from user_role_privs;`

Il est possible de se connecter en tant que l'Administrateur de base de données système ("sysdba"). Cela est possible si l'utilisateur à les permissions nécessaires (normalement attribués par l'administrateur de la base de données ou utilisés par lui-même):
`sqlplus <utilisateur>/<mot de passe>@<adresse IP>[/<SID>] as sysdba`

Si l'accès à la table `sys.user$` est autorisé (en ayant les droits,administrateur de la base...) alors il est possible de récupérer les hashs des utilisateurs et de les cracker hors-ligne. La commande suivante permet de récupérer ces hashs:
`select name, password from sys.user$;`
Attention, Oracle nécessite d'entourer les valeurs comme ci-dessous avec des guillemets:
`SELECT * FROM sys.user$ WHERE name = 'DBSNMP'`

Une autre option est de transférer un web shell vers la cible, pour cela, le serveur doit exécuter un serveur web et il faut connaitre l'emplacement éxact de la racine du serveur web.
Les répertoires racines des serveurs web par défaut sont:

- /var/www/html (Linux)
- C:\inetpub\wwwroot (Windows)

Avant de transférer un web shell, il est conseillé d'essayer avec un fichier qui ne semble pas dangereux pour éviter les mesures de l'antivirus et voir si cela fonctionne et que le fichier est bien accessible.

`./odat.py utlfile -s <adresse IP> -d XE -U <utilisateur> -P <mot de passe> --sysdba --putFile C:\\inetpub\\wwwroot <nom du fichier> ./<emplacement local du fichier à envoyer>`

## IPMI

Intelligent Platform Management Interface (IPMI) est un ensemble de spécifications standardisés pour la gestion matérielle des hôtes, utilisés pour la gestion et la surveillance des systèmes.

C'est un sous-système autonome qui fonctionne indépendamment du BIOS, processeur, firmware et du système d'exploitation.

IPMI permet aux administrateurs d'administrer et de surveiller les systèmes, même si ils sont éteins ou qu'ils sont sans réponse. IPMI fonctionne via une connexion directe aux composants systèmes et ne requière aucun accès au système d'exploitation.

IPMI peut aussi être utilisé pour mettre à jour les systèmes à distance sans nécessiter d'accès physique.

IPMI peut être utilisé de trois manières différentes:

- Avant que le système d'exploitation soit lancé, pour modifier les paramètres du BIOS.
- Quand l'hôte est entièrement éteint.
- Pour l'accès à l'hôte après un échec système.

Quand IPMI n'est pas utilisé pour ces 3 tâches, il peut surveiller une grande variété de métriques comme la température, le voltage, le statut des ventilateurs et l'alimentation. Il peut aussi être utilisé pour la récupération des informations d'inventaire, voir les logs matériels, et créer des alertes grâce à SNMP.

Le système hôte peut être entièrement éteint mais le module IPMI nécessite une source d'énergie et une connexion LAN.

Ce protocole à été développé par Intel en 1998 et est supporté par plus de 200 constructeurs (cisco, Dell, HP, Supermicro, Intel...).

Les systèmes utilisant IPMI 2.0 peuvent être administrés via "Serial over LAN" (mécanisme qui permet de rediriger l'entrée et la sortie du port série sur un système IP).
Ce qui offre aux administrateurs la possibilité de voir la sortie de la console série en mode "in-band" (l'accès se fait via les canaux normaux, comme le réseau IP).

Pour fonctionner, IPMI nécessite:

- Un "Baseboard Management Controller" (BMC) : Un micro-contrôleur, composant essentiel.
- Un "Intelligent Chassis Management Bus" (ICMB) : Une interface permettant la communication d'un châssis à un autre.
- Un "Intelligent Platform Management Bus" (IPMB) : Une extension du BMC.
- La mémoire IPMI : Stocke des informations comme les logs d'évènements système, données dépôt...
- Les interfaces de communication : interfaces systèmes locales, en série et LAN, bus de management ICMB et PCI.

IPMI communique via le port UDP 623. Les systèmes utilisant IPMI sont appelés les Baseboard Management Controllers (BMCs) ou Contrôleurs de gestion de carte mère.
Les BMC sont souvent implémentés comme des systèmes ARM intégrés exécutant Linux, et directement connectés à la carte mère de l'hôte.

Les BMC peuvent être présentes directement sur la carte mère ou ajoutés comme carte PCI.

LEs BMC les plus souvent rencontrés sont HP iLO, Dell DRAC, et Supermicro IPMI.

Beaucoup de BMC mettent à disposition une console web, un système d'accès distant en ligne de commande et bien évidement le protocole IPMI.

Le script NSE [ipmi-version](https://nmap.org/nsedoc/scripts/ipmi-version.html) peut être utilisé pour récupérer des informations sur le service:
`nmap -sU --script ipmi-version -p 623 <adresse IP>`

Le module de scan metasploit [`auxiliary/scanner/ipmi/ipmi_version`](https://www.rapid7.com/db/modules/auxiliary/scanner/ipmi/ipmi_version/) peut aussi être utilisé.

Parfois, le mot de passe par défaut du BMC n'est pas changé, en voici quelque-uns:

| Produit         | Nom d'utilisateur | mot de passe                                               |
| --------------- | ----------------- | ---------------------------------------------------------- |
| Dell iDRAC      | root              | calvin                                                     |
| HP iLO          | Administrator     | 8 caractères aléatoires composés de majuscules et chiffres |
| Supermicro IPMI | ADMIN             | ADMIN                                                      |

Il est possible d'utiliser une vulnérabilité dans le protocole RAKP dans la version 2.0 de IPMI,
pendant la phase d'authentification, le serveur envoi le hash (SHA1 avec sel ou MD5) du mot de passe utilisateur au client. Cela peut être exploité pour obtenir le mot de passe de n'importe quel utilisateur valide sur le BMC.
Ces hashs peuvent être crackés hors-ligne avec une attaque par dictionnaire par exemple. (mode 7300 sur hashcat).
Une attaque par masque est aussi possible pour HP iLO.

Comme aucun réglage ne peut résoudre cette faille (composant critique de la spécification IPMI). Les mots de passe doivent être très robustes aux attaques par force brute et/ou implémenter une segmentation réseau pour restreindre l'accès aux BMC.

De plus, parfois les mots de passe sont réutilisés, c'est pour cela que l'exploration d'IPMI est important et ne doit pas être négligée.

Pour récupérer les hashes IPMI, il est possible d'utiliser le module metasploit [`auxiliary/scanner/ipmi/ipmi_dumphashes`](https://www.rapid7.com/db/modules/auxiliary/scanner/ipmi/ipmi_dumphashes/)

## Linux Remote Management Protocols

Secure Shell (SSH) permet à deux ordinateurs d'établir une connexion chiffrée sur un réseau possiblement non sécurisé. SSH utilise le port TCP 22.

Un des avantages de SSH est que c'est un protocole est utilisable sur tous les systèmes d'exploitation communs. Comme c'est une application Unix à l'origine, il est implémenté nativement sur toutes les distributions Linux/MacOS.

Le serveur [OpenBSD SSH (OpenSSH)](https://www.openssh.com/), est un fork open-source de la version originelle et commerciale "SSH Server" de SSH Communication Security.

SSH dispose de deux version, SSH-1 et SSH-2.
SSH-2, aussi connu sous le nom de SSH version 2, est plus avancé que SSH-1 au niveau du chiffrement, de la vitesse, de la stabilitée et de la sécuritée.
Par exemple, SSH-1 est vulnérable aux attaques MITM (Man In The Middle) tandis que SSH-2 ne l'est pas.

SSH peut être utilisé pour l'envoi de commandes au serveur, le transfert de fichiers ou la redirection de ports.
Mais avant cela il faut se connecter en utilisant le protocole SSH et s'authentifier. OpenSSH dispose de [six méthodes d'authentification](https://www.golinuxcloud.com/openssh-authentication-methods-sshd-config/):
- Authentification par mot de passe
- Authentification par clé publique
- Authentification par hôte
- Authentification clavier-interactive
- Authentification défi-réponse (Challenge–response authentication)
- Authentification par GSSAPI

Voici les différentes étapes de l'authentification par clé publique:
1. le serveur s'authentifier auprès du client (server-side authentication), en envoyant un certificat au client. Cela permet au client de s'assurer que le serveur est le bon.
2. le client s'authentifie auprès du serveur (client-side authentication)
			- L'utilisateur entre la phrase secrète (passphrase) de la clé privée (si celle-ci utilise une passphrase). 			Cela permet au client SSH d'avoir accès à la clé privée.
  		- Le serveur créée un problème cryptographique qui ne peut être résolu qu'avec la clée privée. Et l'envoi au client.
			- Le client déchiffre le problème cryptographique reçu avec sa clée privée et le résout. Puis envoi la solution au serveur. Et indique au serveur qu'il est prêt à établir une connexion légitime.
      
Le fichier [sshd_config](https://www.ssh.com/academy/ssh/sshd_config) (/etc/ssh/sshd_config) est le fichier de configuration pour le serveur OpenSSH.

Certains paramètres peuvent être dangereux:

| Paramètre                  | Description                                  |
|--------------------------|----------------------------------------------|
| PasswordAuthentication yes | Autorise l'authentification avec des mots de passe.       |
| PermitEmptyPasswords yes  | Autorise l'usage de mots de passe vides.          |
| PermitRootLogin yes       | Autorise l'utilisateur root à se connecter.           |
| Protocol 1               | Utilise la version 1 du protocole SSH.     |
| X11Forwarding yes         | Autorise le X11Forwarding pour les applications avec interface graphique. |
| AllowTcpForwarding yes    | Autorise la redirection de ports TCP.             |
| PermitTunnel             | Autorise le tunneling (tunnel de couche 2 ou 3).                           |
| DebianBanner yes          | Affiche une banière spécifique lors de la connexion. |

Des guides pour augmenter la sécurité des serveurs SSH (hardening) sont disponibles en ligne. En voici un [ici](https://www.ssh-audit.com/hardening_guides.html).

[ssh-audit](https://github.com/jtesta/ssh-audit) peut être utilisé pour énumérer le serveur SSH (banière, chiffrement, configuration client et serveur...).

Le flag `-v` peut être utilisé pour afficher plus d'informations lors de la connexion au serveur avec le client openSSH (méthodes d'authentification, version du protocole, version du serveur...)

Pour précisier la méthode d'authentification avec le client OpenSSH (ici "password"):
`ssh <utilisateur>@<adresse IP> -o PreferredAuthentications=password`

[Rsync](https://linux.die.net/man/1/rsync) est un outil rapide et efficace pour copier des fichiers localement ou à distance. Il peut copier des fichiers d'une machine vers et depuis des hôtes distants.

C'est un outil très versatile et renommé pour son algorithme "delta-transfer".
Cet algorithme reduit la quantitée de données transférés quand une version du fichier existe déjà sur l'hôte de destination (en envoyant uniquement les différences entre le fichier source et de destination).

Il est largement utilisé pour les sauvegardes et la réplication. Il trouve les fichiers nécéssitant un transfert en se basant sur leurs taille (si elle à changée) ou la date de dernière modification.

par défaut, rsync utilise le port 873 et peut être configuré pour utiliser le protocole SSH pour le transfert de fichiers.

Ce [guide](https://book.hacktricks.xyz/network-services-pentesting/873-pentesting-rsync) peut être utilisé pour voir les moyens d'exploiter Rsync (lister le contenu des dossiers, récupérer des fichiers, parfois sans authentification)

Il est possible de sonder le service avec netcat:
`nc -nv <adresse IP> 873`
Il est possible de voir les accès disponibles avec la commande `list`.
Puis d'y avoir accès avec la commande rsync pour l'énumérer en détails:
`rsync -av --list-only rsync://<adresse IP>/<partage>`

Un guide pour l'utilisation de Rsync sur le protocole SSH est disponible [ici](https://phoenixnap.com/kb/how-to-rsync-over-ssh).