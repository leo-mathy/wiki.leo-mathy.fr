---
title: Test-AppLockerPolicy
description: Tester une politique AppLocker
published: true
date: 2024-07-11T10:33:18.189Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-07-11T10:33:18.189Z
---

# Introduction

La commande Test-AppLockerPolicy permet de tester une politique AppLocker, AppLocker permet de limiter les fichiers que les utilisateurs ou groupes sont autorisés à exécuter.

# Syntaxe

`Test-AppLockerPolicy -XMLPolicy [politique] [options]`

# Options

| Option                             | Description                                                          |
| ---------------------------------- | -------------------------------------------------------------------- |
| `-Path [chemin de l'éxecutable]`                           | Précise quel éxecutable doit être testé                                |
| `-User [Utilisateur / nom d'utilisateur SAM / SID` | Renvoi la politique AppLocker du domaine pour une GPO en particulier |
| `-XmlPolicy [Chemin du fichier XML quienvoi la politique AppLocker effective                              |
| `-Xml`                             | Affiche la sortie au format XML                                      |

# Exemples

