---
title: Get-HotFix
description: Permet d'afficher les patchs Windows
published: true
date: 2024-07-11T11:40:30.157Z
tags: windows, powershell
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
