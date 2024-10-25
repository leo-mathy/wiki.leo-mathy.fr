---
title: wevtutil
description: Permet de voir, archiver, vider les journaux des événements Windows
published: true
date: 2024-10-25T20:27:43.206Z
tags: windows, commande
editor: markdown
dateCreated: 2024-07-15T16:30:54.309Z
---

# Introduction

Wevtutil permet de voir, archiver, vider les journaux des événements Windows.

# Syntaxe

`wevtutil [commande] [option]`

# Commandes

| Commande            | Description                                                                                                                                                                                                      |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `el`                | Affiche les noms de tous les journaux.                                                                                                                                                                           |
| `gl [log]`          | Affiche les informations de configuration du journal spécifié, qui indiquent si le journal est activé ou non, la limite de taille maximale actuelle du journal et le chemin du fichier où le journal est stocké. |
| `qe [log/fichier]`  | Lit les événements à partir d’un journal des événements ou d’un fichier journal                                                                                                                                  |
| `gli [log]`         | Affiche des informations d’état sur un journal d’événements ou un fichier journal.                                                                                                                               |
| `epl [log/fichier]` | Exporte des événements à partir d’un journal d’événements ou d’un fichier journal                                                                                                                                |
| `cl`                | Efface les événements du journal des événements spécifié.                                                                                                                                                        |

# Options

| Option              | Description                                                                                                                            |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `/f:[xml/text]`     | Spécifie que la sortie doit être au format XML ou texte                                                                                |
| `/e:[true/false]`   | Active ou désactive un journal                                                                                                         |
| `/rd:[true/false]`  | Spécifie le sens dans lequel les événements sont lus. Si la valeur est true, les événements les plus récents sont retournés en premier |
| `/c:[nombre]`       | Définit le nombre maximal d’événements à lire.                                                                                         |
|  |
| `/r:[ordinateur]`   | exécute la commande sur un ordinateur distant.                                                                                         |
| `/u:[Utilisateur]`  | Spécifie un autre utilisateur pour se connecter à un ordinateur distant.                                                               |
| `/p:[mot de passe]` | Spécifie le mot de passe de l’utilisateur.                                                                                             |

# Exemples

Lister les noms de tous les journaux:

`wevtutil el`

Voir les 5 derniers évenements du journal SECURITY au format texte:

`wevtutil qe SECURITY /c:5 /rd:true /f:text`

Afficher l’état du journal des applications:

`wevtutil gli Application`

Exporter des événements du journal système vers C:\temp\system-log.evtx :

`wevtutil epl System C:\temp\system-log.evtx
`
