---
title: Get-Content
description: Permet d'afficher le contenu d'un fichier
published: true
date: 2024-07-16T16:46:51.036Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-07-13T10:11:38.720Z
---

# Introduction

L'applet powerhsell Get-Content permet d'afficher le contenu d'un fichier

# Syntaxe

`Get-Content [options/fichier]`

# Options

| Option                         | Description                                       |
| ------------------------------ | ------------------------------------------------- |
| `-Encoding [encodage]`         | Spécifie le type d'encodage (ascii;ansi;utf8...)  |
| `-Exclude [élement ou modèle]` | Exclu un élement ou modèle, par exemple \*.txt    |
| `-Path [repertoire]`           | Spécifie le repertoire à utiliser                 |
| `-Filter`                      | Spécifie le filtre à utiliser, par exemple \*.txt |

# Exemples

Affiche le contenu des fichiers .txt dans le repertoire C:\Temp\ tout en excluant les fichiers .log

`Get-Content -Path C:\Temp\* -Filter *.txt -Exclude *.log`