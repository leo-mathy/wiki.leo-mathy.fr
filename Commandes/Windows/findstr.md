---
title: findstr
description: Recherche du texte dans les fichiers.
published: true
date: 2024-10-25T20:22:34.725Z
tags: windows, commande
editor: markdown
dateCreated: 2024-08-29T16:16:19.597Z
---

# Introduction

findstr permet de rechercher du texte dans les fichiers.

# Syntaxe

`findstr <texte> <fichier> [paramètres]`

# Paramètres

| Paramètre                  | Description                                                                                                                |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `/b`                       | Recherche au début de la ligne.                                                                                            |
| `/e`                       | Recherche à la fin d'une ligne.                                                                                            |
| `/l`                       | Traite la chaîne de recherche telle quelle. (contrairement à /r)                                                           |
| `/r`                       | Traite la chaîne de recherche en tant qu’expressions régulières. (paramètre par défaut) (contrairement à /l)               |
| `/s`                       | Effectue la recherche dans le répertoire actif ainsi que dans les sous-répertoires.                                        |
| `/i`                       | ignore la casse des caractères.                                                                                            |
| `/x`                       | Affiche les lignes qui correspondent exactement.                                                                           |
| `/v`                       | Affiche les lignes qui ne correspondent pas.                                                                               |
| `/n`                       | Affiche le numéro des lignes.                                                                                              |
| `/m`                       | Affiche uniquement le nom du fichier si une correspondance est trouvé à l'intérieur.                                       |
| `/o`                       | Imprime le décalage des caractères avant chaque ligne correspondante.                                                      |
| `/p`                       | Ignore les fichiers avec des caractères non imprimables.                                                                   |
| `/off`                     | N’ignore pas les fichiers dont l’attribut offline est défini.                                                              |
| `/f:<fichier>`             | Recherche dans une liste de fichiers contenus dans le fichier spécifié.                                                    |
| `/c:<texte>`               | Traite le texte spécifié comme recherche telle quelle.                                                                     |
| `/g:<fichier>`             | Utilise les chaîne de recherche contenues dans le fichier spécifié.                                                        |
| `/d:<dirlist>`             | Effectue la recherche dans les répertoires spécifiés (Utilisation des points-virgules pour préciser plusieurs répertoires. |
| `/a:<attribut de couleur>` | Précise la couleur (voir color /?)                                                                                         |
| `/?`                       | Affiche l'aide                                                                                                             |

# Exemples

Recherche le mot "password" dans le repertoire actif et les sous repertoires en ignorant la casse du mot. Et uniquement dans les fichiers se terminant en .txt
`findstr /SI /C:"password" *.txt`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/fr-fr/windows-server/administration/windows-commands/findstr
