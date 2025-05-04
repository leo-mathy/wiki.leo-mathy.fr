---
title: Set-ItemProperty
description: Crée ou modifie la valeur d'une propriété d'un élément ou de clés de registre.
published: true
date: 2025-05-04T14:56:50.117Z
tags: windows, commande, powershell
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

Modifier la valeur de la propriété "CreationTime" (date de création) du fichier pour "01/01/2000 00:00:01".

`Set-ItemProperty C:\temp\exemple.txt CreationTime "01/01/2000 00:00:01"`

# Voir aussi

[Documentation officielle de l'applet](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/set-itemproperty?view=powershell-7.4)
