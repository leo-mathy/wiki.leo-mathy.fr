---
title: hashID
description: Permet d'identifier de nombreux types de hash.
published: true
date: 2025-05-04T14:54:01.094Z
tags: outil, indépendant
editor: markdown
dateCreated: 2024-11-10T17:21:57.364Z
---

# Introduction

hashID est un outil permettant d'identifier de nombreux types de hash.

> hashID est disponible au téléchargement [ici](https://github.com/psypanda/hashID)
> {.is-info}

# Syntaxe

`hashid.py [paramètres] <fichier/hash>`

# Paramètres

| Paramètre                          | Description                                              |
| ---------------------------------- | -------------------------------------------------------- |
| `-e, --extended`                   | Liste tous les algorithmes de mots de passe avec salage. |
| `-m, --mode`                       | Affiche le mode de Hashcat associé.                      |
| `-j, --john`                       | Affiche le mode de JohnTheRipper associé.                |
| `-o <fichier> --outfile <fichier>` | Spécifie le fichier de sortie.                           |
| `--help`                           | Affiche l'aide.                                          |
| `--version`                        | Affiche la version.                                      |

# Exemples

Identifie les hashes situés dans le fichier "./myhashes.txt" et donne le mode Hashcat associé.
`hashid.py -m ./myhashes.txt`

# Voir aussi

Exemples de hashes
https://hashcat.net/wiki/doku.php?id=example_hashes
