---
title: takeown
description: Permet de devenir le propriétaire d'un fichier ou dossier
published: true
date: 2024-10-25T20:27:04.504Z
tags: cmd, commande
editor: markdown
dateCreated: 2024-07-14T19:26:54.028Z
---

# Introduction

La commande takeown permet de devenir le propriétaire d'un fichier ou dossier.

# Syntaxe

`takeown [repertoire/fichier] [options]`

# Options

| Option                                   | Description                                                                                                                                                                      |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/s [ordinateur]`                        | Spécifie sur quel ordinateur effectuer l'opération                                                                                                                               |
| `/u [domaine\utilisateur / utilisateur]` | Spécifie sous quel utilisateur lancer la commande                                                                                                                                |
| `/p [mot de passe]`                      | Spécifie le mot de passe à utiliser avec l'option /u                                                                                                                             |
| `/f [fichier]`                           | Spécifie le fichier, wildcard utilisable.                                                                                                                                        |
| `/a`                                     | Désigne le propriétaire comme le groupe administrateur                                                                                                                           |
| `/r`                                     | Effectue l'opération récursivement                                                                                                                                               |
| `/d [Y/N]`                               | Lors d'une opération récursive, que faire lorsque les droits "afficher le contenu du dossier" n'est pas présent. Choisir Y pour prendre le controle du dossier ou N pour ignorer |

# Exemples

Prendre le controle du dossier v:\temp\ récursivement, même sur les dossiers ou l'on ne peut pas lister le contenu.

`takeown v:\temp\ /r /d Y`

Prendre le contrôle des fichiers à l'intérieur du dossier v:\temp\

`takeown v:\temp\*`
