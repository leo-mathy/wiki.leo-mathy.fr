---
title: Get-Service
description: Obtient les services sur l’ordinateur.
published: true
date: 2024-08-28T14:24:51.977Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-08-28T14:24:51.977Z
---

# Introduction

L'applet Get-Service permet d'obtenir les services sur l’ordinateur.

# Syntaxe

`Get-Service [nom de service] [paramètres]`

# Paramètres

| Paramètre                                   | Description                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------- |
| `-DependentServices [nom du service]`       | Affiche les services qui dépendent du service spécifié                            |
| `-DisplayName [nom d'affichage du service]` | Affiche le service qui correspond au nom d'affichage spécifié                     |
| `-Exclude [nom du service]`                 | Exclut de l'opération le ou les services spécifiés (wildcard autorisé)            |
| `-Include [nom du service]`                 | Inclut à l'opération le ou les services spécifiés (wildcard autorisé)             |
| `-InputObject [objet ServiceController]`    | Affiche le ou les services qui correspondent a l'objet ServiceController spécifié |
| `-Name [nom du service]`                    | Affiche le nom du service à récupérer                                             |
| `-RequiredServices [nom du service]`        | Affiche les services qui sont requis par le service spécifié                      |

# Exemples

Affiche les services qui ont dans le nom d'affichage le mot "network".
`Get-Service -Displayname "*network*"`

Affiche les services requis par le service GoogleChromeElevationService
`Get-Service "GoogleChromeElevationService" -RequiredServices`

# Voir aussi

Documentation officielle de l'applet
https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.management/get-service
