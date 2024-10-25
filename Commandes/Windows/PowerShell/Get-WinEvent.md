---
title: Get-WinEvent
description: Obtient les événements à partir des journaux des événements et des fichiers journaux
published: true
date: 2024-10-25T20:32:41.949Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-07-15T16:45:59.328Z
---

# Introduction

Get-WinEvent permet d'obtenir les événements à partir des journaux des événements et des fichiers journaux.

# Syntaxe

`Get-WinEvent [option]`

# Options

| option                        | Description                                                                                                 |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------- |
| `-ComputerName [ordinateur]`  | Spécifie le nom de l’ordinateur                                                                             |
| `-Credential [utilisateur]`   | Spécifie le nom d'utilisateur                                                                               |
| `-ListLog [log]`              | Spécifie les journaux des événements (wildcard autorisé)                                                    |
| `-ListProvider`               | Spécifie les fournisseurs de journaux d’événements (wildcard autorisé)                                      |
| `-LogName [log]`              | Spécifie le journal d’événement (virgule autorisé pour spécifier plusieurs journaux)                        |
| `-MaxEvents [nombre]`         | Définit le nombre maximal d’événements à lire                                                               |
| `-Path [chemin]`              | Spécifie le chemin d'accès des fichiers journaux                                                            |
| `-ProviderName [fournisseur]` | Spécifie les fournisseurs de journaux d’événements (virgule autorisé pour spécifier plusieurs fournisseurs) |
| `-Oldest`                     | Affiche les evenements les plus anciens en premier                                                          |

# Exemples

Lister les noms de tous les journaux:

`Get-WinEvent -ListLog *`

Voir les 5 derniers évenements du journal SECURITY:

`Get-WinEvent -logname SECURITY -MaxEvents 5`
