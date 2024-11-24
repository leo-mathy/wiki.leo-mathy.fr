---
title: sqlmap
description: Outil d'automatisation de détection et d'exploitation de failles SQLi (SQL Injection).
published: true
date: 2024-11-24T13:45:11.585Z
tags: outil, indépendant, synthèse
editor: markdown
dateCreated: 2024-11-23T16:26:24.352Z
---

# Introduction

sqlmap est un outil d'automatisation de détection et d'exploitation de failles SQLi (SQL Injection).

> sqlmap est disponible au téléchargement [ici](https://github.com/sqlmapproject/sqlmap)
> {.is-info}

# Syntaxe

`...`

# Paramètres

> Des astérisques sont utilisables pour spécifier les paramètres dans lesquels faire les injections.
> {.is-info}

| Paramètre                           | Description                                                                                                                                                                        |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-h`                                | Afficher l'aide basique.                                                                                                                                                           |
| `-hh`                               | Afficher l'aide avancée.                                                                                                                                                           |
| `--batch`                           | Active le mode automatique, passe les demandes.                                                                                                                                    |
| `-u <URI>`                          | Spécifie une URI comme cible.                                                                                                                                                      |
| `-r <fichier>`                      | Utilise un fichier de requête.                                                                                                                                                     |
| `--data <données de requètes POST>` | Spécifie les valeurs de la requête POST.                                                                                                                                           |
| `--cookie=<données du cookie>`      | Spécifie les valeurs des paramètres du cookie.                                                                                                                                     |
| `-H <header>/ --header <header>`    | Spécifie les valeurs des headers.                                                                                                                                                  |
| `--random-agent`                    | Utilise une valeur aléatoire parmi une liste pour le champ User-agent (par défaut la valeur de ce champ est sqlmap). Cela est utile pour contourner certaines mesures de sécurité. |
| `--method <méthode HTTP>`           | Spécifie une autre méthode HTTP pour effectuer la requête.                                                                                                                         |
| `--dump`                                | Récupère toutes les entrées d'une ou plusieurs tables.                                                                                                                                                           |
| `-T <table>`                                | Spécifie la table à récupérer.                                                                                                                                                           |
| `--parse-errors`                                | Afficher les erreurs du SGBD dans le terminal.                                                                                                                                                           |
| `-t <fichier>`                                | Stocke les requètes et réponses dans un fichier.                                                                                                                                                           |
| `-v <niveau>`                                | Spécifie le niveau du mode verbose.                                                                                                                                                           |
| `--proxy <adresse>`                                | Spécifie le proxy à utiliser.                                                                                                                                                           |
| `--level <1-5>`                                | Spécifie le niveau de vecteurs et limites à utiliser. (1 par défaut)                                                                                                                                                            |
| `--risk <1-3>`                                | Spécifie le niveau de vecteurs, basé sur le risque de problème au niveau de la cible. (1 par défaut)                                                                                                                                                           |
| `--prefix <préfixe>`                                | Spécifie le préfixe du vecteur.                                                                                                                                                          |
| `--suffix <suffixe>`                                | Spécifie le suffixe du vecteur.                                                                                                                                                         |
| `--code <code HTTP>`                                | Spécifie le code HTTP pour la détection des réponses VRAI.                                                                                                                                                         |
| `--titles <titre>`                                | Spécifie le contenu de la balise title pour la détection des réponses VRAI.                                                                                                                                                         |
| `--string <valeur>`                                | Spécifie une valeur pour la détection des réponses VRAI.                                                                                                                                                         |
| `--text-only`                                | Se base uniquement sur le texte affiché pour la détection des réponses VRAI.                                                                                                                                                         |
| `--string <valeur>`                                | Spécifie une valeur pour la détection des réponses VRAI.                                                                                                                                                         |
| `--string <valeur>`                                | Spécifie une valeur pour la détection des réponses VRAI.                                                                                                                                                         |





# Exemples

# Voir aussi
