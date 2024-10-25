---
title: PSSQLite
description: Module PowerShell permettant d'interagir avec des fonctionnalités limités sur une base SQLite.
published: true
date: 2024-10-25T20:46:28.958Z
tags: outil, windows, powershell
editor: markdown
dateCreated: 2024-08-31T16:04:31.046Z
---

# Introduction

PSSQLite est un module PowerShell permettant d'interagir avec des fonctionnalités limités sur une base SQLite.

> Le module PowerShell est disponible au téléchargement [ici](https://github.com/RamblingCookieMonster/PSSQLite)
> {.is-info}

# Syntaxe

`Invoke-SqliteQuery -Query <requête> -DataSource <source> [paramètres]`

# Paramètres

| Paramètre                         | Description                                                                                                                                    |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | -------- | ------------- | --------------------------------------------------- |
| `-Query <requête>`                | Spécifie la requête à effectuer.                                                                                                               |
| `-InputFile <fichier>`            | Spécifie la requête à effectuer depuis un fichier.                                                                                             |
| `-QueryTimeout <secondes>`        | Spécifie le nombre de secondes avant que la requête expire                                                                                     |
| `-As <DataSet                     | DataTable                                                                                                                                      | array of DataRow | PSObject | Single Value` | Spécifie quel est le type de sortie de la commande. |
| `-SqlParameters <paramètres SQL>` | Indique les paramètres SQL sous forme de table de hachage. (présenté comme des variables)                                                      |
| `-SQLiteConnection <connexion>`   | Spécifie une connexion existante à utiliser (ne ferme pas la connexion après utilisation)                                                      |
| `-DataSource <source>`            | Spécifie une ou plusieurs sources de données SQLite à interroger.                                                                              |
| `-AppendDataSource`               | Ajoute la source de donnée lors de la sortie lorsque "PSObject" (Objet Powershell) ou "array of DataRow" est défini au niveau du paramètre -As |

# Exemples

Affiche toutes les entrées de la table "NAMES"
`Invoke-SqliteQuery -DataSource "C:\database.SQLite" -Query "SELECT * FROM NAMES"`

# Voir aussi

Détails du module et explications
https://ramblingcookiemonster.github.io/SQLite-and-PowerShell/

Paramètres SQL SQLite
https://learn.microsoft.com/en-us/dotnet/standard/data/sqlite/parameters

Explications des paramètres SQL
https://blog.codinghorror.com/give-me-parameterized-sql-or-give-me-death/

Tableaux et tables de hachage
https://learn.microsoft.com/fr-fr/powershell/scripting/learn/deep-dives/everything-about-hashtable
