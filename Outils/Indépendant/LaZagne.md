---
title: LaZagne
description: Recherche et récupère de nombreux mots de passe stockés sur un ordinateur, dans différentes applications couramment utilisées ou stockés par des mécanismes internes.
published: true
date: 2024-09-26T17:22:43.475Z
tags: outil, indépendant
editor: markdown
dateCreated: 2024-09-26T16:44:07.624Z
---

# Introduction

LaZagne est un outil qui permet de rechercher et récupérer de nombreux mots de passe stockés sur un ordinateur, dans différentes applications couramment utilisées ou stockés par des mécanismes internes. Il est aussi possible d'utiliser des modules externes spécifiques à certaines applications, services ou tout ce qui peut contenir des mots de passe.

> LaZagne est disponible au téléchargement [ici](https://github.com/AlessandroZ/LaZagne)
> {.is-info}

# Syntaxe

`LaZagne <module> [-<script spécifique>] [paramètres]`

# Paramètres

| Paramètre                   | Description                                                                                                                                                                                   |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-version`                  | Affiche la version de LaZagne.                                                                                                                                                                |
| `-oN`                       | Enregistre les mots de passe trouvés dans un fichier au format texte.                                                                                                                         |
| `-oJ`                       | Enregistre les mots de passe trouvés dans un fichier au format Json.                                                                                                                          |
| `-oA`                       | Enregistre les mots de passe trouvés dans un fichier au format texte et un fichier au format Json.                                                                                            |
| `-output <répertoire>`      | Spécifie le répertoire où les fichiers sont enregistrés.                                                                                                                                      |
| `-h`                        | Affiche l'aide globale ou pour un module spécifique.                                                                                                                                          |
| `-v`                        | Mode verbeux.                                                                                                                                                                                 |
| `-vv`                       | Mode verbeux détaillé.                                                                                                                                                                        |
| `-quiet`                    | Ne produit aucune sortie dans le terminal.                                                                                                                                                    |
| `-password <mot de passe>`  | Précise le mot de passe de l'utilisateur actuel pour le déchiffrement d'identifiants du domaine. Si ce paramètre n'est pas précisé, LaZagne testera les mots de passe Windows déjà récupérés. |
| `--password <mot de passe>` | (Mac OS) Précise le mot de passe de l'utilisateur actuel. Il est difficile de récupérer des mots de passe sans cela sur Mac OS.                                                               |
| `-i`                        | (Mac OS) Active le mode intéractif pour la saisie des mots de passe.                                                                                                                          |

# Modules

La liste des modules par défaut est disponible [ici](https://github.com/AlessandroZ/LaZagne?tab=readme-ov-file#supported-software). Il est possible d'importer d'autres modules.

> Chaque module contient des scripts, il est possible de lancer un script spécifique comme indiqué dans la syntaxe.
> {.is-info}

> Certains modules nécessites des droits administrateurs (pour l'accès aux cartes wifi par exemple)
> {.is-warning}

> Tous les modules et scripts ne sont pas présents entre Linux, Windows et Mac OS.
> {.is-warning}

| Module                                 | Description                                                           |
| -------------------------------------- | --------------------------------------------------------------------- |
| `all`                                  | Lance tous les modules.                                               |
| `Browsers`                             | Module comportant de nombreux navigateurs web.                        |
| `Chats`                                | Module comportant des applications de communication de type tchat.    |
| `Databases`                            | Module comportant des Systèmes de Gestion de Bases de Données (SGBD). |
| `Games`                                | Module comportant des jeux.                                           |
| `Git`                                  | Module comportant les applications Git.                               |
| `Mails`                                | Module comportant des clients mails.                                  |
| `Maven`                                | Module comportant l'outil Apache Maven.                               |
| `Dumps from memory`                    | Module utilisant la mémoire de la machine.                            |
| `Multimedia`                           | Module comportant des outils multimédias.                             |
| `PHP`                                  | Module comportant des outils PHP.                                     |
| `SVN`                                  | Module comportant des clients SVN.                                    |
| `Sysadmin`                             | Module comportant des outils d'administration système.                |
| `Wifi`                                 | Module utilisant des méthodes basées sur le WIFI.                     |
| `Internal mechanism passwords storage` | Module utilisant des mécanismes de stockages de mots de passe.        |

# Exemples

Lance tous les modules et enregistre les mots de passe trouvés dans un fichier au format texte, dans le répertoire C:\temp.
`laZagne.exe all -oA -output C:\temp\`

# Voir aussi

Wiki officiel:
https://github.com/AlessandroZ/LaZagne/wiki/
