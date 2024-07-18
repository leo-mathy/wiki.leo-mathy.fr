---
title: Set-DnsServerGlobalQueryBlockList
description: 
published: true
date: 2024-07-18T13:40:05.766Z
tags: windows, powershell, rédaction incomplète
editor: markdown
dateCreated: 2024-07-16T18:11:24.036Z
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
