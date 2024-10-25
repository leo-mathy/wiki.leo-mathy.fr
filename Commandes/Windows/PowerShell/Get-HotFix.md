---
title: Get-HotFix
description: Permet d'afficher les patchs Windows
published: true
date: 2024-10-25T20:31:32.624Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-07-11T11:40:30.157Z
---

# Introduction

La commande Get-HotFix permet d'afficher les patchs Windows installés.

# Syntaxe

Get-HotFix [options]

# Options

| Option                         | Description                    |
| ------------------------------ | ------------------------------ |
| `-ComputerName [ordinateur]`   | Spécifie un ordinateur distant |
| `-Description [type de patch]` | spécifier les types de patch   |

# Exemples

Affiche les patchs de sécurité

`Get-HotFix -Description Security*`

# Voir aussi

Consulter les patchs en détails avec leurs dates, taille ou encore classification.
https://www.catalog.update.microsoft.com/
