---
title: route
description: Permet d'afficher ou modifier la table de routage
published: true
date: 2024-07-11T09:59:23.790Z
tags: cmd, windows
editor: markdown
dateCreated: 2024-07-11T09:57:49.944Z
---

# Introduction

La commande route permet d'afficher ou modifier la table de routage, cela est utile pour voir les passerelles actives ou ajouter une nouvelle route par défaut.

# Syntaxe

`route [options]`

# Options

| Option                                                                                      | Description                                                                   |
| ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `PRINT`                                                                                     | Affiche la table de routage                                                   |
| `PRINT -4`                                                                                  | Affiche la table de routage IPv4                                              |
| `PRINT -6`                                                                                  | Affiche la table de routage IPv6                                              |
| `PRINT [recherche]*`                                                                        | Affiche la table de routage ou la valeure commence par une valeure spécifique |
| `DELETE [Adresse IP]`                                                                       | Supprime une route                                                            |
| `ADD [Adresse IP ou réseau de destination] [masque de sous réseau] [passerelle] [métrique]` | Ajoute une route statique                                                     |

# Exemples

Affiche toutes les routes actives

`route PRINT`

Affiche toutes les routes IPv4 actives

`route PRINT -4`

Affiche toutes les routes qui commencent par 192.168

`route PRINT 192.168*`
