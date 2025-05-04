---
title: Get-ADGroupMember
description: Permet de récupérer les membres d'un groupe Active Directory
published: true
date: 2025-05-04T14:55:58.470Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-07-16T17:27:31.984Z
---

# Introduction

la commande Get-ADGroupMember permet de récupérer les membres d'un groupe Active Directory, les membres peuvent être des utilisateurs, groupes ou ordinateurs.

# Syntaxe

`Get-ADGroupMember -Identity [groupe] [options]`

# Options

| Option                      | Description                                                       |
| --------------------------- | ----------------------------------------------------------------- |
| `-Credential [utilisateur]` | Spécifie avec quel utilisateur lancer la commande                 |
| `-Partition [partition]`    | Spécifie le nom distinct de la partition d'un Active Directory    |
| `-Recursive`                | Affiche récursivement les utilisateurs (sous groupes par exemple) |
| `-Server[serveur]`          | Spécifie le serveur à interroger                                  |

# Exemples

Affiche tous les membres du groupe Administrateurs récursivement

`Get-ADGroupMember -Identity Administrateurs -Recursive`
