---
title: Test-AppLockerPolicy
description: Tester une politique AppLocker
published: true
date: 2024-10-25T20:34:57.779Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-07-11T10:33:18.189Z
---

# Introduction

La commande Test-AppLockerPolicy permet de tester une politique AppLocker, AppLocker permet de limiter les fichiers que les utilisateurs ou groupes sont autorisés à exécuter.

# Syntaxe

`Test-AppLockerPolicy -XMLPolicy [Chemin du fichier XML qui contient la politique] [options]`

# Options

| Option                                                         | Description                                                                                                           |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `-Path [chemin de l'éxecutable]`                               | Précise quel éxecutable doit être testé, plusieurs éxecutables peuvent être précisés avec des virgules et/ou wildcard |
| `-User [Utilisateur / nom d'utilisateur SAM / SID]`            | Précise avec quel utilisateur tester la politique                                                                     |
| `-XmlPolicy [Chemin du fichier XML qui contient la politique]` | Précise le fichier avec lequel tester la politique                                                                    |

# Exemples

Tester si le groupe "Everyone" a accès à cmd.exe avec la politique AppLockerPolicy.xml

`Test-AppLockerPolicy -XMLPolicy .\AppLockerPolicy.xml -User Everyone -Path C:\Windows\system32\cmd.exe`

Tester si le groupe "Everyone" a accès à cmd.exe et powershell.exe avec la politique AppLockerPolicy.xml

`Test-AppLockerPolicy -XMLPolicy .\AppLockerPolicy.xml -User Everyone -Path C:\Windows\system32\cmd.exe, C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`

Tester si le groupe "Everyone" a accès à aux éxecutables .exe dans C:\Windows\System32\ avec la politique AppLockerPolicy.xml

`Test-AppLockerPolicy -XMLPolicy .\AppLockerPolicy.xml -User Everyone -Path C:\Windows\System32\*.exe`
