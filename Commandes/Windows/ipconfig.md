---
title: ipconfig
description: Commande permettant d'afficher la configuration de carte(s) réseau
published: true
date: 2024-10-25T20:23:10.135Z
tags: windows, commande
editor: markdown
dateCreated: 2024-04-28T13:32:25.385Z
---

# Introduction

La commande ipconfig, permet d'afficher la configuration de carte(s) réseau ou d'effectuer des opérations simple sur celle(s)-ci comme le renouvellement des beaux dhcp.

# Syntaxe

`ipconfig [paramètres] [nom de la carte]`

> si aucune carte n'est spécifié, toutes les cartes seront concernées
> {.is-info}

# Options

| Option        | Description                                                                  |
| ------------- | ---------------------------------------------------------------------------- |
| `/all`        | affiche toutes les informations des cartes                                   |
| `/release`    | Libère le bail DHCP                                                          |
| `/renew`      | Libère le bail DHCP et redemande une autre addresse IP via le protocole DHCP |
| `/flushdns`   | Purge le cache de résolution DNS                                             |
| `/displaydns` | Affiche le contenu du cache de résolution DNS                                |

# Exemples

Affiche toutes les informations de toutes les cartes réseau

`ipconfig /all`

Libère le bail DHCP et redemande une autre addresse IP via le protocole DHCP, sur toutes les cartes

`ipconfig /renew`
