---
title: Write-UserAddMSI
description: Outil de la suite PowerSploit. Écris un fichier d'installateur au format msi qui crée un nouvel utilisateur. Cela peut servir pour exploiter la faille "AlwaysInstallElevated".
published: true
date: 2024-09-29T15:47:22.909Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-09-29T15:47:22.909Z
---

# Introduction

Script PowerShell de la suite PowerSploit. Écris un fichier d'installateur au format msi qui crée un nouvel utilisateur. Cela peut servir pour exploiter la faille "AlwaysInstallElevated".

> Le script PowerShell Write-UserAddMSI est disponible au téléchargement [ici](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1)
> {.is-info}

> Par défaut, le fichier msi est créé dans le répertoire actuel.
> {.is-info}

# Syntaxe

`Write-UserAddMSI [emplacement de sortie]`

# Exemples

Écris un fichier d'installateur au format msi qui crée un nouvel utilisateur dans le répertoire actuel.
`Write-UserAddMSI`

# Voir aussi

paramètre "AlwaysInstallElevated"
https://learn.microsoft.com/en-us/windows/win32/msi/alwaysinstallelevated
