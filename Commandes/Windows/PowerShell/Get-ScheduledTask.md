---
title: Get-ScheduledTask
description: Récupère les tâches planifiées locales.
published: true
date: 2025-05-04T14:56:24.521Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-10-26T19:05:26.400Z
---

# Introduction

Get-ScheduledTask est une applet PowerShell qui permet de récupérer les tâches planifiées locales.

# Syntaxe

`Get-ScheduledTask [paramètres]`

# Paramètres

| Paramètre                          | Description                                                                                                            |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `-AsJob`                           | Lance l'opération en arrière-plan.                                                                                     |
| `-CimSession <ordinateur/session>` | Exécute la commande sur une session distante.                                                                          |
| `-TaskName <tâche(s)>`             | Récupère la ou les tâches en fonction de leur nom. La wildcard est utilisable.                                         |
| `-TaskPath <namespace>`            | Récupère la ou les tâches en fonction de leur namespace. La wildcard est utilisable. Le namespace est root par défaut. |
| `-ThrottleLimit <nombre>`          | Spécifie le nombre maximal d'opérations pour exécuter cette commande. Par défaut cela est défini automatiquement.      |

# Exemples

Récupère les tâches qui possèdent le mot "backup" dans leur nom.
`Get-ScheduledTask -TaskName *backup*`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/en-us/powershell/module/scheduledtasks/get-scheduledtask
