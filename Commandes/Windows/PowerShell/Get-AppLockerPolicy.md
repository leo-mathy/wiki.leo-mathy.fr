---
title: Get-AppLockerPolicy
description: Voir la politique AppLocker locale, effective ou du domaine
published: true
date: 2024-10-25T20:30:21.549Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-07-11T10:23:43.013Z
---

# Introduction

La commande Get-AppLockerPolicy permet de voir la politique AppLocker, AppLocker permet de limiter les fichiers que les utilisateurs ou groupes sont autorisés à exécuter.

# Syntaxe

`Get-AppLockerPolicy [politique] [options]`

# Options

| Option                             | Description                                                          |
| ---------------------------------- | -------------------------------------------------------------------- |
| `-Local`                           | Renvoi la politique AppLocker locale                                 |
| `-Domain -LDAP [chemin de la GPO]` | Renvoi la politique AppLocker du domaine pour une GPO en particulier |
| `-Effective`                       | Renvoi la politique AppLocker effective                              |
| `-Xml`                             | Affiche la sortie au format XML                                      |

# Exemples

Renvoi la politique AppLocker effective

`Get-AppLockerPolicy -Effective`

Renvoi la politique AppLocker définie dans une GPO.

`Get-AppLockerPolicy -Domain -LDAP "LDAP:// DC13.Contoso.com/CN={31B2F340-016D-11D2-945F-00C04FB984F9},CN=Policies,CN=System,DC=Contoso,DC=com"`
