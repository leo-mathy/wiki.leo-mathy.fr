---
title: dnscmd
description: Permet de gérer un serveur DNS
published: true
date: 2024-07-16T16:44:42.921Z
tags: cmd, windows, powershell, rédaction incomplète
editor: markdown
dateCreated: 2024-07-16T16:42:05.458Z
---

# Introduction

dnscmd permet de gérer un serveur DNS depuis la ligne de commande.

# Syntaxe

`dnscmd [commande] [options]`

# Options

| Option                                         | Description                                           |
| ---------------------------------------------- | ----------------------------------------------------- |
| `dnscmd /clearcache`                           | Efface le cache DNS des enregistrements de ressources |
| `/config /serverlevelplugindll [fichier .dll]` | Spécifie le chemin d’accès d’un plug-in personnalisé. |

# Exemples