---
title: Netstat
description: Permet d'afficher les connexions TCP/UDP actives et de connaitre les services qui écoutent sur les ports.
published: true
date: 2024-07-16T16:51:23.198Z
tags: cmd, windows, powershell
editor: markdown
dateCreated: 2024-07-11T12:08:55.167Z
---

# Introduction

Netstat permet d'afficher les connexions TCP/UDP actives et de voir quels services écoutent sur quels ports. Cela peut permettre d'identifier les services accessibles depuis l'exterieur ou uniquement depuis la machine, et ainsi identifier des vulnérabilités.

# Syntaxe

`netstat [options]`

# Options

| Option                     | Description                                                                                                                    |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `-a`                       | Affiche toutes les connexions et tous les ports d'écoute                                                                       |
| `-n`                       | Affiche des adresses et numéros de ports en format numérique (n'affiche pas le nom de l'ordinateur pour désigner une addresse) |
| `-o`                       | Affiche le PID du processus associé à la connexion                                                                             |
| `-b`                       | Affiche l'éxecutable impliqué dans la création de chaque connexion                                                             |
| `-p [TCP/UDP/TCPv6/UDPv6]` | Affiche les connexions qui utilisent le protocole spécifié                                                                     |
| `-r`                       | Affiche la table de routage                                                                                                    |

# Exemples

Affiche toutes les connexions et ports d'écoute au format numérique ainsi que le PID du processus associé

`netstat -ano`
