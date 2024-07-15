---
title: secretsdump
description: Lis les informations concernant les comptes depuis la base ntds.dit
published: true
date: 2024-07-15T13:03:04.230Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-15T12:49:07.492Z
---

# Introduction

secretsdump est un script python de la suite Impacket, ce script permet de récupérer les informations concernant les comptes depuis la base ntds.dit

> La suite Impacket est disponible au téléchargement ici: https://github.com/fortra/impacket
> {.is-info}

# Syntaxe

`impacket-secretsdump [options] [[domaine/]utilisateur[:mot de passe]@[addresse] / LOCAL]`

# Options

| Option                            | Description                                                                                                |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `-bootkey [clé de démarrage]`     | Spécifie la clé de démarrage (ou clé système) pour déchiffrer les valeurs des attribus secrets             |
| `-system [fichier .hiv]`          | Spécifie le chemin vers le fichier ruche de registre SYSTEM (sauvegardé depuis la clé HKLM\SYSTEM)         |
| `-security [fichier .hiv]`        | Spécifie le chemin vers le fichier ruche de registre SECURITY (sauvegardé depuis la clé HKLM\SECURITY)     |
| `-sam [fichier .hiv]`             | Spécifie le chemin vers le fichier ruche de registre SAM (sauvegardé depuis la clé HKLM\SAM)               |
| `-ntds [fichier ntds.dit]`        | Spécifie le chemin vers le fichier de la base de donnée d'un domaine                                       |
| `-outputfile [fichier de sortie]` | Enregistre la sortie dans un fichier                                                                       |
| `-just-dc-user [Nom SAM]`         | Spécifie quel compte récupérer en fonction du nom SAM (Security Account Manager) depuis la base de données |
| `-ldapfilter [Nom distinct]`      | Spécifie quel compte récupérer en fonction du DN (nom distinct) depuis la base de données                  |
| `-just-dc`                        | Extrait uniquement les hashs NTML et clés kerberos                                                         |
| `-just-dc-ntlm`                   | Extrait uniquement les hashs NTML                                                                          |
| `-pwd-last-set`                   | Affiche l'attribut pwdLastSet pour chaque compte                                                           |
| `-user-status`                    | Affiche si l'utilisateur est désactivé ou non                                                              |
| `-history`                        | Affiche l'historique de mot de passe et la dernière valeur du secret LSA (oldVal)                          |
| `-hashes LMHASH:NTHASH`           | change le format des hashs NTML pour LMHASH:NTHASH (et non NTHASH:LMHASH)                                  |

# Exemples

En local, récupère tous les comptes depuis ntds.dit en utilisant la clé de démarrage contenue dans system.hiv. Utilise le format lmhash:nthash pour la sortie et exporte les résultats dans le fichier secretdump.log.

`secretsdump.py -ntds ntds.dit -system system.hiv -hashes lmhash:nthash -outputfile secretdump.log LOCAL`

En local, récupère tous les comptes depuis ntds.dit en utilisant la clé de démarrage acdba64a3929261b04e5270c3ef973cf.

`secretsdump.py -ntds ntds.dit -bootkey acdba64a3929261b04e5270c3ef973cf LOCAL`
