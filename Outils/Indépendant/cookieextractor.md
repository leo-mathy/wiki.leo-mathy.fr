---
title: cookieextractor
description: Extrait les cookies souhaités depuis la base de données sqlite FireFox.
published: true
date: 2024-10-26T14:14:43.752Z
tags: outil, indépendant
editor: markdown
dateCreated: 2024-10-26T14:14:43.752Z
---

# Introduction

cookieextractor permet d'extraire les cookies souhaités depuis la base de données sqlite FireFox.

> cookieextractor est disponible au téléchargement [ici](https://github.com/juliourena/plaintext/blob/master/Scripts/cookieextractor.py)
> {.is-info}

Par défaut, la base sqlite de FireFox est situé à l'emplacement suivant:
`APPDATA\Mozilla\Firefox\Profiles\<aléatoire>.default-release\cookies.sqlite`

> Il est possible de déplacer le fichier pour l'exploiter en mode hors ligne.
> {.is-info}

# Syntaxe

`cookieextractor.py --dbpath <chemin vers le fichier sqlite> --host <hôte du cookie> --cookie <nom du cookie>`

# Paramètres

| Paramètre                                  | Description                                            |
| ------------------------------------------ | ------------------------------------------------------ |
| `--dbpath <chemin vers le fichier sqlite>` | Précise le chemin vers la base de données sqlite.      |
| `--host <hôte du cookie>`                  | Précise le domaine ou sous-domaine du cookie (l'hôte). |
| `--cookie <nom du cookie>`                 | Précise le nom du cookie à récupèrer.                  |

# Exemples

cookieextractor.py --dbpath "./cookies.sqlite" --host mydomain --cookie token

# Voir aussi

Documentation Mozilla sur les cookies:
https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
