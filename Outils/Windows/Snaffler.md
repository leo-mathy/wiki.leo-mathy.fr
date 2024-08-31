---
title: Snaffler
description: Recherche des partages de fichiers sur les ordinateurs d'un domaine Active Directory et indique les permissions sur ceux-ci. De plus, Snaffler utilise des règles pour filtrer les fichiers pouvant être intéressants.
published: true
date: 2024-08-31T14:08:12.747Z
tags: outil, windows
editor: markdown
dateCreated: 2024-08-30T17:08:08.063Z
---

# Introduction

Snaffler permet de rechercher des partages de fichiers sur les ordinateurs d'un domaine Active Directory et indique les permissions sur ceux-ci. De plus, Snaffler utilise des règles pour filtrer les fichiers pouvant être intéressants.

>  Snaffler est disponible au téléchargement [ici](https://github.com/SnaffCon/Snaffler)
{.is-info}

# Syntaxe

`Snaffler.exe <-o <fichier de sortie>|-s> [paramètres]`

# Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `-e <minutes>, --timeout <minutes>`     | Défini l'intervalle de temps mort, si aucune réponse n'est reçu dans ce temps alors l'opération échoue. (5minutes par défaut). Utile si la connexion est lente ou si un temps d'attente entre chaque requête LDAP est présent.        |
| `-z <fichier|generate>, --config <fichier|generate>` | Chemin vers un fichier de configuration au format .toml, Si le paramètre est utilisé avec le terme "generate" alors un fichier sera créer.  |
| `-o <fichier>, --outfile <fichier>` | Précise le fichier de sortie. |
| `-h, --help` | Affiche l'aide. |
| `-s, --stdout` | Active la sortie dans le terminal et affiche les résultats en temps réel. |
| `-m <repertoire>, --snaffle <repertoire>` | Spécifie un repertoire ou Snaffler effectuera une copie de chaque fichier trouvé. |
| `-l <taille>, --snafflesize <taille>` | Spécifie la taille maximum des fichiers à copier. (10Mb par défaut) |
| `-i <chemin>, --dirtarget <chemin>` | Spécifie un chemin pour directement effectuer une recherche de fichiers. Désactive la découverte de partages automatique. |
| `-b <niveau>, --interest <niveau>` | Spécifie le niveau d'intérêt au raport (de 0 à 3) |
| `-d <domaine>` | ... |
| `...` | ... |
| `...` | ... |
| `...` | ... |
| `...` | ... |
| `...` | ... |
| `...` | ... |
| `...` | ... |

# Exemples

# Voir aussi

        -d, --domain[optional]... Domain to search for computers to search for shares on to search for files in. Easy.

        -v, --verbosity[optional]... Controls verbosity level, options are Trace (most verbose), Debug (less verbose), Info (less verbose still, default), and Data (results only). e.g '-v debug'

        -c, --domaincontroller[optional]... Domain controller to query for a list of domain computers.

        -r, --maxgrepsize[optional]... The maximum size file (in bytes) to search inside for interesting strings. Defaults to 500k.

        -j, --grepcontext[optional]... How many bytes of context either side of found strings in files to show, e.g. -j 200

        -u, --domainusers[optional]... Makes Snaffler grab a list of interesting-looking accounts from the domain and uses them in searches.

        -y, --tsv[optional]... Makes Snaffler output as tsv.

        -f, --dfs[optional]... Limits Snaffler to finding file shares via DFS, for "OPSEC" reasons.

        -a, --sharesonly[optional]... Stops after finding shares, doesn't walk their filesystems.

        -x, --maxthreads[optional]... How many threads to be snaffling with. Any less than 4 and you're gonna have a bad time.

        -n, --comptarget[optional]... Computer (or comma separated list) to target.

        -p, --rulespath[optional]... Path to a directory full of toml-formatted rules. Snaffler will load all of these in place of the default ruleset.

        -t, --logtype[optional]... Type of log you would like to output. Currently supported options are plain and JSON. Defaults to plain.

        -k, --exclusions[optional]... Path to a file containing a list of computers to exclude from scanning.
