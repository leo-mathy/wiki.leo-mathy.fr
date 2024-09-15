---
title: hashcat
description: hashcat est un puissant outil pour l'obtention de mots de passe avec diverse méthodes (brute-force, dictionnaire...).
published: true
date: 2024-09-15T10:33:35.479Z
tags: outil, rédaction incomplète
editor: markdown
dateCreated: 2024-09-14T19:05:36.980Z
---

# Introduction

hashcat est un puissant outil pour l'obtention de mots de passe avec diverse méthodes (brute-force, dictionnaire...).

> hashcat est disponible au téléchargement [ici](https://github.com/hashcat/hashcat)
> {.is-info}

# Syntaxe

`hashcat [paramètres] <hash|fichier contenant un hash|fichier hccapx> [dictionnaire|masque|repertoire]`

# Paramètres

| Paramètre                | Description                                                                                                                                                    |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-m <ID type de hash>`   | Spécifie le type de hash (autodétection par défaut).                                                                                                           |
| `-a <ID type d'attaque>` | Spécifie le type d'attaque (voir Types d'attaques supportées) (attaque par dictionnaire par défaut). |
| `-v`                    | Affiche la version de hashcat.                                                                                                                                                            |
| `-h`                    | Affiche l'aide                                                                                                                                                            |
| `--quiet`                    | N'affiche aucune sortie.                                                                                                                                                            |
| `--hex-charset`                    | Spécifie que le codage est donné en hexadécimal.                                                                                                                                                            |
| `--hex-salt`                    | Spécifie que le salt est donné en hexadécimal.                                                                                                                                                           |
| `--hex-wordlist`                    | Spécifie que les mots du dictionnaires sont donnés en hexadécimal.                                                                                                                                                            |
| `--force`                    | Ignore les avertissements.                                                                                                                                                            |
| `--deprecated-check-disable`                    | Active les extensions non supportées.                                                                                                                                                            |
| `--status`                    | Active le rafraichissement automatique du statut.                                                                                                                                                            |
| `--status-json`                    | Utilise le format json pour la sortie du statut.                                                                                                                                                            |
| `--status-timer=<secondes>`                    | Précise le nombre de secondes entre deux actualisations du statut.                                                                                                                                                            |
| `--stdin-timeout-abort=<secondes>`                    | Interompt l'opération si aucune entrée n'est effectuée depuis le stdin depuis un certain nombre de secondes.                                                                                                                                                            |
| `--machine-readable`                    | Affiche le statut en mode lisible par des machines.                                                                                                                                                            |
| `--keep-guessing`                    | Continuer de chercher le hash après avoir été crack.                                                                                                                                                           |
| `--self-test-disable`                    | Désactive l'autodiagnotic au démarage.                                                                                                                                                            |
| `--loopback`                    | Précise que les fichiers se situent dans le même repertoire. Cela évite de préciser le chemin absolu pour tous les fichiers.                                                                                                                                                          |
| `--markov-hcstat2=<fichier hcstat2>`                    | Précise l'emplacement du fichier hcstat2 à utiliser.                                                                                                                                                            |
| `-markov-disable`                    | Désactive les chaînes de Markov, utilise un brute-force classique.                                                                                                                                                            |
| `--markov-classic`                    | Utilise les chaînes classiques de Markov.                                                                                                                                                           |
| `--markov-inverse`                    | Utilise les chaînes inverseés de Markov.                                                                                                                                                            |
| `-t <nombre>`                    | Précise le seuil après lequel aucune nouvelle chaîne de Markov sera acceptée.                                                                                                                                                           |
| `--runtime=<secondes>`                    | Interompt la session après un nombre de secondes donné.                                                                                                                                                            |
| `--session=<nom>`                    | Spécifie le nom de la session.                                                                                                                                                            |
| `--restore=<nom>`                    | Restore une session avec un nom de session.                                                                                                                                                            |
| `--restore-disable`                    | N'écrit pas de fichier de restoration.                                                                                                                                                            |
| `--restore-file-path=<fichier>`                    | Spécifie l'emplacement du fichier de restoration.                                                                                                                                                            |
| `-o <fichier>`                    | Spécifie le fichier de sortie.                                                                                                                                                            |
| `--outfile-format=<format>`                    | Format de sortie à utiliser (voir Formats de sortie).                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |
| `...`                    | ...                                                                                                                                                            |

# Types d'attaques supportées

| ID type d'attaque                     | Description                                                                             |
| ------------------------------------- | --------------------------------------------------------------------------------------- |
| `3`                                   | [Attaque par Brute-Force](https://hashcat.net/wiki/doku.php?id=mask_attack)             |
| `1`                                   | [Attaque combinatoire](https://hashcat.net/wiki/doku.php?id=combinator_attack)          |
| `0`                                   | [Attaque par dictionnaire](https://hashcat.net/wiki/doku.php?id=dictionary_attack)      |
| `6 ou 7`                              | [Attaque hybride](https://hashcat.net/wiki/doku.php?id=hybrid_attack)                   |
| `3`                                   | [Attaque par masque](https://hashcat.net/wiki/doku.php?id=mask_attack)                  |
| `0`                                   | [Attaque basées sur des règles](https://hashcat.net/wiki/doku.php?id=rule_based_attack) |
| `supporté avec des règles uniquement` | [Attaque à bascule](https://hashcat.net/wiki/doku.php?id=toggle_case_attack)            |
| `9`                                   | [Attaque par association](https://hashcat.net/wiki/doku.php?id=association_attack)      |

# Formats de sortie

| ID type d'attaque                     | Description                                                                             |
| ------------------------------------- | --------------------------------------------------------------------------------------- |
| `1`                                   | hash:salt             |
| `2`                                   | Texte en clair             |
| `3`                                   | Héxadécimal en clair             |
| `4`                                   | Format spécifique aux mots de passe             |
| `5`                                   | Horodatage absolu          |
| `6`                                   | Horodatage relatif          |

# Exemples

# Voir aussi

Documentation officielle et valeurs par défaut
https://hashcat.net/wiki/doku.php?id=hashcat

Les différents hash-mode avec exemples
https://hashcat.net/wiki/doku.php?id=example_hashes
