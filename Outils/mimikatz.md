---
title: mimikatz
description: Permet d'extraire les mots de passe, hash, codes PIN ou tickets Kerberos depuis la mémoire. Peut aussi effectuer des attaques de type pass-the-hash, pass-the-ticket ou construire des Golden tickets.
published: true
date: 2024-07-14T13:29:55.675Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-14T13:18:23.544Z
---

# Introduction

***Ce document est toujours en cours d'édition, en fonction des outils utilisés.***

Permet d'extraire les mots de passe, hash, codes PIN ou tickets Kerberos depuis la mémoire. Peut aussi effectuer des attaques de type pass-the-hash, pass-the-ticket ou construire des Golden tickets.

https://github.com/gentilkiwi/mimikatz

# Syntaxe de lancement

`mimikatz.exe [instruction(s)]`

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
| `base64`    | Permet d'utiliser l'encodage base64 toute sortie vers un fichier |
| `version`    | Affiche la version |

# Modules

Les modules sont des boites à outils permettant des actions spécifiques.

| Module             | Description                               |
| ------------------ | ----------------------------------------- |
| `privilege`     | Permet de manipuler les privilèges du processus mimikatz                 |
| `sekurlsa` | Permet d'extraire les mots de passe, hash, codes PIN ou tickets Kerberos depuis la mémoire du processus LSASS          |

# Exemples

Se connecter en RDP à une machine en précisant l'utilisateur.

`xfreerdp /u:<utilisateur> /v:<serveur>`

# A voir

Wiki de Mimikatz:
https://github.com/gentilkiwi/mimikatz/wiki
