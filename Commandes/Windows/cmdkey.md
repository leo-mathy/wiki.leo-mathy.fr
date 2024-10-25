---
title: cmdkey
description: Créer, lister et supprimer des mots de passe et noms d'utilisateurs enregistrés.
published: true
date: 2024-10-25T20:21:02.771Z
tags: windows, commande
editor: markdown
dateCreated: 2024-09-08T08:14:52.836Z
---

# Introduction

La commande cmdkey permet de créer, lister et supprimer des mots de passe et noms d'utilisateurs enregistrés.
Ces informations peuvent être retrouvées dans le gestionnaire d'identification ou avec la fonction KRShowKeyMgr.

# Syntaxe

`cmdkey </add <paramètres>|/delete <paramètres> | /list <paramètres>> [paramètres]`

# Paramètres

| Paramètre                          | Description                                                                                                                                                                                    |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/list[:nom de la cible]`          | Affiche la liste des mots de passe et noms d'utilisateurs enregistrés. Il est possible de préciser le nom de la cible pour afficher uniquement l'entrée souhaitée.                             |
| `/delete:<nom de la cible> [/ras]` | Supprime une entrée dans la liste des mots de passe et noms d'utilisateurs enregistrés. Il est possible d'utiliser l'option /ras pour supprimer ces informations sur le serveur Remote Access. |
| `/smartcard`                       | Affiche la liste des mots de passe et noms d'utilisateurs enregistrés sur une carte à puce.                                                                                                    |
| `/add:<nom de la cible>`           | Ajoute un nom d'utilisateur et un mot de passe à la liste.                                                                                                                                     |
| `/generic:<nom de la cible>`       | Ajoute une information d'identification générique à la liste.                                                                                                                                  |
| `/user:<nom d'utilisateur>`        | Spécifie le nom d'utilisateur.                                                                                                                                                                 |
| `/pass:<mot de passe>`             | Spécifie le mot de passe.                                                                                                                                                                      |
| `/?`                               | Affiche l'aide.                                                                                                                                                                                |

# Exemples

Liste les informations d'identification:
`cmdkey /list`

Supprime l'entrée "MicrosoftAccount:target=SSO_POP_Device" de la liste
`cmdkey /delete:MicrosoftAccount:target=SSO_POP_Device`

Ajoute une entrée avec comme nom "DBPass01" comme mot de passe "mydbpass", et comme nom d'utilisateur "DBuser"
`cmdkey /add:DBPass01 /user:DBuser /pass:mydbpass`

# Voir aussi

Documentation officielle de la commande
https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/cmdkey
