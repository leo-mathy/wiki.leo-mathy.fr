---
title: systeminfo
description: Affiche les informations de configuration du système d’exploitation
published: true
date: 2024-10-25T20:26:50.159Z
tags: windows, commande
editor: markdown
dateCreated: 2024-07-11T11:21:37.863Z
---

# Introduction

La commande systeminfo permet d'afficher les informations détaillées sur le système d'exploitation, comme la version de Windows ou encore la date du dernier démarrage. Cela peut être utile pour voir la dernière version de patch ou encore si la machine est virtuelle.

# Syntaxe

`systeminfo [options]`

# Options

| Option                                   | Description                                         |
| ---------------------------------------- | --------------------------------------------------- |
| `/S [ordinateur]`                        | Spécifie le système distant sur lequel se connecter |
| `/U [DOMAINE\Utilisateur / Utilisateur]` | précise quel utilisateur éxecute la commande        |

# Exemples

Affiche les informations sur le système d'exploitation

`systeminfo`
