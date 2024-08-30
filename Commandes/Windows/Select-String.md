---
title: Select-String
description: Recherche du texte dans les fichiers et des chaînes.
published: true
date: 2024-08-30T16:43:28.492Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-08-30T16:17:34.831Z
---

# Introduction

L'applet Select-String permet de chercher du texte dans les fichiers et des chaînes.

# Syntaxe

`Select-String <recherche> <fichier|objet powershell> [paramètres]`

# Paramètres

| Paramètre     | Description                                                                                                                    |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `-AllMatches` | Continue la recherche sur la même ligne si une correspondance est trouvée (Par défaut la recherche passe à la ligne suivante). |
| `-CaseSensitive`           | N'ignore pas la casse des caractères.                 |
| `-Context <nombre>`          | Précise le nombre de lignes à capturer avant et après le résultat.                 |
| `-Culture <culture>`          | Spécifie la culture de la recherche (utile pour faire des recherches dans d'autres langages)                 |
| `-Encoding <codage>`          | Précise l'encodage à utiliser pour la recherche (ascii;ansi;utf8...).                |
| `-Exclude <élement>`     | Exclu des fichiers de la recherche. Wildcard utilisable.                |
| `-Include <élement>`           | Inclus des fichiers de la recherche. Wildcard utilisable.                 |
| `-InputObject <objet powershell>`          | Spécifie le texte à rechercher à l'aide d'un objet powershell.                 |
| `-List`          | Passe au fichier suivant dès que la recherche à trouvé un résultat.                 |
| `-LiteralPath <chemin>`                 | Indique le cheralement (la valeur est utilisée exactement comme elle est tapée).

| `-Exclude <élement>`           | ...                 |
| `-Exclude <élement>`          | ...                 |
| `-Exclude <élement>`           | ...                 |

# Exemples

# Voir aussi
