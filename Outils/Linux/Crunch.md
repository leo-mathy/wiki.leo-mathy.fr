---
title: Crunch
description: Permet de générer des listes de mots en fonction de paramètres comme la longueur, les mots, les caractères ou encore un patron.Permet de générer des listes de mots en fonction de paramètres comme la longueur, les mots, les caractères ou encore un patern.
published: true
date: 2024-11-19T18:20:21.753Z
tags: outil, linux
editor: markdown
dateCreated: 2024-11-18T18:36:06.762Z
---

# Introduction

Crunch permet de générer des listes de mots en fonction de paramètres comme la longueur, les mots, les caractères ou encore un patron.

> Crunch est disponible au téléchargement [ici](https://sourceforge.net/projects/crunch-wordlist/)
> {.is-info}

# Syntaxe

`crunch <longueur minimale> <longueur maximale> [-o <fichier de sortie/"START">] [-t <patron>] [paramètres]`

# Paramètres

| Paramètre                   | Description                                                                                                                                                              |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-b <nombre>`               | Spécifie la taille maximale du fichier de sortie en Octets.                                                                                                              |
| `-c <nombre>`               | Spécifie le nombre de lignes maximal dans le fichier de sortie. À utiliser avec "-o START" uniquement. (Génère plusieurs fichiers en fonction du nombre de générations). |
| `-d <nombre<symbole>`       | Supprime la génération de chaînes avec plus de X nombre de doublons adjacents du jeu de caractères donné.                                                                |
| `-e <chaîne de caractères>` | Stoppe la génération lorsque la chaîne de caractères spécifiée est atteinte.                                                                                             |
| `-f <fichier>`              | Spécifie un fichier de codage de caractères.                                                                                                                             |
| `-i`                        | Inverse la sortie.                                                                                                                                                       |
| `-l <caractères>`           | Spécifie les caractères à ne pas interpréter.                                                                                                                            |
| `-o <fichier/START>`        | Spécifie le fichier de sortie. Si START est utilisé, le fichier généré portera le nom de la première génération et de la dernière.                                       |
| `-p <caractères/mots>`      | Ne répète aucun caractère ou mot indiqué.                                                                                                                                |
| `-q <fichier>`              | Ne répète aucun caractère ou mot indiqué dans un fichier.                                                                                                                |
| `-r`                        | Résume la session précédente.                                                                                                                                            |
| `-s <chaîne de caractères>` | Spécifie la génération de départ.                                                                                                                                        |
| `-t <patron>`               | Spécifie un patron. Il peut être composé en plus de texte, de "@" (pour a-z), "," (pour A-Z), "%" (pour 0-9) et "^" (pour les symboles).                                 |
| `-u`                        | Désactive le threading permettant l'affichage de l'avancée.                                                                                                              |
| `-z`                        | Ajoute le support pour la compression du fichier de sortie. Doit être utilisé avec "-o" et les extensions gzip, bzip, lzma et 7z.                                        |

# Exemples

Génère une wordlist de root001 à root999 vers le fichier wordlist.txt
`crunch -t root%%% -o wordlist.txt`

# Voir aussi

CUPP (Common User Passwords Profiler)[cupp](/Outils/Indépendant/cupp)
