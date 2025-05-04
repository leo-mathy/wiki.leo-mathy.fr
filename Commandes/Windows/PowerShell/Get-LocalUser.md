---
title: Get-LocalUser
description: Récupère les utilisateurs locaux.
published: true
date: 2025-05-04T14:56:15.834Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-10-26T18:57:14.646Z
---

# Introduction

Get-LocalUser permet de récupérer les utilisateurs locaux.

# Syntaxe

`Get-LocalUser [paramètres]`

# Paramètres

| Paramètre                      | Description                                         |
| ------------------------------ | --------------------------------------------------- |
| `-Name <nom de l'utilisateur>` | Récupère l'utilisateur indiqué.                     |
| `-SID <Security Identifier>`   | Récupère l'utilisateur qui possède le SID spécifié. |

# Exemples

Récupère l'utilisateur local nommé BackupAccount.
`Get-LocalUser -Name BackupAccount`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.localaccounts/get-localuser
