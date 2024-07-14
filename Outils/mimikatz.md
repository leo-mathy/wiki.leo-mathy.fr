---
title: mimikatz
description: Permet d'extraire les mots de passe, hash, codes PIN ou tickets Kerberos depuis la mémoire. Peut aussi effectuer des attaques de type pass-the-hash, pass-the-ticket ou construire des Golden tickets.
published: true
date: 2024-07-14T13:18:23.544Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-14T13:18:23.544Z
---

# Introduction

Permet d'extraire les mots de passe, hash, codes PIN ou tickets Kerberos depuis la mémoire. Peut aussi effectuer des attaques de type pass-the-hash, pass-the-ticket ou construire des Golden tickets.

https://github.com/gentilkiwi/mimikatz

# Syntaxe de lancement

`mimikatz.exe`

# Syntaxe d'instruction

`[nom du module]::[commande] [arguments]`

# Commandes du module standard

> Les commandes du module standard peuvent être exécutés sans préciser le module standard.
{.is-info}

| Commande             | Description                               |
| ------------------ | ----------------------------------------- |
| `exit`     | Quitte mimikatz                  |
| `cls` | Efface l'affichage          |
| `log`    | Enregistre les entrées et sorties de mimikatz dans un fichier |

# Modules

Les modules sont des boites à outils permettant des actions spécifiques.

| Module             | Description                               |
| ------------------ | ----------------------------------------- |
| `privilege`     | Quitte mimikatz                  |
| `sekurlsa` | Efface l'affichage          |
| `kerberos`    | Enregistre les entrées et sorties de mimikatz dans un fichier |
| `crypto`    | Enregistre les entrées et sorties de mimikatz dans un fichier |
| `vault`    | Enregistre les entrées et sorties de mimikatz dans un fichier |
| `lsadump`    | Enregistre les entrées et sorties de mimikatz dans un fichier |

# Exemples

Se connecter en RDP à une machine en précisant l'utilisateur.

`xfreerdp /u:<utilisateur> /v:<serveur>`

# A voir

Wiki de Mimikatz:
https://github.com/gentilkiwi/mimikatz/wiki
