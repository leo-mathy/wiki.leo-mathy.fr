---
title: Invoke-Expression
description: Alias de IEX, exécute des commandes ou des expressions sur l'ordinateur local.
published: true
date: 2024-10-25T20:33:27.063Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-10-06T10:13:16.438Z
---

# Introduction

Alias de IEX, Invoke-Expression est une applet PowerShell qui permet d'exécuter des commandes ou des expressions sur l'ordinateur local.

# Syntaxe

`Invoke-Expression <[commande]|[-command <commande>]>`

# Paramètres

| Paramètre             | Description                    |
| --------------------- | ------------------------------ |
| `-command <commande>` | Défini la commande à exécuter. |

# Exemples

Récupère le script distant et l'exécute sur l'ordinateur local.
`Invoke-Expression (iwr 'http://10.10.10.10/ExternalScript.ps1')`

Exécute la commande "ps"
`"ps" | Invoke-Expression`

# Voir aussi

Documentation officielle:
https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.utility/invoke-expression
