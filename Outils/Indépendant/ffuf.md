---
title: ffuf
description: Puissant outil de fuzzing web. Permet la découverte de répertoires, et l'utilisation de diverses requêtes.
published: true
date: 2024-11-09T18:59:40.636Z
tags: outil, indépendant, synthèse
editor: markdown
dateCreated: 2024-11-09T18:29:59.210Z
---

# Introduction

ffuf (Fuzz Faster U Fool) est un puissant outil de fuzzing web. Il permet d'effectuer des découvertes de répertoires ainsi que l'utilisation de diverses requêtes.

> Le terme "fuzzing" désigne le fait de tester une interface avec des données diverses (parfois aléatoires) et de vérifier si un changement (neutre, positif ou négatif) s'est produit.
> {.is-info}

> ffuf est disponible au téléchargement [ici](https://github.com/ffuf/ffuf)
> {.is-info}

# Syntaxe

`ffuf [-w <fichier wordlist>:<mot clé>] [-u <cible<mot clé>>] [paramètres]`

# Paramètres

| Paramètre                   | Description                                                                                                  |
| --------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `-h`                        | Affiche l'aide.                                                                                              |
| `-H <nom:valeur>`           | Précise un header. Plusieurs -H peuvent être utilisés.                                                       |
| `-X <méthode HTTP>`         | Précise la méthode HTTP à utiliser. (GET par défaut)                                                         |
| `-b <nom=valeur>`           | Précise le/les données des cookies. (chaque entrée doit être séparée par un point-virgule)                   |
| `-d <données POST>`         | Précise les données POST lors des requêtes POST.                                                             |
| `-recursion`                | Effectue le opérations récursivement, l'URL doit se terminer par le mot clé FUZZ.                            |
| `-recursion-depth <nombre>` | Précise le niveau de récursion. (0 par défaut)                                                               |
| `-u <cible<FUZZ>>`          | Précise l'URL cible.                                                                                         |
| `-mc <all,code HTTP>`       | Précise le code HTTP attendu. (par défaut: 200,204,301,302,307,401,403). Préciser "all" pour tous les codes. |
| `-ms <taille>`              | Spécifie la taille de la réponse attendue.                                                                   |
| `-fc <code HTTP>`           | Filtre par code HTTP. (chaque entrée doit être séparée par un point-virgule)                                 |
| `-fs <taille>`              | Spécifie la/les tailles de la réponse attendue. (chaque entrée doit être séparée par un point-virgule)       |
| `-w <fichier>:<mot clé>`    | Spécifie le fichier wordlist. Il est possible d'utiliser des mots clés. (par défaut le mot clé est FUZZ)     |
| `-o <fichier>`              | Spécifie le fichier de sortie.                                                                               |
| `-t <nombre>`               | Spécifie le nombre de threads à utiliser. (40 par défaut)                                                    |
| `-ic`                       | Ne prend pas en compte les lignes commentés des wordlists.                                                   |

# Exemples

Effectue une simple découverte de répertoire.
`ffuf -w ./wordlist.txt -u https://www.example.com/FUZZ`

Effectue une simple découverte de répertoire, en utilisant un autre mot clé que FUZZ avec 64 threads.
`ffuf -w ./wordlist.txt:FFUF -u https://www.example.com/FFUF -t 64`

# Voir aussi

Documentation officielle
https://github.com/ffuf/ffuf/wiki

Guide détaillé sur ffuf
https://codingo.io/tools/ffuf/bounty/2020/09/17/everything-you-need-to-know-about-ffuf.html
