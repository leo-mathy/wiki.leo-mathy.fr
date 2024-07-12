---
title: Netcat
description: Netcat est un utilitaire permettant d'ouvrir des connexions réseau, cet outil peut être utilisé pour de nombreux usages
published: true
date: 2024-07-12T16:41:41.335Z
tags: outil, linux
editor: markdown
dateCreated: 2024-04-15T06:48:30.391Z
---

# Introduction

Netcat est un puissant outil permetttant l'écoute de ports ou encore l'ouverture de connexion réseau, cet outil est principalement utilisé pour se connecter à une une connexion inverse ou backdoor, mais il a d'autres nombreux usages.

# Syntaxe

`netcat [ip/port/les deux]`

# Options

| Option          | Description                                                              |
| --------------- | ------------------------------------------------------------------------ |
| `-l`            | Mode écoute (listen), attendre une connexion entrante                    |
| `-v`            | Mode verbose, affiche des informations supplémentaires                   |
| `-n`            | Désactive la résolution DNS (permet d'augmenter la vitesse de connexion) |
| `-p [port]`     | Spécifie un port d'écoute et aussi là où la connexion est transmise      |
| `-e [commande]` | Éxecute la commande spécifiée lorsqu'une connexion est établie           |

# Exemples

Écoute sur sur le port 8080

`netcat -lp 8080`
