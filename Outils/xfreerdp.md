---
title: xfreerdp
description: xfreerdp est un client RDP (Remote Desktop Protocol), ce qui permet de se connecter sur des machines windows depuis des machines linux
published: true
date: 2024-04-17T06:53:52.885Z
tags: outil, linux
editor: markdown
dateCreated: 2024-04-14T16:36:19.842Z
---

# Introduction

xfreerdp est un client RDP (Remote Desktop Protocol), ce qui permet de se connecter à des machines windows depuis des machines linux.

# Synopsis

`xfreerdp [fichier] [options] [/v:serveur[:port]]`

# Exemple

Se connecter en RDP à une machine en précisant l'utilisateur. Par défaut le port est le 3389 si il n'est pas précisé.

`xfreerdp /u:<utilisateur> /v:<serveur>`

# Options

| Raccourci          | Description                               |
| ------------------ | ----------------------------------------- |
| `/v:[serveur]`     | Spécifie le serveur RDP                   |
| `/u:[UTILISATEUR]` | Spécifie le nom de l'utilisateur          |
| `/p:[PASSWORD]`    | Spécifie le mot de passe de l'utilisateur |
| `-f`               | Mode plein écran                          |















