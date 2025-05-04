---
title: kwprocessor
description: Générateur de "keyboard-walk". C'est a dire de chaines de caractères qui sont tapés sur un clavier suivant un modèle.
published: true
date: 2025-05-04T14:54:44.583Z
tags: outil, linux, synthèse
editor: markdown
dateCreated: 2024-11-19T18:34:40.652Z
---

# Introduction

kwprocessor est un outil avancé de génération de "keyboard-walk". C'est a dire de chaines de caractères qui sont tapés sur un clavier suivant un modèle.

> kwprocessor est disponible au téléchargement [ici](https://github.com/hashcat/kwprocessor)
> {.is-info}

# Syntaxe

`kwp [paramètres] <fichier de codage de caractères> <fichier d'organisation des touches du clavier> <fichier route>`

> Par défaut, kwprocessor possède des fichiers route dans la source.
> {.is-info}

> Les fichiers routes correspondent aux déplacements effectués sur le clavier.
> {.is-info}

# Paramètres

| Paramètre                              | Description                                                                             |
| -------------------------------------- | --------------------------------------------------------------------------------------- |
| `-h`                                   | Affiche l'aide.                                                                         |
| `-o <fichier> --output-file <fichier>` | Spécifie le fichier de sortie.                                                          |
| `-s`                                   | Utilise les caractères qui peuvent être atteints en ayant un doigt sur la touche Shift. |
