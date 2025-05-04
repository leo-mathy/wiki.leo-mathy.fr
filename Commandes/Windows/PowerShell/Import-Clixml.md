---
title: Import-Clixml
description: Permet d'importer des objets PowerShell depuis un fichier en utilisant le format XML.
published: true
date: 2025-05-04T14:56:32.830Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-08-29T16:54:58.449Z
---

# Introduction

l'applet Import-Clixml permet d'importer des objets PowerShell depuis un fichier en utilisant le format XML. Peut être utilisé avec Export-Clixml.

# Syntaxe

`Import-Clixml [fichier] [paramètres]`

# Paramètres

| Paramètre               | Description                                                                                               |
| ----------------------- | --------------------------------------------------------------------------------------------------------- |
| `-First <nombre>`       | Importe uniquement le nombre d'objets spécifié.                                                           |
| `-IncludeTotalCount`    | Affiche le nombre total d'objets dans le fichier.                                                         |
| `-LiteralPath <chemin>` | Indique le fichier XML à importer littéralement (la valeur est utilisée exactement comme elle est tapée). |
| `-Path <chemin>`        | Indique le fichier XML à importer.                                                                        |
| `-Skip`                 | Précise le nombre d'objets à ignorer.                                                                     |

# Exemples

Affiche un objet powershell depuis le fichier services.xml.
`Import-Clixml '.\services.xml'`

Affiche les informations détaillées sur les processus
`$process = Import-Clixml '.\process.xml'`
`Get-Process $process`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.utility/import-clixml
