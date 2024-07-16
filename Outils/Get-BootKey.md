---
title: Get-BootKey
description: Permet de récupérer la clé de démarrage (ou clé système) depuis le système actuel ou la ruche de registre SYSTEM
published: true
date: 2024-07-16T17:04:26.800Z
tags: outil, windows, powershell
editor: markdown
dateCreated: 2024-07-15T12:31:37.362Z
---

# Introduction

Get-BootKey est une applet powershel du module DSInternals, cette commande ermet de récupérer la clé de démarrage (ou clé système) depuis le système actuel ou la ruche de registre SYSTEM.

> Le module DSInternals est disponible au téléchargement ici: https://github.com/MichaelGrafnetter/DSInternals/tree/master
> {.is-info}

# Syntaxe

`Get-ADDBAccount -DatabasePath [fichier ntds.dit] [options]`

# Options

| Option                                                                  | Description                                                                                       |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `-Online`                                                               | Récupère la clé depuis le système d'exploitation actuel                                           |
| `-SystemHiveFilePath [fichier ruche de registre SYSTEM au format .hiv]` | Récupère la clé depuis le fichier ruche de registre SYSTEM (sauvegardé depuis la clé HKLM\SYSTEM) |

# Exemples

Récupère la clé depuis le fichier ruche de registre SYSTEM C:\temp\SYSTEM.hiv

`Get-BootKey -SystemHiveFilePath C:\temp\SYSTEM.hiv`

Récupère la clé depuis le système d'exploitation actuel

`Get-BootKey -Online`
