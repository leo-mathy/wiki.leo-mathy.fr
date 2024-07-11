---
title: Get-WmiObject
description: Obtient des instances de classes WMI (Windows Management Instrumentation), ce qui permet de surveiller les ressources systèmes.
published: true
date: 2024-07-11T11:53:49.448Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-07-11T11:53:49.448Z
---

# Introduction

Obtient des instances de classes WMI (Windows Management Instrumentation), ce qui permet de surveiller les ressources systèmes. Cet commande peut être utile pour récupérer des informations diverses et/ou précises.

# Syntaxe

`Get-WmiObject -Class [classe WMI]`

# Options

| Option                       | Description                    |
| ---------------------------- | ------------------------------ |
| `-ComputerName [ordinateur]` | Spécifie un ordinateur distant |
| `-Namespace [espace de nom]` | Change l'espace de nom.        |
| `-list`                      | liste les différentes classes  |

# Exemples

Affiche les informations sur les produits installés

`Get-WmiObject -Class Win32_Product`
