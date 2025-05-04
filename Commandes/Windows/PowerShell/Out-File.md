---
title: Out-File
description: Envoie la sortie vers un fichier
published: true
date: 2025-05-04T14:56:41.494Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-07-19T12:29:53.066Z
---

# Introduction

Out-File permet d'envoyer la sortie vers un fichier.

# Syntaxe

`Out-File -FilePath [chemin du fichier de sortie] -InputObject [objet powershell] [options]`

> l'entrée de l'applet Out-File est -InputObject
> {.is-info}

# Options

| Option                                    | Description                                                                            |
| ----------------------------------------- | -------------------------------------------------------------------------------------- |
| `-Append`                                 | Ajoute la sortie à un fichier (remplace par défaut)                                    |
| `-Confirm`                                | Demande une confirmation avant d'exécuter la commande                                  |
| `-Encoding [encodage]`                    | Spécifie le type d'encodage (ascii;ansi;utf8...)                                       |
| `-FilePath [chemin du fichier de sortie]` | Spécifie le chemin d'accès au fichier de sortie                                        |
| `-Force`                                  | Remplace le fichier si celui-ci est en lecture seule                                   |
| `-InputObject [objet powershell]`         | Spécifie les objets à écrire dans le fichier                                           |
| `-NoClobber`                              | Ne remplace pas un fichier déjà existant                                               |
| `-NoNewline`                              | Ne reviens pas à la ligne                                                              |
| `-WhatIf`                                 | N'exécute pas la commande mais indique ce qui se passerai si la commande était exécuté |

# Exemples

Envoi le resultat de la commande Get-Process vers le fichier result.txt

`out-file -InputObject $(Get-Process) -FilePath result.txt`

Envoi le resultat de la commande Get-Process vers le fichier result.txt

`Get-Process | out-file -FilePath result.txt`
