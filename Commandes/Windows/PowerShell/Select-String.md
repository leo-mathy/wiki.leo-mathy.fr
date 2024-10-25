---
title: Select-String
description: Recherche du texte dans les fichiers et des chaînes.
published: true
date: 2024-10-25T20:34:07.036Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-08-30T16:17:34.831Z
---

# Introduction

L'applet Select-String permet de chercher du texte dans les fichiers et des chaînes.

# Syntaxe

`Select-String <recherche> <fichier|objet powershell> [paramètres]`

# Paramètres

| Paramètre                                 | Description                                                                                                                    |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `-AllMatches`                             | Continue la recherche sur la même ligne si une correspondance est trouvée (Par défaut la recherche passe à la ligne suivante). |
| `-CaseSensitive`                          | N'ignore pas la casse des caractères.                                                                                          |
| `-Context <nombre de lignes avant,après>` | Précise le nombre de lignes à capturer avant et après le résultat.                                                             |
| `-Culture <culture>`                      | Spécifie la culture de la recherche (utile pour faire des recherches dans d'autres langages)                                   |
| `-Encoding <codage>`                      | Précise l'encodage à utiliser pour la recherche (ascii;ansi;utf8...).                                                          |
| `-Exclude <élement>`                      | Exclu des fichiers de la recherche. Wildcard utilisable.                                                                       |
| `-Include <élement>`                      | Inclus des fichiers de la recherche. Wildcard utilisable.                                                                      |
| `-InputObject <objet powershell>`         | Spécifie le texte à rechercher à l'aide d'un objet powershell.                                                                 |
| `-List`                                   | Passe au fichier suivant dès que la recherche à trouvé un résultat.                                                            |
| `-LiteralPath <chemin>`                   | Indique le chemin littéralement (la valeur est utilisée exactement comme elle est tapée).                                      |

| `-NoEmphasis` | Ne met pas en surbrillance le terme recherché lors de son affichage. |
| `-Path <chemin>` | Indique le chemin la recherche est effectuée |
| `-Pattern <recherche>` | Spécifie la recherche, il est possible d'utiliser des expressions régulières. |
| `-Quiet` | Retourne une réponse simple comme sortie au lieu d'un objet MatchInfo. |
| `-Raw` | Retourne les résultats correspondants uniquement. Sans utiliser d'objet MatchInfo. |
| `-SimpleMatch` | N'utilise pas une expression régulière lors de la recherche. |

# Exemples

Recherche le terme "password" dans les fichiers .txt du repertoire actuel.
`Select-String -Path *.txt *.php -Pattern 'password'`

Recherche le terme "password" dans les fichiers .txt et .php du repertoire C:\tmp\.
`Select-String -Include *.txt,*.php -Path 'C:\tmp\*' -Pattern 'password'`

Recherche le terme "password" récursivement dans les fichiers .txt et .php du repertoire C:\tmp\.
`Get-ChildItem C:\tmp\ -Recurse | Select-String -Include *txt,*.php -Pattern 'password'`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.utility/select-string
