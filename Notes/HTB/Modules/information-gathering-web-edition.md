---
title: Information Gathering - Web Edition
description: 
published: true
date: 2025-02-11T18:13:14.728Z
tags: notes, htb, module
editor: markdown
dateCreated: 2025-02-08T15:33:50.601Z
---

# Information Gathering - Web Edition

Date de complétion: XX/XX/2025

[information_gathering_web_edition_module_cheat_sheet.pdf](/cheat_sheet/information_gathering_web_edition_module_cheat_sheet.pdf)

# Notes

## Introduction

La reconnaissance web est une partie de la phase de collecte d'information lors du processus de pentest.
Ce processus doit systématiquement et de manière méticuleuse, collecter des informations sur une application ou un site web.

C'est la phase préparatoire avant l'analyse poussée et l'exploitation.

Le but de la reconnaissance web est:

- D'identifier les actifs: Définir les composants de la cible accessibles publiquement (pages web, domaines, adresses, technologies...), ce qui permet d'avoir une vue globale de la présence en ligne de la cible.
- Découvrir les informations cachées: Localiser les informations sensibles qui peuvent être exposés par inadvertance (fichiers,configurations,documentation...). Ces fichiers peuvent révéler des informations précieuses et des points d'entrés potentiels aux attaques.
- Analyser la surface d'attaque: Analyser la surface d'attaque permet d'identifier les vulnérabilités et failles potentielles. Cela correspond à l'évaluation des technologies utilisées, des configurations et des possibles points d'entrés.
- Collecter les renseignements (Intelligence gathering): Collecter les informations qui peuvent être utilisées pour l'exploitation ou les attaques sociales. Cela correspond à l'identification du personnel clé, adresses mail... ou encore des modèles ou comportements pouvant être exploités.

Toutes ces informations sont utilisées par les attaquants pour façonner leurs attaques en ciblant des faiblesses spécifiques et en contournant les mesures de sécurité.
En revanche, les défenseurs utilisent ces informations pour proactivement identifier et corriger les vulnérabilités avant leurs exploitation.

Il y a deux types de méthodologies de reconnaissance, active et passive.

Dans une reconnaissance active, l'attaquant interagi directement avec le système cible pour récupérer des informations (scan de ports/vulnérabilités, cartographie réseau, banner grabing, OS fingerprinting, spidering), dans la plupart des cas, la reconnaissance active est associée à un risque de détection plus grand.

Dans une reconnaissance passive, l'attaquant n'interagi pas directement avec la cible pour récupérer des informations. Cela se base sur l'analyse des informations et ressources disponibles publiquement (Moteurs de recherche,WHOIS,DNS,Archives web, Réseaux sociaux, repos de code...).
La reconnaissance passive est donc plus discrète.

## WHOIS

WHOIS est un protocole créé pour accéder aux bases de données stockant les informations concernant les ressources Internet enregistrées. En plus d'être associé aux noms de domaines, WHOIS peut aussi fournir les détails sur les blocks d'IP et les systèmes autonomes.

WHOIS peut être représenté comme un annuaire pour Internet, qui permet de voir qui est responsable ou propriétaire pour de nombreux types de ressources en ligne.

WHOIS est apparu dans les années 70 pour surveiller et administrer les ressources sur le réseau Arpanet. Le successeur de WHOIS est RDAP.

`whois <domaine.tld>`

WHOIS est important dans la reconnaissance web, il permet de:

