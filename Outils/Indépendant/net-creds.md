---
title: net-creds
description: Script Python qui récupère les mots de passes et hashes depuis une interface ou un fichier de capture de paquets (pcap). Assembles les paquets et ne se base pas sur les ports pour l'identification du service.
published: true
date: 2025-05-04T14:54:12.777Z
tags: outil, indépendant
editor: markdown
dateCreated: 2024-10-06T10:02:02.316Z
---

# Introduction

net-creds est un script python qui récupère les mots de passes et hashes depuis une interface ou un fichier d'analyse de paquets (pcap). Assembles les paquets et ne se base pas sur les ports pour l'identification du service.

> net-creds est disponible au téléchargement [ici](https://github.com/DanMcInerney/net-creds/)
> {.is-info}

# Syntaxe

`net-creds.py <[-p <fichier pcap]|[-i <interface>]> [paramètres]`

# Paramètres

| Paramètre                                   | Description                                            |
| ------------------------------------------- | ------------------------------------------------------ |
| `-i <interface>, -inferface <interface>`    | Indique l'interface à utiliser.                        |
| `-p <fichier pcap>, -pcap <fichier pcap>`   | Indique le fichier d'analyse de paquets au format pcap |
| `-f <addresse IP>, --filterip <adresse IP>` | Ne pas récupérer les paquets pour une adresse IP.      |
| `-v, --verbose`                             | Active le mode verbose.                                |

# Exemples

Renifler les mots de passes et hashes depuis l'interface wlan0
`net-creds.py -i wlan0`

# Voir aussi

Site officiel de TCPdump et LibPcap:
https://www.tcpdump.org/
