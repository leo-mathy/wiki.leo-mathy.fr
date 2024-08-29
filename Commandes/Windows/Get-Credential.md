---
title: Get-Credential
description: l'applet Get-Credential permet de créer un objet d'informations d'identification (objet PSCredential) avec les informations entrées (nom d'utilisateur et mot de passe)
published: true
date: 2024-08-29T15:51:07.991Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-08-29T15:33:45.175Z
---

# Introduction

l'applet Get-Credential permet de créer un objet d'informations d'identification (objet PSCredential) avec les informations entrées (nom d'utilisateur et mot de passe)

# Syntaxe

Get-Credential [paramètres]

# Paramètres

| Paramètre                          | Description                                |
| ---------------------------------- | ------------------------------------------ |
| `-Credential <objet PSCredential>` | Précise un objet PSCredential comme entrée |
| `-Message <message>`               | Précise le message affiché                 |
| `-Title <titre>`                   | Précise le titre affiché                   |
| `-UserName <nom d'utilisateur>`    | Précise le nom d'utilisateur               |

# Exemples

Demande le mot de passe pour l'utilisateur Paul avec un message et un titre personnalisé
`Get-Credential -Message "Requête d'identifiants" -Title Identification -Username Paul`

# Voir aussi

Documentation officielle de l'applet
https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-credential

Détails sur l'objet PSCredential
https://learn.microsoft.com/en-us/dotnet/api/system.management.automation.pscredential
