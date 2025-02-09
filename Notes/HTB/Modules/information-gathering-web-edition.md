---
title: Information Gathering - Web Edition
description: 
published: true
date: 2025-02-09T14:22:47.825Z
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
| Outil      | Description |
|------------|------------|
| [dnsenum](https://github.com/fwaeytens/dnsenum)    | Outil complet d'énumération DNS prenant en charge les attaques par dictionnaire et force brute pour découvrir des sous-domaines. |
| [fierce](https://github.com/mschwager/fierce)     | Outil convivial pour la découverte récursive de sous-domaines, avec détection de caractères génériques et une interface facile à utiliser. |
| [dnsrecon](https://github.com/darkoperator/dnsrecon)   | Outil polyvalent combinant plusieurs techniques de reconnaissance DNS et offrant des formats de sortie personnalisables. |
| [amass](https://github.com/owasp-amass/amass)      | Outil activement maintenu axé sur la découverte de sous-domaines, connu pour son intégration avec d'autres outils et ses nombreuses sources de données. |
| [assetfinder](https://github.com/tomnomnom/assetfinder)| Outil simple mais efficace pour trouver des sous-domaines en utilisant diverses techniques, idéal pour des analyses rapides et légères. |
| [puredns](https://github.com/d3mondev/puredns)    | Outil puissant et flexible de force brute DNS, capable de résoudre et de filtrer efficacement les résultats. |

Effectue un brute-force de sous-domaine récursivement avec Dnsenum:
`dnsenum --enum <domaine> -f <wordlist> -r`

## DNS Zone Transfers

Le mécanisme de transfert de zones DNS permet de répliquer les enregistrements entre les serveurs DNS. Il est possible d'exploiter ce mécanisme si il est mal configuré pour récupérer de nombreuses informations.

Un transfert de zone correspond à une copie entière de tous les enregistrements DNS d'une zone d'un serveur à un autre.
Ce processus est esentiel pour maintenir la conssistance et la redondance entre les serveurs DNS. 
En revanche, si le transfert de zone n'est pas correctement configuré, il est possible de récupérer le fichier de zone au complet, révélant ainsi la liste complète des sous-domaines ainsi que les adresses IP et d'autres informations sensibles.

Voici le fonctionnement d'un transfert de zone:
1. **Requète de transfert de zone (AXFR)**:
	Le serveur secondaire initie le processus en envoyant une requète de transfert de zone au serveur primarie. Cette requète utilise normalement le type AXFR (Full ZOne Transfer).
2. **Transfert de l'enregistrement SOA**:
	Après avoir reçu la requète (et peut être authentifié le serveur secondaire), le serveur primaire réponds en envoyant son enregistrement SOA (Start of Authority). L'enregistrement SOA contient l'information vitale à propos de la zone comme le numéro de série (qui permet au serveur secondaire de déterminer si les données sont à jour).
3. ** ransmission des enregistrements**: Le serveur primaire envoi tous les enregistrements un par un au serveur secondaire.
4. 