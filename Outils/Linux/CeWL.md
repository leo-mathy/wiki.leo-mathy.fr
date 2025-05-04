---
title: CeWL
description: Puissant outil d'extraction de mots depuis un site web pour la création de liste de mots personnalisées.
published: true
date: 2025-05-04T14:54:29.465Z
tags: outil, linux, synthèse
editor: markdown
dateCreated: 2024-11-19T19:08:22.651Z
---

# Introduction

CeWL est un puissant outil d'extraction de mots depuis un site web pour la création de liste de mots personnalisées.

> CeWL est disponible au téléchargement [ici](https://github.com/digininja/CeWL)
> {.is-info}

# Syntaxe

`cewl [paramètres] <url>`

# Paramètres

| Paramètre                                 | Description                                                                                                     |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `-h, --help`                              | Affiche l'aide.                                                                                                 |
| `-k, --keep`                              | Conserve les fichiers téléchargés.                                                                              |
| `-d <nombre>, --depth <nombre>`           | Spécifie le niveau de profondeur maximum des pages suivies. (2 par défaut).                                     |
| `-m <nombre>, --min_word_length <nombre>` | Spécifie la taille minimale des mots récupérés.                                                                 |
| `-o, --offsite`                           | Autoriser la visite d'autres sites.                                                                             |
| `-w <fichier>, --write <fichier>`         | Spécifie le fichier de sortie.                                                                                  |
| `-u <valeur>, --ua <valeur>`              | Spécifie la valeur du champ HTTP User-Agent.                                                                    |
| `-n, --no-words`                          | N'affiche pas la liste de mots.                                                                                 |
| `-a, --meta`                              | Précise à l'outil d'inspecter aussi les métadonnées.                                                            |
| `--meta_file <fichier>`                   | Spécifie le fichier de sortie pour les métadonnées.                                                             |
| `-e, --email`                             | Inclut les adresses mail.                                                                                       |
| `--email_file <fichier>`                  | Spécifie le fichier de sortie pour les adresses mail.                                                           |
| `--meta-temp-dir <répertoire>`            | Spécifie l'emplacement du dossier temporaire utilisé par ExifTool pour la lecture des métadonnées des fichiers. |
| `-c, --count`                             | Affiche le nombre de mots.                                                                                      |
| `-v, --verbose`                           | Active le mode verbose.                                                                                         |
| `--debug`                                 | Active le mode debug.                                                                                           |
| `--auth_type <Digest/basic>`              | Spécifie le mode d'authentification au site.                                                                    |
| `--auth_user <nom d'utilisateur>`         | Spécifie l'utilisateur pour l'authentification au site.                                                         |
| `--auth_pass <mot de passe>`              | Spécifie le mot de passe pour l'authentification au site.                                                       |
| `--proxy_host <adresse>`                  | Spécifie l'adresse du proxy.                                                                                    |
| `--proxy_port <port>`                     | Spécifie le port du proxy.                                                                                      |
| `--proxy_username <nom d'utilisateur>`    | Spécifie l'utilisateur pour l'authentification au proxy.                                                        |
| `--proxy_password <mot de passe>`         | Spécifie le mot de passe pour l'authentification au proxy.                                                      |
| `--header <clé=valeur>, -H <clé=valeur>`  | Spécifie les champs du header. (plusieurs possibles)                                                            |

# Exemples

Créer un fichier wordlist.txt avec les mots extraits de la page http://example.com/blog
`cewl -w wordlist.txt http://example.com/blog `
