---
title: smbserver
description: Script Python permettant la création rapide d'un serveur SMB de partage de fichiers.
published: true
date: 2025-05-04T14:54:20.503Z
tags: outil, indépendant
editor: markdown
dateCreated: 2024-09-29T15:36:32.995Z
---

# Introduction

smbserver est un script Python de la suite Impacket, permettant la création rapide d'un serveur SMB de partage de fichiers.

> Le script smbserver est disponible au téléchargement [ici](https://github.com/fortra/impacket/blob/master/impacket/smbserver.py)
> {.is-info}

# Syntaxe

`smbserver.py [paramètres] <Nom du partage> <Emplacement du partage>`

# Paramètres

| Paramètre                                 | Description                                                                                  |
| ----------------------------------------- | -------------------------------------------------------------------------------------------- |
| `-h, --help`                              | Affiche la page d'aide.                                                                      |
| `-comment <commentaire>`                  | Indique le commentaire associé au partage.                                                   |
| `-username <nom d'utilisateur>`           | Spécifie le nom de l'utilisateur pour l'authentification (accès à tout le monde par défaut). |
| `-password <mot de passe>`                | Spécifie le mot de passe associé à l'utilisateur (paramètre username).                       |
| `-hashes <hashs au format LMHASH:NTHASH)` | Spécifie le hash pour l'authentification.                                                    |
| `-ts`                                     | Ajoute un horodatage pour chaque sortie dans le terminal.                                    |
| `-debug`                                  | Active le mode debug                                                                         |
| `-IP <interface d'écoute>`                | Spécifie l'interface d'écoute. (0.0.0.0 par défaut)                                          |
| `-port <port>`                            | Spécifie le port utilisé. (445 par défaut pour le protocole SMB)                             |
| `-smb2support`                            | Active le support pour le SMBv2. (expérimental)                                              |

# Exemples

Créer un serveur SMB avec un partage nommé TMP situé dans le dossier du serveur /tmp
`smbserver.py TMP /tmp`

# Voir aussi

Suite Impacket
https://github.com/fortra/impacket
