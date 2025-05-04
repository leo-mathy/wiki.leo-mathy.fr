---
title: mRemoteNG-Decrypt
description: Déchiffre les mots de passes stockés par mRemoteNG.
published: true
date: 2025-05-04T14:54:08.250Z
tags: outil, indépendant
editor: markdown
dateCreated: 2024-10-26T13:49:46.299Z
---

# Introduction

mRemoteNG est un outil utilisé pour gérer les connexions et se connecter aux systèmes en utilisant divers protocoles.

Par défaut, mRemoteNG stocke les informations de connexions dans le fichier AppData\Roaming\mRemoteNG\confCons.xml.
Les mots de passes (champ Password) contenus dans ce fichier sont chiffrés avec un mot de passe maître (champ Protected).
Cependant, si le mot de passe maître n'est pas défini par l'utilisateur, celui-ci est "mR3m".

mRemoteNG-Decrypt permet de déchiffrer mots de passes stockés dans le fichier confCons.xml.

> mRemoteNG-Decrypt est disponible au téléchargement [ici](https://github.com/haseebT/mRemoteNG-Decrypt)
> {.is-info}

# Syntaxe

`mremoteng_decrypt.py -s <champ Password> [-p <mot de passe personnalisé>]`

# Paramètres

| Paramètre             | Description                                                                                                                        |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `-p <mot de passe>`   | Précise le mot de passe utilisé pour déchiffrer le champ Password. Si il n'est pas précisé, "mR3m" est utilisé comme mot de passe. |
| `-s <champ Password>` | Précise la valeur du champ Password.                                                                                               |
