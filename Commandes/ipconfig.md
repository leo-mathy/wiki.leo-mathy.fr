---
title: ipconfig
description: Commande permettant d'afficher la configuration de carte(s) réseau
published: true
date: 2024-04-28T13:40:48.230Z
tags: cmd, windows
editor: markdown
dateCreated: 2024-04-28T13:32:25.385Z
---

# Introduction

la commande ipconfig, permet d'afficher la configuration de carte(s) réseau ou d'effectuer des opérations simple sur celle(s)-ci comme le renouvellement des beaux dhcp.

# Synopsis

`ipconfig [paramètres] [nom de la carte]`

> si aucune carte n'est spécifié, toutes les cartes seront concernées
{.is-info}


# Options

| Raccourci                       | Description                         |
| ------------------------------- | ----------------------------------- |
| `/all`                   | affiche toutes les informations des cartes        |
| `/release` | Libère l’adresse IPv4 pour la carte spécifiée |
| `/flushdns`           | Purge le cache de résolution DNS   |
| `/displaydns`           | Affiche le contenu du cache de résolution DNS |
