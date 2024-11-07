---
title: Hydra
description: Puissant outil de Brute-Force supportant de nombreux protocoles.
published: true
date: 2024-11-07T17:32:53.685Z
tags: outil, indépendant, synthèse
editor: markdown
dateCreated: 2024-11-07T17:03:55.416Z
---

# Introduction

Hydra est un puissant outil de Brute-Force supportant de nombreux protocoles. Cet outil est reconnu de par son efficacité (utilisation des threads et connexions parallèles), sa flexibilité (support de nombreux protocoles et services) et sa facilité d'utilisation

> hydra est disponible au téléchargement [ici](https://github.com/vanhauser-thc/thc-hydra)
> {.is-info}

# Syntaxe

`hydra [option(s) d'identifiant] [option(s) de mot de passe] [option(s) de l'attaque] [service://cible] [option(s) du service] [paramètres]`

`hydra [option(s) d'identifiant] [option(s) de mot de passe] [cible] [service] [option(s) du service] [paramètres]`

# Paramètres

| Paramètre                         | Description |
| --------------------------------- | ----------- |
| `-l <identifiant> ` | Spécifie un identifiant à utiliser.         |
| `-L <fichier>` | Spécifie une liste d'identifiants à utiliser.         |
| `-p <mot de passe>` | Spécifie un mot de passe à utiliser.        |
| `-P <fichier>` | Spécifie une liste de mots de passe à utiliser.         |
| `-t <nombre de threads>` | Spécifie le nombre de threads à utiliser.         |
| `-f` | Active le mode rapide, arrète l'attaque après la première réussite de l'authentification.         |
| `-s <port>` | Spécifie un port personnalisé.         |
| `-v` | Active le mode verbose.         |
| `-V` | Active le mode verbose avancé.         |
| `-m <options>` | Spécifie les options spécifiques au service.         |
| `-M <fichier>` | Spécifie une liste de cible
.         |

# Exemples

Lancement d'une attaque avec le module http-get en utilisant une liste d'identifiants et de mots de passe.
`hydra -L logins.txt -P passwords.txt www.example.com http-get
`
Lancement d'une attaque avec le module http-post-form en utilisant une liste de mots de passe. Précise les détails de la requète et le code de retour HTTP qui correpsond au code attendu.
`hydra -l admin -P pass.txt www.example.com http-post-form "/connexion:user=^USER^&pass=^PASS^:S=302"`

# Voir aussi
