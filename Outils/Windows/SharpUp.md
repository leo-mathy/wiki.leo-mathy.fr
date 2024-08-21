---
title: SharpUp
description: Portage des fonctionnalités de PowerUp en C#. Permet d'effectuer des vérifications basiques comme les permissions sur les exécutables de services.
published: true
date: 2024-08-21T17:00:30.061Z
tags: outil, windows
editor: markdown
dateCreated: 2024-08-21T16:58:16.910Z
---

# Introduction

SharpUp est un outil utilisant le langage C#, basé sur les fonctionnalités de PowerUp (outil de la suite PowerSploit). SharpUp permet d'effectuer des vérifications basiques pour vérifier la présence de vulnérabilités.

> SharpUp est disponible au téléchargement ici: https://github.com/GhostPack/SharpUp/
> {.is-info}

# Syntaxe

`SharpUp.exe [audit] [Vérification 1] [Autres vérifications]`

# Paramètres

| Paramètre        | Description                                                                                                                                                                                                                                    |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `audit`          | Active le mode audit, ce qui lance les vérifications sans se préoccuper de si le processus est exécuté en mode privilégié ou si l'utilisateur actuel a des droits. Si aucune vérification n'est précisé à la suite, elles sont toutes lancées. |
| `[Vérification]` | Précise quelle vérification lancer. Plusieurs peuvent être indiqués à la suite.                                                                                                                                                                |

# Vérifications possibles

Les vérifications de vulnérabilités disponibles sont celles-ci:

- AlwaysInstallElevated
- CachedGPPPassword
- DomainGPPPassword
- HijackablePaths
- McAfeeSitelistFiles
- ModifiableScheduledTask
- ModifiableServiceBinaries
- ModifiableServiceRegistryKeys
- ModifiableServices
- ProcessDLLHijack
- RegistryAutoLogons
- RegistryAutoruns
- TokenPrivileges
- UnattendedInstallFiles
- UnquotedServicePath

# Exemples

Vérifie toutes les vulnérabilités peu importe les droits du processus ou des privilèges de l'utilisateur

`SharpUp.exe audit`

Vérifie la vulnérabilitée nommée "HijackablePaths" (Vérifie si des chemins dans la variable %PATH% sont modifiables).

`SharpUp.exe HijackablePaths`

Vérifie la vulnérabilitée nommée "HijackablePaths" (Vérifie si des chemins dans la variable %PATH% sont modifiables) peu importe les droits du processus ou des privilèges de l'utilisateur.

`SharpUp.exe audit HijackablePaths`

# Voir aussi

PowerUp (outil de la suite PowerSploit):
https://github.com/PowerShellMafia/PowerSploit/blob/dev/Privesc/PowerUp.ps1
https://github.com/PowerShellMafia/PowerSploit/blob/dev/Privesc/README.md
