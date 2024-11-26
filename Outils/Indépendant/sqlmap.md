---
title: sqlmap
description: Outil d'automatisation de détection et d'exploitation de failles SQLi (SQL Injection).
published: true
date: 2024-11-26T18:45:53.720Z
tags: outil, indépendant, synthèse
editor: markdown
dateCreated: 2024-11-23T16:26:24.352Z
---

# Introduction

sqlmap est un outil d'automatisation de détection et d'exploitation de failles SQLi (SQL Injection).

> sqlmap est disponible au téléchargement [ici](https://github.com/sqlmapproject/sqlmap)
> {.is-info}

# Syntaxe

`sqlmap <lien avec la base de données> [paramètres]`

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
| `--dump`                            | Récupère toutes les entrées d'une ou plusieurs tables.                                                                                                                             |
| `--dump-all`                        | Récupère toutes les entrées de toutes les tables de toutes les bases de données.                                                                                                   |
| `--exclude-sysdbs`                  | Né récupère pas les bases de données systèmes.                                                                                                                                     |
| `-T <table>`                        | Spécifie la table à récupérer.                                                                                                                                                     |
| `--tables`                          | Liste les tables présentes dans la base de données.                                                                                                                                |
| `--parse-errors`                    | Afficher les erreurs du SGBD dans le terminal.                                                                                                                                     |
| `-t <fichier>`                      | Stocke les requêtes et réponses dans un fichier.                                                                                                                                   |
| `-v <niveau>`                       | Spécifie le niveau du mode verbose.                                                                                                                                                |
| `--proxy <adresse>`                 | Spécifie le proxy à utiliser.                                                                                                                                                      |
| `--level <1-5>`                     | Spécifie le niveau de vecteurs et limites à utiliser. (1 par défaut)                                                                                                               |
| `--risk <1-3>`                      | Spécifie le niveau de vecteurs, basé sur le risque de problème au niveau de la cible. (1 par défaut)                                                                               |
| `--prefix <préfixe>`                | Spécifie le préfixe du vecteur.                                                                                                                                                    |
| `--suffix <suffixe>`                | Spécifie le suffixe du vecteur.                                                                                                                                                    |
| `--code <code HTTP>`                | Spécifie le code HTTP pour la détection des réponses VRAI.                                                                                                                         |
| `--titles <titre>`                  | Spécifie le contenu de la balise title pour la détection des réponses VRAI.                                                                                                        |
| `--string <valeur>`                 | Spécifie une valeur pour la détection des réponses VRAI.                                                                                                                           |
| `--text-only`                       | Se base uniquement sur le texte affiché pour la détection des réponses VRAI.                                                                                                       |
| `--technique <technique(s)>`        | Spécifie les techniques SQLi à utiliser.                                                                                                                                           |
| `--banner`                          | Récupère la bannière.                                                                                                                                                              |
| `--current-user`                    | Récupère le nom de l'utilisateur actuel.                                                                                                                                           |
| `--current-db`                      | Récupère le nom de la base de données actuelle.                                                                                                                                    |
| `--is-dba`                          | Indique si l'utilisateur actuel a des droits d'administrateurs de la base de données.                                                                                              |
| `-D <base de données>`              | Précise la base de données dans laquelle effectuer les opérations.                                                                                                                 |
| `--dump-format <format>`            | Spécifie le format à utiliser lors de la récupération des tables. (csv par défaut)                                                                                                 |
| `-C <colonnes>`                     | Spécifie le nom des colonnes à récupérer.                                                                                                                                          |
| `--start <numéro de ligne>`         | Spécifie la ligne de début à récupérer.                                                                                                                                            |
| `--stop <numéro de ligne>`          | Spécifie la ligne de fin à récupérer.                                                                                                                                              |
| `--where=<condition SQL>`           | Spécifie les lignes à récupérer à l'aide d'une condition. (exemple: name LIKE 'françois')                                                                                          |
| `--schema`                          | Affiche l'architecture complète de la base de données.                                                                                                                             |
| `--search`                          | Spécifie que l'élément indiquée (table, colonne, base de données) est une recherche.                                                                                               |
| `--passwords`                       | Énumère les hashes des utilisateurs du SGBD.                                                                                                                                       |
| `--csrf-token=<nom du token>`       | Défini le nom du token anti-CSRF pour le réutiliser dans les prochaines requêtes..                                                                                                 |
| `--randomize=<champ>`               | Défini le champ dans la requête à rendre aléatoire.                                                                                                                                |
| `--tor`                             | Utilise le réseau Tor comme proxy.                                                                                                                                                 |
| `--tamper <script>`                 | Utilise un script d'altération de la requête.                                                                                                                                      |
| `--list-tampers`                    | Liste les scripts pythons utilisables pour altérer les requêtes.                                                                                                                   |
| `--file-read <fichier>`             | Récupère un fichier depuis la cible.                                                                                                                                               |
| `--file-write <fichier>`            | Écrit un fichier sur la cible.                                                                                                                                                     |
| `--file-dest <répertoire>`          | Spécifie l'emplacement du fichier lors de l'écriture d'un fichier sur la cible.                                                                                                    |
| `--os-shell`                        | Demande un shell interactif.                                                                                                                                                       |

# Exemples

Récupère la table "users" en utilisant une requête POST avec comme paramètre d'injection "id".
De plus, le script d'altération between est utilisé pour contourner le WAF en plus d'utiliser une valeur aléatoire parmi une liste pour le champ User-agent.

`sudo sqlmap -u http://192.168.1.1:4343/index.php?id=1 --batch --data='{"id":1}' --random-agent --method POST -H 'Content-Type:application/json' --dump --tamper between.py -T users`

# Voir aussi

Documentation officielle
https://github.com/sqlmapproject/sqlmap/wiki

Usage de sqlmap
https://github.com/sqlmapproject/sqlmap/wiki/usage
