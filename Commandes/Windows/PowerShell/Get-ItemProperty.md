---
title: Get-ItemProperty
description: Récupère la valeur d'une propriété d'un élément ou de clés de registre.
published: true
date: 2024-10-26T12:58:28.792Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-10-26T12:58:28.792Z
---

# Introduction

L'applet Get-ItemProperty permet de récupérer la valeur d'une propriété d'un élément ou de clés de registre.

# Syntaxe

`Set-ItemProperty <élement> [paramètres]`

# Paramètres

| Paramètre                                      | Description                                                                              |
| ---------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `-Credential <utilisateur/objet PScredential>` | Exécute la commande en tant qu'un autre utilisateur.                                     |
| `-Exclude <élément>`                           | Spécifie un élément à exclure de l'opération. L'utilisation d'une wildcard est possible. |
| `-Filter <élément>`                            | Spécifie un élément à intégrer à l'opération. L'utilisation d'une wildcard est possible. |
| `-Include`                                     | Spécifie un élément à inclure à l'opération. L'utilisation d'une wildcard est possible.  |
| `-LiteralPath <chemin>`                        | Précise le chemin littéral de l'objet à récupérer.                                       |
| `-Name <nom de la propriété>`                  | Précise le nom de la propriété à récupérer.                                              |
| `-Path <chemin>`                               | Précise le chemin de l'objet à modifier.                                                 |

# Exemples

Récupère une entrée nommé "Numéro" dans la clé "Exemple".

`Get-ItemProperty -Path "HKLM:\Software\Exemple" -Name "Numéro"`

Récupère toutes les propriétés du fichier exemple.txt.

`Get-ItemProperty C:\temp\exemple.txt`

# Voir aussi

[Documentation officielle de l'applet](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-itemproperty)
