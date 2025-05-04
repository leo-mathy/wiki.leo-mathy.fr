---
title: Compare-Object
description: Alias de diff et compare. Compare deux objets PowerShell.
published: true
date: 2025-05-04T14:55:54.167Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-10-06T10:37:17.555Z
---

# Introduction

Alias de diff et compare, Compare-Object permet de comparer des objets PowerShell.

# Syntaxe

`Compare-Object <objet(s) de référence> <objet(s) de différence> [paramètres]`

# Paramètres

| Paramètre                                    | Description                                                                                                                                              |
| -------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| `-CaseSensitive`                             | Indique que la comparaison doit comprendre la casse.                                                                                                     |
| `-Culture <culture>`                         | Indique la culture à utiliser.                                                                                                                           |
| `-DifferenceObject <objet(s) de différence>` | Indique le(s) objet(s) de différence. (comparé à la références)                                                                                          |
| `-ExcludeDifferent`                          | N'affiche pas les éléments non égaux entre les deux objets. (à utiliser avec -IncludeEqual)                                                              |
| `-IncludeEqual`                              | Affiche uniquement les éléments égaux entre les deux objets.                                                                                             |
| `-PassThru`                                  | Ne crée par un nouvel objet de comparaison comportant les différences mais conserve les objets d'origine.                                                |
| `-Property <propriétés                       | bloc de script>`                                                                                                                                         | Compare uniquement certaines propriétés. |
| `-ReferenceObject <objet(s) de référence>`   | Indique que la comparaison doit comprendre la casse.                                                                                                     |
| `-SyncWindow <nombre>`                       | Défini le nombre d'objets adjacents à inspecter quand la recherche ne trouve pas l'objet à la même position. Par défaut, tous les objets sont inspectés. |

# Exemples

Compare les propriétés de deux boites mails Exchange
`Compare-Object -ReferenceObject (Get-mailbox -identity user1@company.domain) -DifferenceObject (Get-mailbox -identity user2@company.domain)`

# Voir aussi

Documentation officielle:
https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/compare-object
