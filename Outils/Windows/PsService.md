---
title: PsService
description: Communique avec le Controlleur de Services et les services installés, permet d'interagir avec les services
published: true
date: 2024-07-23T13:34:23.492Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-23T13:34:23.492Z
---

# Introduction

PsService est un outil de la suite Sysinternals de Microsoft permettant de communiquer avec le Controlleur de Services et les services installés, permet d'interagir avec les services. Cet outil permet aussi d'afficher le Descripteur de sécurité d'un service sans passer par le language SDD (contrairement à sc qui utilise ce language peu lisible rapidement pour un humain)

> PsService est disponible au téléchargement ici: https://learn.microsoft.com/fr-fr/sysinternals/downloads/psservice
> {.is-info}

# Syntaxe

`PsService.exe [commande] [options]`

# Commande

| Option                       | Description                                                                  |
| ---------------------------- | ---------------------------------------------------------------------------- |
| `query [nom du service]`     | Affiche l’état d’un service.                                                 |
| `config [nom du service]`    | Affiche la configuration d’un service.                                       |
| `setconfig [nom du service]` | Définit le type de démarrage (désactivé, automatique, demande) d’un service. |
| `config [nom du service]`    | Affiche la configuration d’un service.                                       |
| `start [nom du service]`     | Démarre un service.                                                          |
| `stop [nom du service]`      | Arrête un service.                                                           |
| `config [nom du service]`    | Affiche la configuration d’un service.                                       |
| `restart [nom du service]`   | Arrête, puis redémarre un service.                                           |
| `pause [nom du service]`     | Interrompt un service                                                        |
| `cont	[nom du service]`      | Reprend un service suspendu.                                                 |
| `depend [nom du service]`    | Répertorie les services qui dépendent de celui spécifié.                     |
| `security [nom du service]`  | Affiche le Descripteur de sécurité d'un service.                             |
| `find [nom du service]`      | Recherche le service spécifié.                                               |
| `\\[ordinateur]`             | Précise l'ordinateur                                                         |
| `-u [nom d'utilisateur]`     | Précise le nom d'utilisateur                                                 |
| `-p [mot de passe]`          | Précise le mot de passe associé à l'utilisateur                              |

# Exemples

Affiche le Descripteur de sécurité du service EventLog

`PsService.exe security EventLog`
