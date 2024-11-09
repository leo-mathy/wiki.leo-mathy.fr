---
title: ffuf
description: Puissant outil de fuzzing web. Permet la découverte de répertoires, et l'utilisation de diverses requêtes.
published: true
date: 2024-11-09T18:29:59.210Z
tags: outil, indépendant, synthèse
editor: markdown
dateCreated: 2024-11-09T18:29:59.210Z
---

# Introduction

ffuf (Fuzz Faster U Fool) est un puissant outil de fuzzing web. Il permet d'effectuer des découvertes de répertoires ainsi que l'utilisation de diverses requêtes.

> Le terme "fuzzing" désigne le fait de tester une interface avec des données diverses (parfois aléatoires) et de vérifier si un changement (neutre,positif ou négatif) s'est produit.
{.is-info}

> ffuf est disponible au téléchargement [ici](https://github.com/ffuf/ffuf)
{.is-info}

# Syntaxe

`ffuf [-w <fichier wordlist>] [-u [cible<FUZZ>]] [paramètres]`

# Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |
| `...`     | ...         |

# Exemples

Effectue une simple découverte de répertoire.
`ffuf -w ./wordlist.txt -u https://www.example.com/FUZZ`

# Voir aussi

Documentation officielle
https://github.com/ffuf/ffuf/wiki

Guide détaillé sur ffuf
https://codingo.io/tools/ffuf/bounty/2020/09/17/everything-you-need-to-know-about-ffuf.html