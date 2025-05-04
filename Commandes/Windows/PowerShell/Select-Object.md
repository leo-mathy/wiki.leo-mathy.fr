---
title: Select-Object
description: Sélectionne des objets ou des propriétés contenues dans les objets.
published: true
date: 2025-05-04T14:56:43.648Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-10-26T13:28:10.099Z
---

# Introduction

Select-Object (alias de select) est une applet PowerShell qui permet de sélectionner des objets ou des propriétés contenues dans les objets.

# Syntaxe

`Select-Object <objet(s)> [paramètres]`

# Paramètres

| Paramètre                         | Description                                                                                              |
| --------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `-CaseInsensitive`                | A utiliser avec -Unique. Ne respecte pas la casse lors du traitement.                                    |
| `-ExcludeProperty <propriété(s)>` | Exclu des propriétés du traitement.                                                                      |
| `-ExpandProperty <propriété>`     | Essaye de développer la propriété indiquée.                                                              |
| `-First <nombre>`                 | Spécifie le nombre d'objets à sélectionner depuis le début si plusieurs objets d'entrés sont présents.   |
| `-Index <index>`                  | Spécifie quels index sélectionner.                                                                       |
| `-InputObject <objet(s)>`         | Spécifie le ou les objets à traiter.                                                                     |
| `-Last <nombre>`                  | Spécifie le nombre d'objets à sélectionner depuis la fin si plusieurs objets d'entrés sont présents.     |
| `-Property <propriété(s)>`        | Sélectionne les propriétés de l'objet. Wildcard utilisable pour sélectionner toutes les propriétés.      |
| `-Skip <nombre>`                  | Spécifie le nombre d'objets à ne pas traiter depuis le début si plusieurs objets d'entrés sont présents. |
| `-SkipIndex <index>`              | Spécifie quels index ne pas sélectionner.                                                                |
| `-SkipLast <nombre>`              | Spécifie le nombre d'objets à ne pas traiter depuis la fin si plusieurs objets d'entrés sont présents.   |
| `-Unique`                         | sélectionne uniquement les objets qui ont les mêmes propriétés.                                          |
| `-Wait`                           | Désactive l'optimisation PowerShell qui exécute les commandes dans l'ordre.                              |

# Exemples

Sélectionne toutes les propriétés des fichiers et dossiers dans le répertoire actuel
`Get-ChildItem | select *`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.utility/select-object
