---
title: mssqlclient
description: mssqlclient est un programme python permettant de se connecter à un serveur SQL Windows. Il permet d'activer facilement l'option xp_cmdshell avec une simple commande, ce qui permet l'exécution de commandes depuis le client SQL.
published: true
date: 2025-05-04T14:54:10.539Z
tags: outil, indépendant
editor: markdown
dateCreated: 2024-07-13T09:21:17.856Z
---

# Introduction

mssqlclient est un script python permettant de se connecter à un serveur SQL Windows. Il permet d'activer facilement l'option xp_cmdshell avec une simple commande, ce qui permet l'exécution de commandes depuis le client SQL.

> mssqlclient est disponible au téléchargement ici: https://github.com/fortra/impacket/blob/master/examples/mssqlclient.py
> {.is-info}

# Syntaxe

`mssqlclient.py [[domaine/]utilisateur[:mot de passe]]@[Adresse] [options]`

# Options

| Option                  | Description                                                                                                  |
| ----------------------- | ------------------------------------------------------------------------------------------------------------ |
| `-p [port]`             | Spécifie le port MSSQL (1433 par défaut)                                                                     |
| `-db [base de données]` | Spécifie l'instance de la base de données MSSQL (aucune par défaut)                                          |
| `-windows-auth`         | Spécifie si l'authentification Windows doit être utilisée (non par défaut)                                   |
| `-file [fichier]`       | Spécifie un fichier contenant des commandes à éxecuter dans le shell SQL                                     |
| `--no-pass`             | Ne demande pas de mot de passe lors de la connexion                                                          |
| `-k`                    | Utilise l'authentification Kerberos en utilisant le fichier cache (variable d'environement KRB5CCNAME)       |
| `-dc-ip [adresse IP]`   | Spécifie l'addresse du controlleur de domaine, si non précisé, utilise celui entré dans la commande initiale |

# Procédures

Des procédures sont présentes une fois connecté au serveur, cela correspond à des fonctions spécifiques. Pour activer une procédure, il suffit de l'appeller par son nom dans le terminal.

| Procédure                | Description                                                                                              |
| ------------------------ | -------------------------------------------------------------------------------------------------------- |
| `lcd [chemin]`           | Change le repertoire local actuel vers un nouveau                                                        |
| `exit`                   | Arrète le processus du server et la session                                                              |
| `enable_xp_cmdshell`     | Active la fonctionnalité xp_cmdshell (permet l'exécution de commandes systèmes depuis le serveur SQL)    |
| `disable_xp_cmdshell`    | Désactive la fonctionnalité xp_cmdshell (permet l'exécution de commandes systèmes depuis le serveur SQL) |
| `xp_cmdshell [commande]` | Execute une commande en utilisant la fonctionnalité xp_cmdshell                                          |
| `! {cmd}`                | Execute un terminal local cmd                                                                            |

# Exemples

Se connecte au serveur MSSQL 10.129.43.30 avec l'utilisateur sql_dev en utilisant l'authentification Windows (c'est à dire que l'utilisateur sql_dev est un utilisateur Windows) avec le mot de passe "sqlpasswd"

`mssqlclient.py sql_dev:sqlpasswd@10.129.43.30 -windows-auth`
