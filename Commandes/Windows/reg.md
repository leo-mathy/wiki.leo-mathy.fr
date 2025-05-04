---
title: reg
description: Permet d'effectuer des opérations sur le registre Windows
published: true
date: 2025-05-04T14:52:57.875Z
tags: windows, commande, rédaction incomplète
editor: markdown
dateCreated: 2024-07-15T11:58:30.391Z
---

# Introduction

Reg permet d'effectuer des opérations sur le registre Windows

# Syntaxe

`reg [commande] [options]`

# Commandes

| Commande                       | Description                                                                                            |
| ------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `reg query [chemin de la clé]` | retourne la liste des sous-clés                                                                        |
| `reg save [chemin de la clé] [fichier au format .hiv]`  | Sauvegarde la clés et sous-clés dans un fichier au format .hiv (préserve les ACL et les propriétaires) |

# Exemples

Sauvegarde la base SAM dans le fichie sam.hib

`reg save HKLM\SAM sam.hiv`

# Voir aussi

Documentation officielle:
https://learn.microsoft.com/fr-fr/windows-server/administration/windows-commands/reg-query
