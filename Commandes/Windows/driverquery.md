---
title: driverquery
description: Affiche la liste des pilotes installés et leurs propriétés
published: true
date: 2025-05-04T14:52:40.623Z
tags: windows, commande
editor: markdown
dateCreated: 2024-07-19T10:48:29.657Z
---

# Introduction

Driverquery affiche la liste des pilotes installés et leurs propriétés.

# Syntaxe

`driverquery [options]`

# Options

| Option                                   | Description                                            |
| ---------------------------------------- | ------------------------------------------------------ |
| `/s [ordinateur]`                        | Exécute la commande sur un autre ordinateur            |
| `/u [domaine\utilisateur / utilisateur]` | Exécute la commande en tant que l'utilisateur spécifié |
| `/p [Mot de passe]`                      | Mot de passe de l'utilisateur associé à /u             |
| `/fo [table/list/csv]`                   | Spécifie la mise en forme                              |
| `/nh`                                    | N'affiche pas la ligne d'en-tête                       |
| `/v`                                     | Mode verbose                                           |
| `/si`                                    | Affiche les informations sur les pilotes signés        |
| `/?`                                     | Affiche l'aide                                         |

# Exemples

Afficher la liste des pilotes installés sur l'ordinateur 10.10.10.1 en tant que liste et en mode verbose

`driverquery /s 10.10.10.1 /fo list /v`
