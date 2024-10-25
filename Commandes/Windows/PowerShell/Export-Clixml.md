---
title: Export-Clixml
description: Permet d'exporter des objets PowerShell dans un fichier en utilisant le format XML.
published: true
date: 2024-10-25T20:29:51.249Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-08-29T16:37:58.735Z
---

# Introduction

l'applet Export-Clixml permet d'exporter des objets PowerShell dans un fichier en utilisant le format XML. Peut être utilisé avec Import-Clixml.

> Sur les systèmes Windows, les objets informations d'identifications sont chiffrés avec DPAPI, le fichier ne peut donc pas être utilisé sur un autre ordinateur ou par un autre utilisateur.
> {.is-info}

# Syntaxe

`Export-Clixml <chemin> <objet powershell> [paramètres]`

# Paramètres

| Paramètre                         | Description                                                                                                                    |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `-Confirm`                        | Demande confirmation avant l'exécution.                                                                                        |
| `-Depth <nombre>`                 | Précise le nombre de niveaux d'objets contenus inclus dans le fichier (2 par défaut).                                          |
| `-Encoding <encodage>`            | Précise l'encodage à utiliser lors de la création du fichier XML (ascii;ansi;utf8...).                                         |
| `-Force`                          | Force l'opération en remplace le fichier de sortie même s'il est en lecture seule.                                             |
| `-InputObject <objet powershell>` | Précise l'objet powershell à exporter vers le fichier.                                                                         |
| `-LiteralPath <chemin litéral>`   | Indique le fichier XML vers lequel l'objet est exporté littéralement (la valeur est utilisée exactement comme elle est tapée). |
| `-NoClobber`                      | Ne remplace pas le contenu d'un fichier si celui-ci existe déjà.                                                               |
| `-Path <chemin>`                  | Indique le fichier XML vers lequel l'objet est exporté.                                                                        |
| `-WhatIf`                         | N'exécute pas la commande mais indique ce qui se passe lors de son exécution.                                                  |

# Exemples

Exporte l'objet d'informations d'identifications vers le fichier creds.xml
`Get-Credential | Export-Clixml -Path '.\creds.xml'`

# Voir aussi

Documentation officielle de l'applet
https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.utility/export-clixml
