---
title: AccessChk
description: Afficher les droits des groupes ou des utilisateurs sur des fichiers, répertoires, clés de registre, objets globaux et services ainsi que les privilèges des groupes ou des utilisateurs.
published: true
date: 2024-08-22T13:02:39.497Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-31T17:24:12.539Z
---

# Introduction

AccessChk est un outil de la suite Sysinternals de Microsoft. Cet outil permet d'afficher les droits des groupes ou des utilisateurs sur des fichiers, répertoires, clés de registre, objets globaux et services ainsi que les privilèges des groupes ou des utilisateurs.

> AccessChk est disponible au téléchargement [ici](https://learn.microsoft.com/fr-fr/sysinternals/downloads/accesschk)
> {.is-info}

# Syntaxe

`accesschk [paramètres] <fichier, répertoire, clé de registre, processus, service, objet>`

# Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `-a <privilège|*>`     | Affiche les utilisateurs et groupes disposant d'un privilège spécifique sur l'élement indiqué. Il est possible d'utiliser une wildcard pour afficher tous les privilèges d'un utilisateur ou groupe.         |
| `-c <service|*>`     | Affiche les droits assignés au service indiqué. Il est possible d'utiliser une wildcard pour afficher tous les services.         |
| `-d`     | Traiter uniquement les répertoires ou les clés de niveau supérieur |
| `-e`     | Afficher uniquement les niveaux d'intégrité explicitement définis (faible, moyen, élevé et système).         |
| `-f`     | Si vous suivez `-p`, affiche les informations complètes sur le jeton de processus.         |
| ` -p <nom du processus|PID>`     | Affiche les droits assignés du processus.        |
| `-h <partage de fichier ou d'imprimante|*>`     | Affiche les droits assignés au partage de fichier ou d'imprimante indiqué. Il est possible d'utiliser une wildcard pour afficher tous les partage de fichier ou d'imprimante.         |
| `-i`     | 	Ignorer les objets avec uniquement des ACE héritées (afficher les objets avec des ACE explicites).         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |

# Exemples

# Voir aussi

Explications sur le Contrôle d’intégrité obligatoire (lien avec -e):
https://learn.microsoft.com/fr-fr/windows/win32/secauthz/mandatory-integrity-control

