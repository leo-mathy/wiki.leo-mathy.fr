---
title: PrintSpoofer
description: Permet de créer un processus SYSTEM dans la console, utilise le privilège SeImpersonate pour escalader les privilèges jusqu'au compte NT AUTHORITY\SYSTEM
published: true
date: 2024-10-25T20:45:04.497Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-13T10:26:57.386Z
---

# Introduction

PrintSpoofer permet de créer un processus SYSTEM dans la console à l'aide des Canaux Nommés, utilise le privilège SeImpersonate pour escalader les privilèges jusqu'au compte NT AUTHORITY\SYSTEM.

> PrintSpoofer est disponible au téléchargement ici: https://github.com/itm4n/PrintSpoofer
> {.is-info}

> PrintSpoofer est une alternative à Juicy Potato, qui ne fonctionne pas sur les versions après Windows Server 2019 et Windows 10 build 1809.
> {.is-info}

# Syntaxe

`PrintSpoofer.exe [options]`

# Options

| Option          | Description                                                       |
| --------------- | ----------------------------------------------------------------- |
| `-c [commande]` | Spécifie la commande à exécuter                                   |
| `-i`            | Interagir avec le processus créer dans la ligne de commande       |
| `-d [ID]`       | Créer le processus dans le bureau correspondant à l'ID de session |

# Exemples

Lance une console cmd sur le bureau correspondant à la session 1

`PrintSpoofer.exe -d 1 -c cmd.exe`

Lancer PowerShell dans la console actuelle en tant que SYSTEM

`PrintSpoofer.exe -i -c powershell.exe`

# Voir aussi

Fonctionnement de l'exploit expliqué:
https://itm4n.github.io/printspoofer-abusing-impersonate-privileges/

Pourquoi JuicyPotato ne fonctionne pas sur les versions après Windows Server 2019 et Windows 10 build 1809:
https://decoder.cloud/2018/10/29/no-more-rotten-juicy-potato/

Présentation et fonctionnement basique des potatoes:
https://jlajara.gitlab.io/Potatoes_Windows_Privesc#juicyPotato
