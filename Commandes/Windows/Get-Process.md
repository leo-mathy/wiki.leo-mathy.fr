---
title: Get-Process
description: Obtient les processus qui s’exécutent sur l’ordinateur local.
published: true
date: 2024-08-28T14:01:30.958Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-08-28T14:01:30.958Z
---

# Introduction

L'applet Get-Process permet d'obtenir les processus qui s’exécutent sur l’ordinateur local.

# Syntaxe

`Get-Process [paramètres]`

# Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `-FileVersionInfo`     | Affiche la version de l'exécutable du processus       |
| `-Id [PID]`     | Affiche le processus qui correspond au Process ID spécifié       |
| `-IncludeUserName`     | Affiche le propriétaire du processus        |
| `-InputObject [objet processus]`     | Affiche le processus qui correspond a l'objet processus spécifié         |
| `-Module`     | Affiche les modules chargés par les processus         |

# Exemples

# Voir aussi

Documentation de l'applet officielle
https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.management/get-process
