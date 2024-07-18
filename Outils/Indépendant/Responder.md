---
title: Responder
description: Permet d'empoisonner certains protocoles (LLMNR;NBT-NS;MDNS) et permet la création de serveurs rogue (proxy WPAD, HTTP) pour la récupération d'identifiants
published: true
date: 2024-07-18T14:53:24.803Z
tags: outil
editor: markdown
dateCreated: 2024-07-18T14:53:24.803Z
---

# Introduction

Permet d'empoisonner certains protocoles (LLMNR;NBT-NS;MDNS) et permet la création de serveurs rogue (proxy WPAD, HTTP) pour la récupération d'identifiants

> Responder est disponible au téléchargement ici: https://github.com/lgandx/Responder
{.is-info}


# Syntaxe

`Set-DnsServerGlobalQueryBlockList [options]`

# Options

| Option                             | Description                                                                                          |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `-AsJob`                           | Exécute la commande en arrière-plan                                                                  |
| `-CimSession [Session/ordinateur]` | Exécute la commande sur une session spécifique ou un ordinateur                                      |
| `-ComputerName [ordinateur]`       | Spécifie l'ordinateur distant                                                                        |
| `-Confirm`                         | Demande une confirmation avant d'exécuter la commande                                                |
| `-Enable [True/False]`             | Active ou désactive la liste globale de requêtes bloquées sur un serveur DNS                         |
| `-List [noms]`                     | Modifie les entrées bloqués                                                                          |
| `-PassThru`                        | Affiche la liste globale de requêtes bloquées sur un serveur DNS après l'exécution de la commande |
| `-WhatIf`                          | N'exécute pas la commande mais indique ce qui se passerai si la commande était exécuté               |

# Exemples

Modifie la liste globale de requête bloquées sur le serveur DNS 10.10.10.1, pour que le serveur ignore les requètes vers le nom ISATAP.

`Set-DnsServerGlobalQueryBlockList -ComputerName 10.10.10.1 -List "ISATAP"`

Désactive la liste globale de requêtes bloquées sur le serveur DNS.

`Set-DnsServerGlobalQueryBlockList -Enable False`
