---
title: SessionGopher
description: Recherche raisonnablement discrètement des informations de session d'outils d'accès à distance, sauvegardées dans la ruche de registre HKEY_USERS ou dans des fichiers.
published: true
date: 2024-09-26T17:43:50.243Z
tags: outil, windows
editor: markdown
dateCreated: 2024-09-26T17:37:08.015Z
---

# Introduction

SessionGopher est un script PowerShell qui permet de rechercher raisonnablement discrètement des informations de session d'outils d'accès à distance (qui comportent des mots de passe), sauvegardées dans la ruche de registre HKEY_USERS ou dans des fichiers.

> SessionGopher est disponible au téléchargement [ici](https://github.com/Arvanaghi/SessionGopher)
{.is-info}

> Des droits administrateurs sont nécessaires pour l'accès aux autres clés des utilisateurs contenues dans HKEY_USERS. Sans ces droits uniquement l'utilisateur actuel sera ciblé.
{.is-warning}

# Syntaxe

`Invoke-SessionGopher [paramètres]`

# Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `-Thorough`     | Recherche sur tous les disques des fichiers d'informations de session. (.ppk, .rdp et .sdtid)         |
| `-o` | Enregistre les informations trouvées dans des fichiers CSV.  |
| `-iL <fichier>` | Indique un fichier contenant la liste des hôtes sur lesquels effectuer l'opération (un hôte par ligne). |
| `-AllDomain` | Interroge le contrôleur de domaine pour obtenir une liste des ordinateurs du domaine et lance l'opération sur tous ceux retournés. |
| `-Target:<cible. |
| `-o` | ... |
| `-o` | ... |
| `-o` | ... |
| `-o` | ... |
| `-o` | ... |
| `-o` | ... |

# Exemples

# Voir aussi
