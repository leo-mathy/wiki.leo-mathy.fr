---
title: GCC
description: GCC (GNU Compiler Collection) est une suite de logiciels libres de compilation. On l'utilise dans le monde Linux dès que l'on veut transcrire du code source en langage machine, La suite gère les langages C, C++, Objective-C, Fortran, Ada, Go et D.
published: true
date: 2024-07-11T09:39:17.095Z
tags: outil, linux
editor: markdown
dateCreated: 2024-04-17T06:42:27.481Z
---

# Introduction

Netcat est un puissant outil permetttant l'écoute de ports ou encore l'ouverture de connexion réseau, cet outil est principalement utilisé pour se connecter à une une connexion inverse ou backdoor, mais il a d'autres nombreux usages.

# Syntaxe

`netcat [ip/port/les deux]`

# Options

| Option | Description                                                              |
| ------ | ------------------------------------------------------------------------ |
| `-l`   | Mode écoute (listen), attendre une connexion entrante                    |
| `-v`   | Mode verbose, affiche des informations supplémentaires                   |
| `-n`   | Désactive la résolution DNS (permet d'augmenter la vitesse de connexion) |
| `-p`   | Spécifie un port d'écoute et aussi là où la connexion est transmise      |

# Exemples

Écoute sur sur le port 8080

`netcat -lp 8080`
