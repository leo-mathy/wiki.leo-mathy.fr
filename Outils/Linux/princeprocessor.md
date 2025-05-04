---
title: princeprocessor
description: Génère des candidats de mots de passe depuis une liste de mots en utilisant l'algorithme de Prince (PRobability INfinite Chained Elements).
published: true
date: 2025-05-04T14:54:51.170Z
tags: outil, linux, synthèse
editor: markdown
dateCreated: 2024-11-19T18:50:40.930Z
---

# Introduction

princeprocessor permet de générer des candidats de mots de passe depuis une liste de mots en utilisant l'algorithme de Prince (PRobability INfinite Chained Elements).

> princeprocessor est disponible au téléchargement [ici](https://github.com/hashcat/princeprocessor)
> {.is-info}

# Syntaxe

`pp64.bin [paramètres] [<] <fichier d'entrée>`

# Paramètres

| Paramètre                                                    | Description                        |
| ------------------------------------------------------------ | ---------------------------------- |
| `-v`                                                         | Affiche la version.                |
| `-h`                                                         | Affiche l'aide.                    |
| `--keyspace`                                                 | Calcule le nombre de combinaisons. |
| `-o <fichier de sortie>,  --output-file=<fichier de sortie>` | Spécifie le fichier de sortie.     |

> Par défaut, uniquement les mots inférieurs à 16 de longueur sont sauvegardés.
> {.is-warning}

# Exemples

Génère une liste de mots de passe candidats depuis la liste de mots words.
`./pp64.bin -o wordlist.txt < words`

# Voir aussi

Point de l'auteur présentant l'outil à la conférence "Passwords^14".
https://hashcat.net/events/p14-trondheim/prince-attack.pdf

Présentation détaillée de l'outil.
http://reusablesec.blogspot.de/2014/12/tool-deep-dive-prince.html
