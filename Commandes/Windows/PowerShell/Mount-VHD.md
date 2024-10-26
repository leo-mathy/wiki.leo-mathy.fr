---
title: Mount-VHD
description: Monte un ou plusieurs disques virtuels au format vhd/vhdx.
published: true
date: 2024-10-26T18:49:46.010Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-10-26T18:49:46.010Z
---

# Introduction

l'applet PowerShell Mount-VHD permet de monter un ou plusieurs disques virtuels au format vhd/vhdx.

# Syntaxe

`Mount-VHD -Path <chemin du fichier vhd/vhdx> [paramètres]`

# Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `-CimSession <ordinateur/session>`     | Exécute la commande sur une session distante.         |
| `-ComputerName <machine>`     | Monte le disque sur un ordinateur exécutant les services hyper-v.         |
| `-Confirm`     | Demande confirmation avant l'exécution de la commande.         |
| `-Credential <utilisateur/Objet PScredential>`     | Exécute la commande en tant qu'un autre utilisateur.         |
| `-NoDriveLetter`     | N'assigne pas de lettre de lecteur au volume.|
| `-Passthru`     | Passe l'objet powershell représentant le disque virtuel à monter.
| `-Path <chemin du fichier vhd/vhdx>`    | Précise le chemin du fichier vhd/vhdx.
| `-ReadOnly`     | Monte le disque
| `-CimSession <ordinateur/session>`     | Exécute la commande sur une session distante.         |

# Exemples

# Voir aussi
