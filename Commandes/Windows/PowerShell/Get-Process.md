---
title: Get-Process
description: Obtient les processus qui s’exécutent sur l’ordinateur local.
published: true
date: 2025-05-04T14:56:22.415Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-08-28T14:01:30.958Z
---

# Introduction

L'applet Get-Process permet d'obtenir les processus qui s’exécutent sur l’ordinateur local.

# Syntaxe

`Get-Process [processus] [paramètres]`

# Paramètres

| Paramètre                        | Description                                                                |
| -------------------------------- | -------------------------------------------------------------------------- |
| `-FileVersionInfo`               | Affiche la version de l'exécutable du processus                            |
| `-Id [PID]`                      | Affiche le processus qui correspond au Process ID spécifié                 |
| `-IncludeUserName`               | Affiche le propriétaire du processus                                       |
| `-InputObject [objet processus]` | Affiche le ou les processus qui correspondent a l'objet processus spécifié |
| `-Module`                        | Affiche les modules chargés par les processus                              |
| `-Name`                          | Affiche le processus qui correspond au nom de processus spécifié           |

# Exemples

Obtenir tous les processus actifs
`Get-Process`

Obtenir les processus chrome et lsass
`Get-Process chrome, lsass`

Obtenir la version de l'exécutable du processus lsass. (C:\Windows\system32\lsass.exe)
`Get-Process lsass -FileVersionInfo`

# Voir aussi

Documentation de l'applet officielle
https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.management/get-process
