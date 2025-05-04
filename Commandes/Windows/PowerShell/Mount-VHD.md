---
title: Mount-VHD
description: Monte un ou plusieurs disques virtuels au format vhd/vhdx.
published: true
date: 2025-05-04T14:56:39.396Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-10-26T18:49:46.010Z
---

# Introduction

l'applet PowerShell Mount-VHD permet de monter un ou plusieurs disques virtuels au format vhd/vhdx.

# Syntaxe

`Mount-VHD -Path <chemin du fichier vhd/vhdx> [paramètres]`

# Paramètres

| Paramètre                                      | Description                                                       |
| ---------------------------------------------- | ----------------------------------------------------------------- |
| `-CimSession <ordinateur/session>`             | Exécute la commande sur une session distante.                     |
| `-ComputerName <machine>`                      | Monte le disque sur un ordinateur exécutant les services hyper-v. |
| `-Confirm`                                     | Demande confirmation avant l'exécution de la commande.            |
| `-Credential <utilisateur/Objet PScredential>` | Exécute la commande en tant qu'un autre utilisateur.              |
| `-NoDriveLetter`                               | N'assigne pas de lettre de lecteur au volume.                     |
| `-Passthru`                                    | Passe l'objet PowerShell représentant le disque virtuel à monter. |
| `-Path <chemin du fichier vhd/vhdx>`           | Précise le chemin du fichier vhd/vhdx.                            |
| `-ReadOnly`                                    | Monte le disque virtuel en mode lecture seule.                    |
| `-SnapshotId <GUID>`                           | Précise l'ID unique d'un set VHD.                                 |
| `-WhatIf`                                      | N'exécute pas la commande mais indique les résultats attendus.    |

# Exemples

Monte le disque dur virtuel SRV-TEST.vhdx en mode lecture seule.
`Mount-VHD -Path ./SRV-TEST.vhdx -ReadOnly`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/en-us/powershell/module/hyper-v/mount-vhd
