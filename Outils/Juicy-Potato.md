---
title: Juicy Potato
description: Version améliorée de RottenPotatoNG, permet d'utiliser les privilèges SeImpersonate et/ou SeAssignPrimaryToken pour escalader les privilèges jusqu'au compte NT AUTHORITY\SYSTEM
published: true
date: 2024-07-12T17:08:36.726Z
tags: outil, windows, élévation des privilèges
editor: markdown
dateCreated: 2024-07-12T15:45:18.846Z
---

# Introduction

Juicy Potato est une version améliorée de RottenPotatoNG, Cet outil permet d'utiliser les privilèges SeImpersonate et/ou SeAssignPrimaryToken pour escalader les privilèges jusqu'au compte NT AUTHORITY\SYSTEM.

> Juicy Potato est disponible au téléchargement ici: https://github.com/ohpe/juicy-potato
> {.is-info}

> JuicyPotato ne fonctionne pas sur les versions après Windows Server 2019 et Windows 10 build 1809, du fait que DCOM ne rentre plus en communication avec le serveur COM MITM, de plus, le client ne négocie plus une authentification si les données ont étés transferés.
> {.is-danger}

# Syntaxe

`JuicyPotato.exe -t [t/u/*] -p [programme à éxecuter] -l [port d'écoute du serveur COM] [options]`

# Options

| Option       | Description                                                                                                            |
| ------------ | ---------------------------------------------------------------------------------------------------------------------- |
| `-t [t/u/*]` | Spécifie la fonction CreateProcessWithTokenW (SeImpersonate) ou CreateProcessAsUser (SeAssignPrimaryToken) ou les deux |
| `-p`         | Spécifie le programme à éxecuter                                                                                       |
| `-l`         | Spécifie le port d'écoute du serveur COM                                                                               |
| `-a`         | Argument à passer au programme                                                                                         |
| `-c`         | Précise le CLSID utilsé (par defaut, celui du Service de transfert intelligent en arrière-plan (BITS) est utilisé)     |

Pourquoi le CLSID du Service de transfert intelligent en arrière-plan (BITS) est utilisé par défaut? C'est simple, le CLSID de BITS est le même entre chaque machine.

# Exemples

Utilise la fonction CreateProcessWithTokenW (utilise le CLSID pour obtenir un token et créer un processus avec celui-ci), puis éxecute le programme "cmd.exe" avec comme consigne contenue dans l'argument d'éteindre la machine.

`JuicyPotato.exe -t t -p c:\windows\system32\cmd.exe -l 53375 -a "shutdown /s"`

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
