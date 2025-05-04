---
title: GCC
description: GCC (GNU Compiler Collection) est une suite de logiciels libres de compilation. On l'utilise dans le monde Linux dès que l'on veut transcrire du code source en langage machine, La suite gère les langages C, C++, Objective-C, Fortran, Ada, Go et D.
published: true
date: 2025-05-04T14:54:40.122Z
tags: outil, linux
editor: markdown
dateCreated: 2024-04-17T06:42:27.481Z
---

# Introduction

GCC (GNU Compiler Collection) est une suite de logiciels libres de compilation. On l'utilise dans le monde Linux dès que l'on veut transcrire du code source en langage machine, c'est le plus répandu des compilateurs. La suite gère les langages C, C++, Objective-C, Fortran, Ada, Go et D.

# Syntaxe

`gcc [fichier code source]`

# Options

| Raccourci                | Description                  |
| ------------------------ | ---------------------------- |
| `-o [fichier de sortie]` | précise le fichier de sortie |

> Si aucun fichier de sortie n'est précisé, celui-ci sera nommé a.out
> {.is-info}

# Exemples

Compilation d'un fichier code source C

`gcc [fichier code source C] -o [sortie binaire]`
