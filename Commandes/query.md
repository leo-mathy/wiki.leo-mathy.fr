---
title: query
description: Affiche des informations sur les processus, sessions et serveurs hôtes de session Bureau à distance.
published: true
date: 2024-07-16T16:52:10.960Z
tags: cmd, windows, powershell
editor: markdown
dateCreated: 2024-07-11T12:15:29.849Z
---

# Introduction

Affiche des informations sur les processus, sessions et serveurs hôtes de session Bureau à distance. Cela permet principalement de voir les utilisateurs connectés.

# Syntaxe

query [ PROCESS / SESSION / TERMSERVER / USER ]

# Options

| Option              | Description                    |
| ------------------- | ------------------------------ |
| `/SERVER:[serveur]` | Défini le serveur à interroger |

# Exemples

Afficher les utilisateur connectés

`query user`
