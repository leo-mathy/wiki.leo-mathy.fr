---
title: hashcat
description: hashcat est un puissant outil pour l'obtention de mots de passe avec diverse méthodes (brute-force, dictionnaire...).
published: true
date: 2024-09-15T10:06:18.967Z
tags: outil, rédaction incomplète
editor: markdown
dateCreated: 2024-09-14T19:05:36.980Z
---

# Introduction

hashcat est un puissant outil pour l'obtention de mots de passe avec diverse méthodes (brute-force, dictionnaire...).

> hashcat est disponible au téléchargement [ici](https://github.com/hashcat/hashcat)
> {.is-info}

# Syntaxe

`hashcat [paramètres] <hash|fichier contenant un hash|fichier hccapx> [dictionnaire|masque|repertoire]`

# Paramètres

| Paramètre                | Description                                                                                                                                                    |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-m <ID type de hash>`   | Spécifie le type de hash (autodétection par défaut).                                                                                                           |
| `-a <ID type d'attaque>` | Spécifie le type d'attaque souhaité (par exemple 3 pour une attaque brute-force ou 0 pour une attaque par dictionnaire) (attaque par dictionnaire par défaut). |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |

# Types d'attaques

| ID type d'attaque                     | Description                                                                             |
| ------------------------------------- | --------------------------------------------------------------------------------------- |
| `3`                                   | [Attaque par Brute-Force](https://hashcat.net/wiki/doku.php?id=mask_attack)             |
| `1`                                   | [Attaque combinatoire](https://hashcat.net/wiki/doku.php?id=combinator_attack)          |
| `0`                                   | [Attaque par dictionnaire](https://hashcat.net/wiki/doku.php?id=dictionary_attack)      |
| `6 ou 7`                              | [Attaque hybride](https://hashcat.net/wiki/doku.php?id=hybrid_attack)                   |
| `3`                                   | [Attaque par masque](https://hashcat.net/wiki/doku.php?id=mask_attack)                  |
| `0`                                   | [Attaque basées sur des règles](https://hashcat.net/wiki/doku.php?id=rule_based_attack) |
| `supporté avec des règles uniquement` | [Attaque à bascule](https://hashcat.net/wiki/doku.php?id=toggle_case_attack)            |
| `9`                                   | [Attaque par association](https://hashcat.net/wiki/doku.php?id=association_attack)      |

# Exemples

# Voir aussi

Documentation officielle et valeurs par défaut
https://hashcat.net/wiki/doku.php?id=hashcat

Les différents hash-mode avec exemples
https://hashcat.net/wiki/doku.php?id=example_hashes
