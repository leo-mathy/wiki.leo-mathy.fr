---
title: Get-DnsServerGlobalQueryBlockList
description: Affiche la liste globale de requête bloquées sur un serveur DNS. Le serveur DNS ignore les requêtes dont le nom est dans la liste
published: true
date: 2024-07-18T14:00:54.610Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-07-18T13:47:40.922Z
---

# Introduction

Affiche la liste globale de requête bloquées sur un serveur DNS. Le serveur DNS ignore les requêtes dont le nom est dans la liste.

# Syntaxe

`Get-DnsServerGlobalQueryBlockList [options]`

# Options

| Option                             | Description                                                     |
| ---------------------------------- | --------------------------------------------------------------- |
| `-AsJob`                           | Exécute la commande en arrière-plan                             |
| `-CimSession [Session/ordinateur]` | Exécute la commande sur une session spécifique ou un ordinateur |
| `-ComputerName [ordinateur]`       | Spécifie l'ordinateur distant                                   |

# Exemples

Affiche la liste globale de requête bloquées sur le serveur DNS 10.10.10.1.

`Get-DnsServerGlobalQueryBlockList -ComputerName 10.10.10.1`
