---
title: arp
description: Affiche et modifie les tables de traduction d'adresses IP en adresses physiques utilisées par le protocole de résolution d'adresses ARP
published: true
date: 2024-10-25T20:20:39.233Z
tags: windows, commande
editor: markdown
dateCreated: 2024-04-28T13:43:58.681Z
---

# Introduction

Affiche et modifie les tables de traduction d'adresses IP en adresses
physiques utilisées par le protocole de résolution d'adresses ARP.

# Syntaxe

`arp [paramètres]`

# Options

| Option                            | Description                     |
| --------------------------------- | ------------------------------- |
| `-a`                              | Affiche les entrées ARP actives |
| `-s [addresse ip] [addresse MAC]` | Ajoute une entrée statique      |

# Exemples

Voir les entrées de la table ARP

`arp -a`
