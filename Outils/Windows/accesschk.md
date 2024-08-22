---
title: AccessChk
description: Afficher les droits des groupes ou des utilisateurs sur des fichiers, répertoires, clés de registre, objets globaux et services ainsi que les privilèges des groupes ou des utilisateurs.
published: true
date: 2024-08-22T16:11:47.955Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-31T17:24:12.539Z
---

# Introduction

AccessChk est un outil de la suite Sysinternals de Microsoft. Cet outil permet d'afficher les droits des groupes ou des utilisateurs sur des fichiers, répertoires, clés de registre, objets globaux et services ainsi que les privilèges des groupes ou des utilisateurs.

> AccessChk est disponible au téléchargement [ici](https://learn.microsoft.com/fr-fr/sysinternals/downloads/accesschk)
> {.is-info}

# Syntaxe

`accesschk [paramètres] <fichier, répertoire, clé de registre, processus/PID, service, objet>`

# Paramètres

| Paramètre                               | Description                                                                                                                                                                                           |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-a <privilège                          | \*>`                                                                                                                                                                                                  | Affiche les utilisateurs et groupes disposant d'un privilège spécifique sur l'élément indiqué. Il est possible d'utiliser une wildcard pour afficher tous les privilèges d'un utilisateur ou groupe. |
| `-c <service                            | \*>`                                                                                                                                                                                                  | Affiche les droits assignés au service indiqué. Il est possible d'utiliser une wildcard pour afficher tous les services.                                                                             |
| `-d`                                    | Traiter uniquement les répertoires ou les clés de niveau supérieur                                                                                                                                    |
| `-e`                                    | Afficher uniquement les niveaux d'intégrité explicitement définis (faible, moyen, élevé et système).                                                                                                  |
| `-f`                                    | Si vous suivez `-p`, affiche les informations complètes sur le jeton de processus.                                                                                                                    |
| `-p`                                    | L'élément est un processus.                                                                                                                                                                           |
| `-h <partage de fichier ou d'imprimante | \*>`                                                                                                                                                                                                  | Affiche les droits assignés au partage de fichier ou d'imprimante indiqué. Il est possible d'utiliser une wildcard pour afficher tous les partage de fichier ou d'imprimante.                        |
| `-i`                                    | Ignorer les objets avec uniquement des ACE héritées (afficher les objets avec des ACE explicites).                                                                                                    |
| `-k`                                    | L'élément est une clé de registre.                                                                                                                                                                    |
| `-l`                                    | Afficher le descripteur de sécurité complet (C'est le Security Descriptor, qui contient les DACL,SACL,Propriétaire,Groupe).                                                                           |
| `-n`                                    | Afficher uniquement les objets ou il n'y a pas d'accès.                                                                                                                                               |
| `-o`                                    | L'élément est un objet dans le gestionnaire d'objet. Pour voir le contenu du répertoire, il est possible d'utiliser un antislash ou de préciser l'option -s pour effectuer l'opération récursivement. |
| `-nobanner`                             | N'affiche pas la bannière de démarrage ou le message de copyright.                                                                                                                                    |
| `-r`                                    | Affiche uniquement les objets avec un accès en lecture.                                                                                                                                               |
| `-w`                                    | Affiche uniquement les objets avec un accès en écriture.                                                                                                                                              |
| `-t <filtre>`                           | Filtre les objets par le type précisé.                                                                                                                                                                |
| `-u`                                    | N'affiche pas les erreurs.                                                                                                                                                                            |
| `-v`                                    | Active le mode verbose.                                                                                                                                                                               |
| `/accepteula`                           | Paramètre global pour accepter les conditions d'utilisation.                                                                                                                                          |

# Exemples

Affiche les permissions sur le processus avec comme PID 6624.

`accesschk.exe -p 6624`

Affiche les droits d'écriture uniquement sur la clé de registre "services", en mode verbose et sans afficher les erreurs.

`accesschk.exe -kvuw hklm\System\CurrentControlSet\services`

Affiche tous les services où le groupe "users" a un accès en écriture.

`accesschk.exe users -cw *`

Affiche les permissions du répertoire "Test".

`accesschk.exe -d "C:\Windows`

# Voir aussi

[Explications sur le Contrôle d’intégrité obligatoire (en lien avec le paramètre -e)](https://learn.microsoft.com/fr-fr/windows/win32/secauthz/mandatory-integrity-control)
