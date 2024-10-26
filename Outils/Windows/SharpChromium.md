---
title: SharpChromium
description: Extrait des informations (cookie, historique, informations d'identification) depuis Google Chrome, Microsoft Edge et Microsoft Edge Beta.
published: true
date: 2024-10-26T14:32:31.967Z
tags: outil, windows
editor: markdown
dateCreated: 2024-10-26T14:28:15.762Z
---

# Introduction

SharpChromium permet d'extraire des informations (cookie, historique, informations d'identification) depuis Google Chrome, Microsoft Edge et Microsoft Edge Beta.

> SharpChromium est disponible au téléchargement [ici](https://github.com/djhohnstein/SharpChromium)
> {.is-info}

> SharpChromium utilise le fichier %LOCALAPPDATA%\Google\Chrome\User Data\Default\Cookies pour les cookies. Si le fichier est à un autre endroit (ce qui varie en fonction des versions de Chrome). Une erreur apparaitra.
> {.is-warning}

# Syntaxe

`SharpChromium.exe <all;full;logins;history;cookies> [paramètres]`

# Paramètres

| Paramètre           | Description                                                                                                                                                                  |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `all`               | Récupère les cookies, l'historique et les informations d'identification.                                                                                                     |
| `full`              | Pareil que all                                                                                                                                                               |
| `logins`            | Récupère les informations d'identification avec des mots de passe non nul.                                                                                                   |
| `history`           | Récupère l'historique. Affiche les cookies qui correspondent aux entrées.                                                                                                    |
| `cookies [hôte(s)]` | Récupère tous les cookies et les sauvegarde dans "%TEMP%\$browser-cookies.json". Si des hôtes sont précisés, alors uniquement ceux-ci sont récupérés et uniquement affichés. |

# Exemples

Récupère les cookies, l'historique et les informations d'identification.
`SharpChromium.exe all`

Récupère les cookies de l'hôte mydomain.
`SharpChromium.exe cookies mydomain`
