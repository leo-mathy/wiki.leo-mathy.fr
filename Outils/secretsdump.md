---
title: secretsdump
description: Lis les informations concernant les comptes depuis la base ntds.dit
published: true
date: 2024-07-15T12:49:07.492Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-15T12:49:07.492Z
---

# Introduction

secretsdump est un script python de la suite Impacket, ce script permet de récupérer les informations concernant les comptes depuis la base ntds.dit

> La suite Impacket est disponible au téléchargement ici: https://github.com/fortra/impacket
> {.is-info}

# Syntaxe

`Get-ADDBAccount -DatabasePath [fichier ntds.dit] [options]`

# Options

| Option                                    | Description                                                                                                |
| ----------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `-bootkey [clé de démarrage]`             | Spécifie la clé de démarrage (ou clé système) pour déchiffrer les valeurs des attribus secrets             |
| `-system [fichier .hiv]`        | Spécifie le chemin vers le fichier ruche de registre SYSTEM (sauvegardé depuis la clé HKLM\SYSTEM)                                      |
| `-security [fichier .hiv]`        | Spécifie le chemin vers le fichier ruche de registre SECURITY (sauvegardé depuis la clé HKLM\SECURITY)                                      |
| `-sam [fichier .hiv]`        | Spécifie le chemin vers le fichier ruche de registre SAM (sauvegardé depuis la clé HKLM\SAM)                                      |
| `-ntds [fichier ntds.dit]`        | Spécifie le chemin vers le fichier de la base de donnée d'un domaine                                    |
| `-outputfile [fichier de sortie]`        | Enregistre la sortie dans un fichier                                      |
| `-just-dc-user [Nom SAM]`        | Spécifie quel compte récupérer en fonction du nom SAM (Security Account Manager) depuis la base de données                                     |
| `-ldapfilter [Nom distinct]`        | Spécifie quel compte récupérer en fonction du DN (nom distinct) depuis la base de données                                      |
| `-just-dc`        | Extrait uniquement les hashs NTML et clés kerberos |






| `-DistinguishedName [Nom distinct]`       | Spécifie quel compte récupérer en fonction du DN (nom distinct) depuis la base de données                  |
| `-ObjectGuid [Identifiant unique global]` | Spécifie quel compte récupérer en fonction du GUID (Identifiant unique global) depuis la base de données   |
| `-ObjectSid [Identifiant de sécurité]`    | Spécifie quel compte récupérer en fonction du SID (Identifiant de sécurité) depuis la base de données      |
| `-SamAccountName [Nom SAM]`               | Spécifie quel compte récupérer en fonction du nom SAM (Security Account Manager) depuis la base de données |
| `-DistinguishedName [Nom distinct]`       | Spécifie quel compte récupérer depuis la base de données                                                   |

> Il est possible d'utiliser l'applet Get-BootKey inclus dans la module DSInternals pour récupérer la clé de démarrage (ou clé système)
> {.is-info}

# Exemples

Récupère tous les comptes

`Get-ADDBAccount -DatabasePath ./ntds.dit -All`

Récupère le compte où le nom SAM est Administrateur

`Get-ADDBAccount -DatabasePath ./ntds.dit -SamAccountName Administrateur`

Récupère tous les comptes et déchiffre les valeurs des attribus secrets avec la clé de démarrage

`Get-ADDBAccount -DatabasePath ./ntds.dit -All -BootKey acdba64a3929261b04e5270c3ef973cf