- Identifier le personnel clé: les enregistrements WHOIS révèlent souvent des informations sur le personnel clé (nom, adresses mail, numéros de téléphone...) qui est responsable de l'administration du domaine.
- Découvrir l'infrastructure réseau: des détails techniques comme les serveurs DNS et adresses IP donnent des indices sur le réseau de la cible.
- Analyse des données historiques: Les anciens enregistrements WHOIS peuvent être consultés sur des services comme [WhoisFreaks](https://whoisfreaks.com/). Les anciens enregistrements peuvent être utilisés pour voir les changement de propriétaires, informations de contact ou détails techniques, dans le temps (permet de voir l'évolution de la présence en ligne de la cible).

## Utilising WHOIS

WHOIS peut aussi être utilisé pour:

- vérifier les domaines et si ils sont malveillants.
- récupérer l'identité du fournisseur de service.
- Créer des profils d'acteurs de la menace (Threat actor) avec les tactiques, techniques et procédures (TTPs). Et pouvoir générer si besoin les indicateurs de compromission (IOCs).

WHOIS permet de récupérer les informations principales suivantes:

- les enregistrements du domaine
- les propriétaire du domaine
- les statuts du domaine
- les serveurs de noms

## DNS

Voici le fonctionnement basique de la résolution d'un nom:

- Le système va vérifier son cache DNS à la recherche de l'adresse correspondante.
- Si l'adresse correspondante n'est pas trouvée dans celui-ci, alors il va contacter un résolveur DNS, le résolveur DNS va ensuite aussi vérifier son cache à la recherche de l'adresse correspondante.
- Si l'adresse correspondante n'est pas trouvée dans celui-ci, alors il va contacter un serveur DNS racine.
- Le serveur DNS racine va indiquer où trouver le serveur responsable du TLD.
- Le serveur TLD indique ensuite le serveur DNS faisant autorité pour le domaine.
- Le DNS serveur faisant autorité retourne ensuite l'adresse correspondante au résolveur DNS.
- Le résolveur DNS retourne l'information au système.

Le fichier host permet de mapper les domaines et les adresses IP manuellement.
Il est situé dans` C:\Windows\System32\drivers\etc\hosts` sur Windows et dans` /etc/hosts` sur Linux.

Par exemple, la ligne suivante indique que le nom `localhost` correspond à l'adresse `127.0.0.1`:
`127.0.0.1       localhost`

Ce fichier peut être utilisé pour effectuer des tests (lors d'un développement par exemple) mais aussi pour bloquer certains domaines.
Par exemple pour rediriger le domaine google.com vers une adresse non existante:
`0.0.0.0       google.com`

Une zone est une partie distincte de l'espace de nom du domaine. Par exemple: example.com ou test.example.com.
Une zone correspond à un fichier situé sur le serveur DNS, dans une zone il est possible de trouver de nombreux enregistrements (A,NS,SOA,MX...).

Le DNS est important dans une reconnaissance web pour:

- Récupérer des informations (domaines,sous-domaines,serveurs mail...).
- Cartographier l'infrastructure de la cible.
- Surveiller les changements.

## Digging DNS

De nombreux outils et techniques sont disponibles pour tirer parti du DNS pour la reconnaissance web:

- `dig (Domain Information Groper)`: Outil de recherche DNS polyvalent prenant en charge différents types de requêtes (A, MX, NS, TXT, etc.) et une sortie détaillée.
- `nslookup`: Outil de recherche DNS plus simple, principalement pour les enregistrements A, AAAA et MX.
- `host`: Outil de recherche DNS rationalisé avec une sortie concise.
- `dnsenum`: Outil d'énumération DNS automatisé, attaques par dictionnaire, force brute, transferts de zone (si autorisé).
- `fierce`: Outil de reconnaissance DNS et d'énumération de sous-domaines avec recherche récursive et détection de caractères génériques.
- `dnsrecon`: Combine plusieurs techniques de reconnaissance DNS et prend en charge divers formats de sortie.
- `theHarvester`: Outil OSINT qui rassemble des informations provenant de diverses sources, y compris les enregistrements DNS (adresses e-mail).
- `Services de recherche en ligne`: Interface simple pour la résolution DNS.

Dig (Domain Information Groper) est un puissant outil pour les requêtes DNS. IL est très flexible et personnalisable.

| Commande                         | Description                                                                                          |
| -------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `dig <domaine>`                  | Recherche de l'enregistrement A du domaine (par défaut).                                             |
| `dig <domaine> ANY`              | Recherche tous les enregistrements DNS pour un domaine (peut être désactivé par mesure de sécurité). |
| `dig <domaine> <enregistrement>` | Recherche un enregistrement spécifique pour un domaine.                                              |
| `dig @<résolveur> <domaine>`     | Recherche de l'enregistrement en spécifiant le serveur de résolution de noms.                        |
| `dig +trace <domaine>`           | Recherche en affichant le chemin complet de la résolution DNS.                                       |
| `dig -x <adresse IP>`            | Recherche DNS inverse.                                                                               |
| `dig +short <domaine>`           | Affiche un résumé de la réponse.                                                                     |

Lors d'une réponse, la section "opt" peut être présente, elle est lié au mécanisme d'extension DNS (EDNS), qui ajoute des fonctionnalités comme DNSSEC ou des messages de taille plus grande.

## Subdomains

Le sous-domaines servent d'extension au domaine principal, les sous-domaines sont souvent utilisés pour représenter des fonctionnalités ou sections différentes du site, par exemple `blog.example.com`, `shop.example.com`...

Dans le cadre de la reconnaissance web, les sous-domaines sont importants puisqu'ils peuvent contenir:

- Des environnements de tests (qui manquent souvent de mesures de sécurité et peuvent contenir des vulnérabilités)
- Des portails de connexion (pages d'administration...)
- Applications spécifiques (vielles applications, applications contenant des failles...)
- Informations sensibles (documents internes, fichiers de configuration...)

Pour énumérer les sous-domaines, il est possible d'utiliser des techniques passives et actives.

- Lors de l'utilisation de techniques actives, il faut directement interagir avec le serveur DNS.

  - Une méthode pourrait être d'essayer d'effectuer un transfert de zone, si le serveur est mal configuré la liste complète des sous-domaine serait disponible. Cette méthode est rarement réussie due aux mesures de sécurité renforcées.
  - Une autre méthode est l'énumération par force-brute, ce qui signifie le test de potentiels sous-domaines sur le domaine cible. Des outils comme dnsenum, ffuf ou gobuster peuvent accomplir cela.

- Lors de l'utilisation de techniques passives, la découverte de sous-domaines est effectuée sans interagir directement avec le serveur DNS cible.

  - Une méthode est la récupération des logs de transparence des certificats (CT Logs), qui contiennent souvent une liste des domaines associés aux certificats (dans les champs CN/SAN des certificats par exemple).

  - Il est aussi possible de passer par les moteurs de recherche pour essayer de découvrir les sous-domaines (avec les Google Dorks par exemple).

Les techniques passives sont plus discrète, mais peuvent ne pas découvrir tous les sous-domaines.
Les techniques actives offrent plus de contrôle et de résultats compréhensibles mais sont plus bruyantes.
Il est nécessaire de combiner ces deux approches pour obtenir des résultats complets.

## Subdomain Bruteforcing

Dans un premier temps, il faut avoir la wordlist adéquate:

- Générale: une wordlist avec des noms communs de sous-domaines.
- Spécifique: une wordlist spécifique à une industrie,secteur ou avec des modèles.
- Personnalisée: une wordlist créée spécifiquement pour la cible.

Plusieurs outils peuvent être utilisés pour brute-force les sous-domaines:

| Outil                                                   | Description                                                                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [dnsenum](https://github.com/fwaeytens/dnsenum)         | Outil complet d'énumération DNS prenant en charge les attaques par dictionnaire et force brute pour découvrir des sous-domaines.                        |
| [fierce](https://github.com/mschwager/fierce)           | Outil convivial pour la découverte récursive de sous-domaines, avec détection de caractères génériques et une interface facile à utiliser.              |
| [dnsrecon](https://github.com/darkoperator/dnsrecon)    | Outil polyvalent combinant plusieurs techniques de reconnaissance DNS et offrant des formats de sortie personnalisables.                                |
| [amass](https://github.com/owasp-amass/amass)           | Outil activement maintenu axé sur la découverte de sous-domaines, connu pour son intégration avec d'autres outils et ses nombreuses sources de données. |
| [assetfinder](https://github.com/tomnomnom/assetfinder) | Outil simple mais efficace pour trouver des sous-domaines en utilisant diverses techniques, idéal pour des analyses rapides et légères.                 |
| [puredns](https://github.com/d3mondev/puredns)          | Outil puissant et flexible de force brute DNS, capable de résoudre et de filtrer efficacement les résultats.                                            |

Effectue un brute-force de sous-domaine récursivement avec Dnsenum:
`dnsenum --enum <domaine> -f <wordlist> -r`

## DNS Zone Transfers

Le mécanisme de transfert de zones DNS permet de répliquer les enregistrements entre les serveurs DNS. Il est possible d'exploiter ce mécanisme si il est mal configuré pour récupérer de nombreuses informations.

Un transfert de zone correspond à une copie entière de tous les enregistrements DNS d'une zone d'un serveur à un autre.
Ce processus est essentiel pour maintenir la consistance et la redondance entre les serveurs DNS.

Voici le fonctionnement d'un transfert de zone:

1. **Requête de transfert de zone (AXFR)**:
   Le serveur secondaire initie le processus en envoyant une requête de transfert de zone au serveur primaire. Cette requête utilise normalement le type AXFR (Full ZOne Transfer).
2. **Transfert de l'enregistrement SOA**:
   Après avoir reçu la requête (et peut être authentifié le serveur secondaire), le serveur primaire réponds en envoyant son enregistrement SOA (Start of Authority). L'enregistrement SOA contient l'information vitale à propos de la zone comme le numéro de série (qui permet au serveur secondaire de déterminer si les données sont à jour).
3. **Transmission des enregistrements**:
   Le serveur primaire envoi tous les enregistrements un par un au serveur secondaire.
4. **Transmission des enregistrements terminé**:
   Le serveur primaire signale la fin du transfert de zone. Ce qui indique au serveur secondaire qu'il a bien reçu une copie complète des données de la zone.
5. **Validation (ACK)**:
   Le serveur secondaire informe le serveur primaire de la bonne réception et du traitement des données de zone. Cela complète le processus de transfert de zone.

En revanche, si le transfert de zone n'est pas correctement configuré, il est possible de récupérer le fichier de zone au complet, révélant ainsi la liste complète des sous-domaines ainsi que les adresses IP et d'autres informations sensibles.
C'est pour cela que les Administrateurs doivent autoriser le transfert de zone uniquement pour des serveurs secondaires de confiance.

Pour effectuer une requête de transfert de zone avec dig:
`dig axfr @<serveur faisant autorité pour le domaine> <domaine>`

## Virtual Hosts

Une fois la résolution de nom effectuée, le Traffic est redirigé avec le serveur web. La configuration du serveur web est cruciale pour déterminer comment les requêtes entrantes sont traitées.

Les serveurs comme Apache,Nginx ou IIS sont conçus pour hébergé de nombreux sites web ou applications sur un même serveur. Il y arrivent grâce aux hébergements virtuels (virtual hosting), ce qui leurs permet de faire la différence entre les domaines, sous-domaines ou même des sites web distints.

Cela permet aux serveurs Web de faire la distinction entre plusieurs sites Web ou applications partageant la même adresse IP.

Il arrivent à cela en utilisant le header HTTP "Host", une information incluse dans chaque requête HTTP envoyée par un navigateur web.

Si une entrée DNS n'est pas créée pour le vhost, il est toujours possible de modifier la requête avant son envoi ou de modifier le fichier host.

Pour rappel:

- **Sous domaines** : Extensions d’un domaine principal utilisées pour organiser un site et pouvant pointer vers des adresses IP différentes.
- **Virtual Hosts (VHosts)** : Configurations d’un serveur web permettant d’héberger plusieurs sites ou sous-domaines sur un même serveur avec des paramètres distincts.

Le fuzzing VHost est une technique permettant de découvrir des sous-domaines et des VHosts publics et non publics en testant divers header "host" par rapport à une adresse IP connue.

Voici comment le serveur web détermine quel contenu servir en fonction du header Host:

1. Le navigateur envoie une requête HTTP au serveur web.
2. Le domaine est précisé dans l’en-tête Host.
3. Le serveur identifie le site correspondant via sa configuration.
4. Il envoie les fichiers appropriés au navigateur.

Il existe trois types d’**hébergement virtuel** :

1. **Hébergement virtuel par nom** : Utilise l'en-tête HTTP Host pour distinguer les sites. Il est flexible, économique, mais a des limites avec SSL/TLS.
2. **Hébergement virtuel par IP** : Chaque site a une IP dédiée, offrant une meilleure isolation mais nécessitant plusieurs IPs, ce qui peut être coûteux.
3. **Hébergement virtuel par port** : Différents sites utilisent différents ports sur la même IP, mais cela oblige souvent les utilisateurs à spécifier le port dans l'URL.

Pour découvrir les hébergements virtuels, de nombreux outils existent:

| Outil       | Description                                                                                                                            |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| gobuster    | Outil polyvalent souvent utilisé pour le brute-force de fichiers/répertoires, mais aussi efficace pour la découverte d’hôtes virtuels. |
| Feroxbuster | Similaire à Gobuster, mais implémenté en Rust, connu pour sa rapidité et sa flexibilité.                                               |
| ffuf        | Fuzzer web rapide pouvant être utilisé pour découvrir des hôtes virtuels en testant l’en-tête Host.                                    |

Avec gobuster, brute force les Vhosts:
`gobuster vhost -u http[s]://<adresse IP> -w <wordlist> --append-domain`
(`--append-domain` permet d'ajouter le nom du domaine à la fin de chaque mot de la wordlist)

## Certificate Transparency Logs

SSL/TLS est un protocole qui chiffre la communication entre un navigateur et un site web.
Au cœur de SSL/TLS, il y a le certificat digital, un fichier qui vérifie l'identité du site web et permet la communication chiffrée.

Cependant le processus d'administration des certificats n'est pas sans failles, un attaquant pourrait exploiter un certificat rogue ou mal émis pour se faire passer pour un site web légitime.

C'est pour cela que les journaux de transparence des certificats (CT Logs) existent.
Ces journaux sont publics et en ajout unique (impossible de supprimer des entrées).
Ces journaux contiennent la liste des certificats SSL/TLS émis.

Quand une autorité de certification émet un nouveau certificat, elle doit l'envoyer vers de multiples journaux de transparence de certificats. Diverses organisations maintiennent ces journaux ouverts à tous.

Ces journaux sont utiles pour:

- **Détecter des certificats rogue**: En surveillant ces logs, les propriétaires de sites web peuvent rapidement identifier les certificats suspects ou mal émis. Cela permet de révoquer ces certificats avant leurs utilisation malveillante.
- **Rendre responsable les autorités de certification**: Les journaux de transparence des certificats rendent responsable les autorités de certification en cas de non respect des standards ou des règles.
- **Renforcement de l'infrastructure à clé Publique du web**: Les journaux de Transparence des Certificats améliorent la sécurité et l'intégrité de l'infrastructure à clé Publique du web en offrant un mécanisme de surveillance et de vérification publique des certificats.

Les logs de Certificate Transparency (CT) assurent la transparence et l'intégrité des certificats SSL/TLS grâce à des techniques cryptographiques et à une surveillance publique :

1. **Émission du certificat** : Une Autorité de Certification (CA) vérifie le propriétaire du site et émet un pré-certificat.
2. **Enregistrement dans les logs** : Le pré-certificat est soumis à plusieurs logs CT, immuables et décentralisés.
3. **Signature cryptographique (SCT)** : Chaque log génère une preuve (SCT) confirmant l’enregistrement du certificat.
4. **Vérification par le navigateur** : Lorsqu'un utilisateur visite un site, le navigateur vérifie les SCT pour s’assurer de la validité du certificat.
5. **Surveillance et audit** : Des acteurs surveillent les logs pour détecter d’éventuels certificats frauduleux.

Les logs CT utilisent une **structure de Merkle Tree** pour garantir leur intégrité. Chaque certificat est un nœud feuille, et des hachages intermédiaires permettent une vérification rapide sans nécessiter l’ensemble du log. Toute modification entraînerait un changement du hachage racine, révélant immédiatement toute tentative de falsification.

Pour effectuer une recherche dans les CT logs, voici deux options populaires:

- [crt.sh](https://crt.sh/) (Gratuit, facile à utiliser, aucune inscription requise)
- [censys](https://search.censys.io/) (Données étendues et options de filtrage, accès API)

## Fingerprinting

Le fingerprinting (ou prise d'empreinte) correspond à l'extraction de détails techniques à propos des technologies utilisées par un site ou une application web.

Les signatures digitales des systèmes d'exploitation et composants logiciels peuvent révéler des informations critiques sur l'infrastructure de la cible et de potentielles faiblesses.
Cela permet aussi aux attaquants de façonner leurs attaques et d'exploiter des vulnérabilités spécifiques aux technologies identifiées.

Le fingerprinting est pilier de la reconnaissance web:

- **Attaques ciblées**: permet de cibler des technologies spécifiques avec des exploits ou vulnérabilités connues pour affecter ces systèmes.
- **Identifier les mauvaises configurations**: permet d'exposer les mauvaises configurations, logiciels dépassés, paramètres par défaut ou autres faiblesses.
- **Prioriser les cibles**: Permet de prioriser les efforts en identifiant les systèmes pouvant être les plus vulnérables ou comportant des informations de valeur.
- **Créer un profil compréhensif**: Combiner les données de fingerprint avec d'autres découvertes permet de créer une vue complète de l'infrastructure cible, d'aider dans la compréhension globale de la posture en termes de sécurité et les vecteurs d'attaques potentiels.

Il existe de nombreuses techniques utilisées pour fingeprint les serveurs web et technologies:

- **Banner Grabbing**: Analyser les bannières présentées par les serveurs web et autres services. Ces bannières révèlent souvent le logiciel, la version et d'autres détails.
- **Analyse en-têtes HTTP (HTTP Headers)**: Les en-têtes HTTP sont transmises avec chaque requête/réponse et peuvent contenir de nombreuses informations (logiciels,technologies...).
- **Rechercher des réponses spécifiques (Probing)**: Envoyer des requêtes spécialement forgées vers la cible peut retourner des résultats uniques qui révèlent des technologies spécifiques ou versions. Par exemple, certains messages d'erreurs ou comportements sont caractéristiques d'un serveur ou logiciel particulier.
- **Analyse du contenu de la page**: Le contenu, la structure, les scripts ou autres éléments d'une page peuvent donner des indices sur les technologies utilisées (un message de copyright par exemple).

Voici des outils permettant d'automatiser le processus de fingerprint en combinant plusieurs techniques pour identifier les serveurs Web, systèmes d'exploitation, CMS et autres technologies:

| Outil      | Description                                                                                                                                         |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| Wappalyzer | Extension de navigateur et service en ligne. Identifie de nombreuses technologies Web.                                                              |
| BuiltWith  | Outil de génération de rapports détaillés sur les technologies d’un site web.                                                                       |
| WhatWeb    | Outil en ligne de commande pour le fingerprinting des sites web. Utilise une grande base de signatures pour identifier diverses technologies.       |
| Nmap       | Outil permettant le fingerprinting des services et systèmes d’exploitation.                                                                         |
| Netcraft   | Fournit divers services de sécurité web, notamment le fingerprinting des sites web et la génération de rapports de sécurité.                        |
| wafw00f    | Outil en ligne de commande spécialement conçu pour identifier les pare-feu applicatifs web (WAF). Permet d'identifier son type et sa configuration. |

Récupérer uniquement les headers HTTP avec curl:
`curl -I <adresse>`

Nikto est un outil open-source de scan et d’évaluation des vulnérabilités des serveurs web.

Utiliser Nikto pour exécuter uniquement les modules d’identification logiciel:
`nikto -h <adresse> -Tuning b`

Nikto va effectuer une série de tests pour essayer d'identifier des logiciels obsolètes, fichiers non sécurisés, fichiers de configuration et risques potentiels de sécurité.

## Crawling

Le crawling (ou spidering) est le processus automatisé de systématiquement parcourir le web.
Un web crawler va suivre les liens d'une page à l'autre, collectant l'information.

Les crawlers sont essentiellement des robots qui utilisent des algorithmes pré-définis pour découvrir et indexer les pages web. Cela permet de les rendre accessibles au travers d'un moteur de recherche, d'analyser les données ou d'effectuer une reconnaissance web.

Le robot explore une page, analyse son contenu, extrait les liens, puis les visite à leur tour, répétant le processus pour explorer un site ou une grande partie du web.

Cela le différencie du fuzzing, qui consiste à deviner des liens possibles.

Il y a deux types de crawling:

- **Le Breadth-First Crawling (Exploration en largeur d'abord)**: Explore tous les liens de la page initiale, puis ceux des pages suivantes, et ainsi de suite. Utile pour obtenir une vue d'ensemble de la structure et du contenu d'un site.
- **Le depth-first crawling (Exploration en profondeur d'abord)**: Suit un chemin de liens jusqu'au bout avant de revenir en arrière pour explorer d'autres chemins, utile pour trouver du contenu précis ou explorer en profondeur la structure d'un site.

Les crawlers peuvent extraire divers types de données, chaque type servant un but spécifique dans le processus de reconnaissance:

- **Liens internes et externes** : Cartographient la structure d’un site et ses relations avec d’autres ressources.
- **Commentaires** : Peuvent contenir des fuites d’informations sensibles ou des indices sur des vulnérabilités.
- **Métadonnées** : Fournissent des informations sur le contenu, l’auteur et la pertinence des pages.
- **Fichiers sensibles** : Incluent des sauvegardes, fichiers de configuration ou journaux pouvant exposer des données confidentielles.

Une information seule peut sembler insignifiante, mais combinée à d’autres, elle peut révéler une vulnérabilité critique. Relier les données permet de mieux comprendre l’environnement cible.
Une approche globale est essentielle pour tirer des conclusions pertinentes et affiner l’analyse.

## robots.txt

Le fichier robots.txt agit comme un guide pour les robots, définissant les zones d'un site web autorisées ou hors limite.

Ce fichier est placé à la racine des sites web et adhère à la norme d'exclusion des robots (lignes directrices sur la manière dont les crawlers doivent se comporter lors de la visite d'un site).

Ce fichier contient des instructions sous forme de directives qui indiquent les parties d'un site que les crawlers peuvent ou ne peuvent pas naviguer.

Exemple de fichier robots.txt qui indique à tous les user-agents qu'ils ne sont pas autorisés à accéder aux URLs qui commences par `/private/`:

```
User-agent: *
Disallow: /private/
```

D'autres directives peuvent autoriser l'accès à des répertoires ou à des fichiers spécifiques, définir des délais de crawling pour éviter de surcharger un serveur ou fournir des liens vers des plans de site (sitemaps) pour une exploration efficace.

Le fichier robots.txt est composé d'enregistrements (plusieurs instructions), chaque enregistrement est principalement composé par:

- Une instruction **user-agent**: identifiant pour différents types de robots, par exemple Googlebot pour le robot de google et Bingbot pour celui de Microsoft.
- Des **Directives**: instructions spécifiques pour le user-agent défini.

Même si les crawlers ne sont pas obligés de suivre les instructions de ce fichier, la plupart des crawlers légitimes respectent ces directives. Cela est important pour:

- **Prévenir le trafic excessif**
- **Protéger les informations sensibles** de l'indexation des moteurs de recherches.
- **La conformité juridique et éthique**: parfois ignorer ce fichier peut être considéré comme une violation des termes de service ou même un problème juridique. Surtout pour des données privées ou protégé par le droit d'auteur.

Dans le cadre de la reconnaissance web, le fichier robots.txt peut être une source importante d'information pour:

- **Découvrir les répertoires cachés** : Les chemins interdits de robots.txt peuvent révéler des fichiers sensibles ou des panneaux d’administration.
- **Cartographier la structure du site** : L’analyse des chemins aide à repérer des sections cachées du site.
- **Détecter les pièges à crawlers** : Certains sites ajoutent des répertoires « honeypot » pour attirer les crawlers malveillants.

## Well-Known URIs

Le standard .well-known (défini dans la [RFC 8615](https://datatracker.ietf.org/doc/html/rfc8615)) sert de répertoire standardisé dans le domaine racine d'un site web. Ce répertoire normalement accessible via `/.well-known/`, contient les métadonnées critiques d'un site web, incluant les fichiers de configuration et les informations, relatives au services, protocoles et mécanismes de sécurité.

En établissant un emplacement contant de telles données, .well-known simplifie la découverte et l'accès aux parties prenantes, navigateurs, applications ou outils de sécurité.

Cela permet aux clients de automatiquement localiser et récupérer des fichiers de configuration spécifiques en construisant l'URL appropriée.
Par exemple pour consulter la politique de sécurité d'un site web, un client effectuera une requête vers `<site web>/.well-known/security.txt`.

L'IANA (Internet Assigned Numbers Authority) maintient un [registre](https://www.iana.org/assignments/well-known-uris/well-known-uris.xhtml) des toutes les URI .well-known, chacune servant un but spécifique.

Lors de la reconnaissance web, les URIs .well-known sont une source importante d'informations.

Par exemple l’URI `openid-configuration` de `.well-known` permet d’accéder à la configuration d’un fournisseur OpenID Connect. Cet endpoint (`<site web>/.well-known/openid-configuration`) renvoie un JSON contenant les endpoints, méthodes d’authentification et informations sur l’émission de tokens.

## Creepy Crawlies

Le web crawling est un vaste sujet, de nombreux outils existent.
Les outils les plus populaires sont:

- **Burp Suite Spider** : Un puissant crawler intégré à Burp Suite, utilisé pour cartographier les applications web et détecter des vulnérabilités.
- **OWASP ZAP** : Un scanner de sécurité open-source avec un mode manuel et automatique, incluant un spider pour explorer les applications web.
- **Scrapy** : Un framework Python flexible et évolutif pour créer des web crawlers, idéal pour extraire des données structurées et gérer des scénarios complexes.
- **Apache Nutch** : Un crawler open-source en Java, conçu pour des explorations web à grande échelle, nécessitant une configuration avancée.
