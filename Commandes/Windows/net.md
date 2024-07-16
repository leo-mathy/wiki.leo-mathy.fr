---
title: net
description: Les commandes Net suivantes peuvent être utilisées pour effectuer des opérations sur des groupes, des utilisateurs, des stratégies de compte, des partages, etc
published: true
date: 2024-07-16T18:10:07.592Z
tags: cmd, windows, powershell, rédaction incomplète
editor: markdown
dateCreated: 2024-07-11T12:35:24.269Z
---

# Introduction

Les commandes Net suivantes peuvent être utilisées pour effectuer des opérations sur des groupes, des utilisateurs, des stratégies de compte, des partages, etc.

# Syntaxe

`net [options]`

# Options

| Option                      | Description                                                                  |
| --------------------------- | ---------------------------------------------------------------------------- |
| `user`                      | Affiche les utilisateurs locaux                                              |
| `user [utilisateur local]`  | Affiche les détails à propos d'un utilisateur local                          |
| `accounts`                  | Affiche la politique de mot de passe et 'autres informations sur les comptes |
| `localgroup`                | Affiche les comptes locaux                                                   |
| `localgroup [groupe local]` | Affiche les détails à propos d'un groupe local                               |

# Exemples

Affiche les détails sur le groupe Utilisateurs

`net localgroup Utilisateurs`
