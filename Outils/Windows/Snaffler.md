---
title: Snaffler
description: Recherche des partages de fichiers sur les ordinateurs d'un domaine Active Directory et indique les permissions sur ceux-ci. De plus, Snaffler utilise des règles pour filtrer les fichiers pouvant être intéressants.
published: true
date: 2024-08-31T14:30:19.479Z
tags: outil, windows
editor: markdown
dateCreated: 2024-08-30T17:08:08.063Z
---

# Introduction

Snaffler permet de rechercher des partages de fichiers sur les ordinateurs d'un domaine Active Directory et indique les permissions sur ceux-ci. De plus, Snaffler utilise des règles pour filtrer les fichiers pouvant être intéressants.

> Snaffler est disponible au téléchargement [ici](https://github.com/SnaffCon/Snaffler)
> {.is-info}

# Syntaxe

`Snaffler.exe <-o <fichier de sortie>|-s> [paramètres]`

# Paramètres

| Paramètre                                                                  | Description                                                                                                                                                                                                                    |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `-e <minutes>, --timeout <minutes>`                                        | Défini l'intervalle de temps mort, si aucune réponse n'est reçu dans ce temps alors l'opération échoue. (5minutes par défaut). Utile si la connexion est lente ou si un temps d'attente entre chaque requête LDAP est présent. |
| `-z <fichier                                                               | generate>, --config <fichier                                                                                                                                                                                                   | generate>` | Chemin vers un fichier de configuration au format .toml, Si le paramètre est utilisé avec le terme "generate" alors un fichier sera créer. |
| `-o <fichier>, --outfile <fichier>`                                        | Précise le fichier de sortie.                                                                                                                                                                                                  |
| `-h, --help`                                                               | Affiche l'aide.                                                                                                                                                                                                                |
| `-s, --stdout`                                                             | Active la sortie dans le terminal et affiche les résultats en temps réel.                                                                                                                                                      |
| `-m <repertoire>, --snaffle <repertoire>`                                  | Spécifie un repertoire ou Snaffler effectuera une copie de chaque fichier trouvé.                                                                                                                                              |
| `-l <taille>, --snafflesize <taille>`                                      | Spécifie la taille maximum des fichiers à copier (10Mb par défaut).                                                                                                                                                            |
| `-i <chemin>, --dirtarget <chemin>`                                        | Spécifie un chemin pour directement effectuer une recherche de fichiers. Désactive la découverte de partages automatique.                                                                                                      |
| `-b <niveau>, --interest <niveau>`                                         | Spécifie le niveau d'intérêt au raport (de 0 à 3).                                                                                                                                                                             |
| `-d <domaine> --domain <domaine>`                                          | Précise le domaine sur lequel rechercher les ordinateurs.                                                                                                                                                                      |
| `-v <niveau>, --verbosity <niveau>`                                        | Spécifie le niveau de verbosité à utiliser (Trace;Debug;Info;Data).                                                                                                                                                            |
| `-c <controlleur de domaine>, --domaincontroller <controlleur de domaine>` | Précise quel controlleur de domaine intéroger.                                                                                                                                                                                 |
| `-r <taille>, --maxgrepsize <taille>`                                      | Indique la taille maximum d'un fichier (en octets) pour effectuer une recherche à l'intérieur (500octets par défaut).                                                                                                          |
| `-j <taille>, --grepcontext <taille>`                                      | Spécifie de combien d'octets encadrer un résultat. Permet de voir les informations situés aux abords du résultat.                                                                                                              |
| `-u, --domainusers`                                                        | Snaffler recueille le noms de certains comptes intéressants et utilise ces noms dans les recherches.                                                                                                                           |
| `-y, --tsv`                                                                | Utilise le format de sortie TSV (utile si la sortie est redirigée vers d'autres outils).                                                                                                                                       |
| `-f, --dfs`                                                                | Utilise uniquement le protocole DFS lors de la découverte de partage de fichiers (Utile pour laisser moins de traces).                                                                                                         |
| `-a, --sharesonly`                                                         | Cherche uniquement des partages de fichiers sans acceder à leurs fichiers.                                                                                                                                                     |
| `-x <threads>, --maxthreads <threads>`                                     | Indique le nombre de threads à utiliser.                                                                                                                                                                                       |
| `-n <ordinateur>, --comptarget <ordinateur>`                               | Indique l'ordinateur ou les ordinateurs (séparés par des virgules) à cibler.                                                                                                                                                   |
| `-p <repertoire>, --rulespath <repertoire>`                                | Spécifie le repertoire qui contient des règles au format toml.                                                                                                                                                                 |
| `-t <json                                                                  | plain>, --logtype <json                                                                                                                                                                                                        | plain>`    | Spécifie le type de sortie entre json et texte brut (texte brut par défaut).                                                               |
| `-k <fichier>, --exclusions <fichier>`                                     | Spécifie le fichier contenant des ordinateurs à exclure de la recherche.                                                                                                                                                       |

# Exemples

Lance snaffler en mode verbose au niveau Info et redirige la sortie vers le terminal et le fichier snaffler.log. Recherche uniquement des partages de fichiers sans acceder aux fichiers situés sur ceux-ci.
`snaffler.exe -s -o snaffler.log -v info -a`
