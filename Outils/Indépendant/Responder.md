---
title: Responder
description: Permet d'empoisonner certains protocoles (LLMNR;NBT-NS;MDNS) et permet la création de serveurs rogue (proxy WPAD, HTTP) pour la récupération d'identifiants
published: true
date: 2024-10-25T20:39:41.189Z
tags: outil, indépendant
editor: markdown
dateCreated: 2024-07-18T14:53:24.803Z
---

# Introduction

Permet d'empoisonner certains protocoles (LLMNR;NBT-NS;MDNS) et permet la création de serveurs rogue (proxy WPAD, HTTP) pour la récupération d'identifiants

> Responder est disponible au téléchargement ici: https://github.com/lgandx/Responder
> {.is-info}

# Syntaxe

`Responder.py -I [interface] [options]`

# Options

| Option               | Description                                                                                                                       |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `--version`          | Affiche la version de Responder                                                                                                   |
| `-h`                 | Affiche la page d'aide                                                                                                            |
| `-A`                 | Mode d'analyse, ne répond pas aux requètes                                                                                        |
| `-e [Addresse Ipv4]` | Utilise une addresse Ipv4 différente pour les réponses que cette de Responder                                                     |
| `-b`                 | Retourne les informations d'authentification basic HTTP à la place du hash NTLM                                                   |
| `-d`                 | Active le serveur DHCP et injecte un serveur WPAD dans les réponses                                                               |
| `-D`                 | Injecte un serveur DNS dans les réponses du serveur DHCP                                                                          |
| `-w`                 | Active le serveur rogue WPAD (qui envoi le fichier wpad.dat aux clients)                                                          |
| `-u [[hôte:port]`    | Spécifie un serveur proxy externe pour les requètes sortantes                                                                     |
| `-F`                 | Force une demande d'authentification lorsque le fichier wpad.dat est récupéré (cela peut afficher une fenêtre d'authentification) |
| `-P`                 | Force une demande d'authentification lors des connexions au proxy (cela peut afficher une fenêtre d'authentification)             |
| `-lm`                | Active la rétrogradation des hashs LM lors de la réception (valide pour NTLMv1)                                                   |
| `--disable-ess`      | Force la désactivation de la mesure de sécurité ESS (Extended Session Support)                                                    |
| `-v`                 | Active le mode verbose                                                                                                            |

# Exemples

Active Responder sur l'interface eth0 avec le serveur rogue WPAD activé et force la demande d'authentification.

`Responder.py -I eth0 -w -F`
