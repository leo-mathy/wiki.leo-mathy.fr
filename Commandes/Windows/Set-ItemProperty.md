---
title: Set-ItemProperty
description: Crée ou modifie la valeur d'une propriété d'un élément ou de clés de registre.
published: true
date: 2024-08-22T16:39:58.108Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-07-31T17:34:17.193Z
---

# Introduction

L'applet Set-ItemProperty permet de créer ou modifier la valeur d'une propriété d'un élément ou de clés de registre.

# Syntaxe

`Set-ItemProperty -Path <chemin> -Name <nom de la propriété> -Value <valeur> [paramètres]`

# Paramètres

| Paramètre                     | Description                                                                                                 |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------- | ------ | ----- | ----------- | ----- | --------- | -------------------------------------------------------------------------------------------- |
| `-Confirm`                    | Demande une confirmation avant l'exécution de la commande.                                                  |
| `-Exclude <élément>`          | Spécifie un élément à exclure de l'opération. L'utilisation d'une wildcard est possible.                    |
| `-Filter <élément>`           | Spécifie un élément à intégrer à l'opération. L'utilisation d'une wildcard est possible.                    |
| `-Force`                      | Force l'opération, sur les fichiers en lecture seule par exemple.                                           |
| `-Name <nom de la propriété>` | Précise le nom de la propriété à changer.                                                                   |
| `-PassThru`                   | Retourne la propriété changée comme sortie de commande (par défaut, cette commande ne génère par de sortie. |
| `-Path <chemin>`              | Précise le chemin de l'objet à modifier.                                                                    |
| `-Type <string                | ExpandString                                                                                                | Binary | DWord | MultiString | Qword | Unknown>` | Précise quel type de valeur ajouter dans l'entrée du registre (uniquement pour le registre). |
| `-Value <valeur>`             | Précise la valeur de la propriété ou de l'entrée dans le registre.                                          |
| `-WhatIf`                     | Ne lance pas la commande mais affiche les modifications si elle l'était.                                    |

# Exemples

Créer une entrée nommé "Numéro" dans la clé "Exemple" avec comme valeur 500.

`Set-ItemProperty -Path "HKLM:\Software\Exemple" -Name "Numéro" -Value 500`

# Voir aussi

[Documentation officielle de l'applet](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/set-itemproperty?view=powershell-7.4)
