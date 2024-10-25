---
title: SeBackupPrivilege
description: Module powershell permettant d'activer le privilège SeBackupPrivilege (désactivé par défaut sur les comptes ayant le privilège d'assigné)
published: true
date: 2024-10-25T20:47:10.796Z
tags: outil, windows, powershell
editor: markdown
dateCreated: 2024-07-15T10:52:35.143Z
---

# Introduction

SeBackupPrivilege est un module powershell permettant d'activer le privilège SeBackupPrivilege (désactivé par défaut sur les comptes ayant le privilège d'assigné). Ce qui permet de passer à travers les permissions sur les objets (registre,fichiers,dossiers).

> SeBackupPrivilege est disponible au téléchargement ici: https://github.com/giuliano108/SeBackupPrivilege
> {.is-info}

# Syntaxe

Importer les modules:

`Import-Module .\SeBackupPrivilegeUtils.dll`
`Import-Module .\SeBackupPrivilegeCmdLets.dll`

# Commandes

Après avoir importer les deux modules, il est possible d'utiliser les commandes intégrées au module.

| Commande                                                                 | Description                                                                                                                         |
| ------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| `Get-SeBackupPrivilege`                                                  | Permet de voir si le droit est désactivé ou non                                                                                     |
| `Set-SeBackupPrivilege`                                                  | Active le privilège SeBackupPrivilege pour le processus du terminal                                                                 |
| `Copy-FileSeBackupPrivilege [fichier à copier] [fichier de destination]` | Copie un fichier vers un autre emplacement en utilisant la fonction CreateFileA en spécifiant le drapeau Copy-FileSeBackupPrivilege |

> Avec le privilège d'activé, il est possible de lister tous les repertoires (avec dir / Get-ChildItem), mais pour avoir accès au données des fichiers, la commande Get-Content ou copy ne fonctionnent pas, en effet il faut utiliser la fonction CreateFileA de Microsoft et préciser le drapeau FILE_FLAG_BACKUP_SEMANTICS pour indiquer que l'opération est une opération de sauvegarde. C'est pour cela que la command Copy-FileSeBackupPrivilege est disponible dans le module.
> {.is-info}

> Si le fichier ou dossier à une permission de refus explicite pour l'utilisateur, utiliser le privilège ne fonctionnera pas.
> {.is-danger}

# Exemples

Copie le fichier c:\confidentiel\login.txt vers ./login.txt en utilisant le privilège SeBackupPrivilege:

`Copy-FileSeBackupPrivilege c:\confidentiel\login.txt ./login.txt`
