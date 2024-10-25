---
title: xfreerdp
description: xfreerdp est un client RDP (Remote Desktop Protocol), ce qui permet de se connecter sur des machines windows depuis des machines linux
published: true
date: 2024-07-16T17:15:41.806Z
tags: outil, linux
editor: markdown
dateCreated: 2024-04-14T16:36:19.842Z
---

# Introduction

xfreerdp est un client RDP (Remote Desktop Protocol), ce qui permet de se connecter à des machines windows depuis des machines linux.

# Syntaxe

`xfreerdp [fichier] [options] [/v:serveur[:port]]`

# Options

> Par défaut le port est le 3389 si il n'est pas précisé.
> {.is-info}

| Option                  | Description                                      |
| ----------------------- | ------------------------------------------------ |
| `/v:[serveur]`          | Spécifie le serveur RDP                          |
| `/u:[UTILISATEUR]`      | Spécifie le nom de l'utilisateur                 |
| `/p:[PASSWORD]`         | Spécifie le mot de passe de l'utilisateur        |
| `-f`                    | Mode plein écran                                 |
| `/drive:/[emplacement]` | Créer un lecteur mappé vers l'emplacement client |

# Exemples

Se connecter en RDP à une machine en précisant l'utilisateur.

`xfreerdp /u:<utilisateur> /v:<serveur>`
