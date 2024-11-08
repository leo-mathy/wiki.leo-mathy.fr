---
title: Medusa
description: Puissant outil de Brute-Force supportant de nombreux protocoles.
published: true
date: 2024-11-08T18:22:30.560Z
tags: outil, linux, synthèse
editor: markdown
dateCreated: 2024-11-08T18:06:28.140Z
---

# Introduction

Medusa est un puissant outil de Brute-Force supportant de nombreux protocoles. Cet outil est reconnu de par son efficacité (utilisation des threads et connexions parallèles), sa flexibilité (support de nombreux protocoles et services) et sa facilité d'utilisation.

> Medusa est disponible au téléchargement [ici](https://github.com/jmk-foofus/medusa)
> {.is-info}

# Syntaxe

`medusa [cible] [option(s) d'identifiant] [option(s) de mot de passe] -M <module> [paramètres]`

# Paramètres

| Paramètre               | Description                                                                               |
| ----------------------- | ----------------------------------------------------------------------------------------- |
| `-h <cible>`            | Spécifie une cible.                                                                       |
| `-H <fichier>`          | Spécifie une liste de cibles.                                                             |
| `-u <identifiant> `     | Spécifie un identifiant à utiliser.                                                       |
| `-U <fichier>`          | Spécifie une liste d'identifiants à utiliser.                                             |
| `-p <mot de passe>`     | Spécifie un mot de passe à utiliser.                                                      |
| `-P <fichier>`          | Spécifie une liste de mots de passe à utiliser.                                           |
| `-M <module>`           | Spécifie le module à utiliser.                                                            |
| `-m <options>`          | Spécifie les options spécifiques au module.                                               |
| `-t <nombre de tâches>` | Spécifie le nombre de tentatives à effectuer en parallèle.                                |
| `-f, -F`                | Active le mode rapide, arrête l'attaque après la première réussite de l'authentification. |
| `-n <port>`             | Spécifie un port personnalisé.                                                            |
| `-V <1-6>`              | Spécifie le niveau du mode verbose.                                                       |

# Exemples

Lancement d'une attaque avec le module web-form en utilisant une liste de mots de passe. Précise les détails de la requête et le code de retour HTTP qui correspond au message
non attendu.
`medusa -M web-form -h www.example.com -U logins.txt -P passwords.txt -m FORM:"username=^USER^&password=^PASS^:F=403"`

# Voir aussi

Documentation officielle
https://jmk-foofus.github.io/medusa/medusa.html

Site officiel
http://foofus.net/?page_id=51

Collection de listes de différents types (identifiants, mot de passe, URL...)
https://github.com/danielmiessler/SecLists
