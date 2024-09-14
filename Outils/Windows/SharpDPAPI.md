---
title: SharpDPAPI
description: Portage de certaines fonctionnalités DPAPI de mimikatz en C#. Contient aussi le sous projet SharpChrome (permet le déchiffrement avec DPAPI des logins et cookies).
published: true
date: 2024-09-14T07:23:53.378Z
tags: outil, windows, rédaction incomplète
editor: markdown
dateCreated: 2024-09-12T08:51:59.511Z
---

# Introduction

Portage de certaines fonctionnalités DPAPI de mimikatz en C#. Contient aussi le sous projet SharpChrome (permet le déchiffrement avec DPAPI des logins et cookies).

>  SharpDPAPI et SharpChrome sont disponible au téléchargement [ici](https://github.com/GhostPack/SharpDPAPI)
{.is-info}

# SharpDPAPI

## Syntaxe

`SharpDPAPI <module> [paramètres]`

### Paramètres du module backupkey

Le module backupkey permet de récupérer la clé de sauvegarde DPAPI d'un controlleur de domaine.

| Paramètre | Description |
| --------- | ----------- |
| `/nowrap`     | Désactive le formatage de sortie.         |
| `/server:<serveur>.<domaine>`     | Spécifie le contrôleur de domaine.         |
| `/file:<clé.pvk>`     | Exporte la clé de sauvegarde DPAPI au format .pvk.        |






# Voir aussi

Détails sur DPAPI
https://blog.harmj0y.net/redteaming/operational-guidance-for-offensive-user-dpapi-abuse/
