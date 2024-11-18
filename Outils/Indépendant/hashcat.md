---
title: hashcat
description: hashcat est un puissant outil pour l'obtention de mots de passe avec diverse méthodes (brute-force, dictionnaire...).
published: true
date: 2024-11-18T18:02:08.918Z
tags: outil, indépendant
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

> En raison d'un nombre conséquent de paramètres, certaines descriptions ne sont pas rédigées pour les paramètres les plus avancés. (voir la documentation officielle)
> {.is-warning}

| Paramètre                              | Description                                                                                                                  |
| -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `-m <ID type de hash>`                 | Spécifie le type de hash (autodétection par défaut).                                                                         |
| `-a <ID type d'attaque>`               | Spécifie le type d'attaque (voir Types d'attaques supportées) (attaque par dictionnaire par défaut).                         |
| `-v`                                   | Affiche la version de hashcat.                                                                                               |
| `-h`                                   | Affiche l'aide                                                                                                               |
| `--quiet`                              | N'affiche aucune sortie.                                                                                                     |
| `--hex-charset`                        | Spécifie que le codage est donné en hexadécimal.                                                                             |
| `--hex-salt`                           | Spécifie que le salt est donné en hexadécimal.                                                                               |
| `--hex-wordlist`                       | Spécifie que les mots du dictionnaires sont donnés en hexadécimal.                                                           |
| `--force`                              | Ignore les avertissements.                                                                                                   |
| `--deprecated-check-disable`           | Active les extensions non supportées.                                                                                        |
| `--status`                             | Active le rafraichissement automatique du statut.                                                                            |
| `--status-json`                        | Utilise le format json pour la sortie du statut.                                                                             |
| `--status-timer=<secondes>`            | Précise le nombre de secondes entre deux actualisations du statut.                                                           |
| `--stdin-timeout-abort=<secondes>`     | Interrompt l'opération si aucune entrée n'est effectuée depuis le stdin depuis un certain nombre de secondes.                |
| `--machine-readable`                   | Affiche le statut en mode lisible par des machines.                                                                          |
| `--keep-guessing`                      | Continuer de chercher le hash après avoir été crack.                                                                         |
| `--self-test-disable`                  | Désactive l'autodiagnostic au démarrage.                                                                                     |
| `--loopback`                           | Précise que les fichiers se situent dans le même répertoire. Cela évite de préciser le chemin absolu pour tous les fichiers. |
| `--markov-hcstat2=<fichier hcstat2>`   | Précise l'emplacement du fichier hcstat2 à utiliser.                                                                         |
| `-markov-disable`                      | Désactive les chaînes de Markov, utilise un brute-force classique.                                                           |
| `--markov-classic`                     | Utilise les chaînes classiques de Markov.                                                                                    |
| `--markov-inverse`                     | Utilise les chaînes inversées de Markov.                                                                                     |
| `-t <nombre>`                          | Précise le seuil après lequel aucune nouvelle chaîne de Markov sera acceptée.                                                |
| `--runtime=<secondes>`                 | Interrompt la session après un nombre de secondes donné.                                                                     |
| `--session=<nom>`                      | Spécifie le nom de la session.                                                                                               |
| `--restore=<nom>`                      | Restore une session avec un nom de session.                                                                                  |
| `--restore-disable`                    | N'écrit pas de fichier de restauration.                                                                                      |
| `--restore-file-path=<fichier>`        | Spécifie l'emplacement du fichier de restauration.                                                                           |
| `-o <fichier>`                         | Spécifie le fichier de sortie.                                                                                               |
| `--outfile-format=<format>`            | Format de sortie à utiliser (voir Formats de sortie).                                                                        |
| `--outfile-autohex-disable`            | Désactive le "$HEX[]" dans la sortie.                                                                                        |
| `--outfile-check-timer=<secondes>`     | Spécifie le nombre de secondes entre chaque vérification du fichier de sortie.                                               |
| `--wordlist-autohex-disable`           | Désactive la conversion de "$HEX[]" depuis le dictionnaire.                                                                  |
| `-p <séparateur>`                      | Spécifie le caractère de séparation pour la liste de hash et la sortie.                                                      |
| `--stdout`                             | Ne crack pas le hash mais affiche uniquement les candidats.                                                                  |
| `--show`                               | Compare les liste de hash avec le fichier potfile (affiche les hashs crackés auparavant)                                     |
| `--left`                               | Compare les liste de hash avec le fichier potfile (affiche les hashs non crackés auparavant)                                 |
| `--username`                           | Ignore les noms d'utilisateur dans le fichier des hash.                                                                      |
| `--remove`                             | Supprime les hashs de la liste des hash une fois qu'ils sont crackés.                                                        |
| `--remove-timer=<secondes>`            | Précise le nombre de secondes entre chaque mise à jour du fichier des hash.                                                  |
| `--potfile-disable`                    | Désactive le fichier potfile.                                                                                                |
| `--potfile-path=<fichier>`             | Précise le fichier potfile.                                                                                                  |
| `--encoding-from=<encodage>`           | Force l'encodage du dictionnaire depuis un autre encodage.                                                                   |
| `--encoding-to=<encodage>`             | Force l'encodage du dictionnaire vers un autre encodage.                                                                     |
| `--debug-mode=<niveau>`                | Précise le niveau de debug de 0 à 4. (0 par défaut)                                                                          |
| `--debug-file=<fichier>`               | Spécifie le fichier de debug pour les règles.                                                                                |
| `--induction-dir=<repertoire>`         | Précise le répertoire utilisé pour le loopback. (voir --loopback)                                                            |
| `--outfile-check-dir=<repertoire>`     | Spécifie le répertoire à surveiller pour les règles.                                                                         |
| `--logfile-disable`                    | Désactive le fichier de règles.                                                                                              |
| `--keyboard-layout-mapping=<fichier>`  | Précise le fichier de disposition du clavier pour certains modes de hash.                                                    |
| `--truecrypt-keyfiles=<fichier>`       | Fichier(s) clé à utiliser (séparés par des virgules).                                                                        |
| `--veracrypt-keyfiles=<fichier>`       | Fichier(s) clé à utiliser (séparés par des virgules).                                                                        |
| `-b`                                   | Effectue un benchmark des hash sélectionnés.                                                                                 |
| `--benchmark-all`                      | Effectue un benchmark de tous les hash.                                                                                      |
| `--speed-only`                         | Affiche l'estimation du temps de l'attaque et quitte.                                                                        |
| `--progress-only`                      | Affiche les étapes de progrès idéales et le temps de travail.                                                                |
| `-c <taille en MB>`                    | Spécifie la taille du cache du dictionnaire.                                                                                 |
| `--cpu-affinity=<coeurs cpu>`          | Précise les cœurs du processeur à utiliser (séparés par des virgules).                                                       |
| `--hook-threads=<nombre de threads>`   | Spécifie le nombre de threads pour un hook.                                                                                  |
| `--hash-info`                          | Affiche les informations pour chaque mode de hash.                                                                           |
| `--example-hashes`                     | Alias de --hash-info.                                                                                                        |
| `-I`                                   | Affiche les informations concernant le système, l'environnement et le backend.                                               |
| `-O`                                   | Active l'optimisation des kernels. (Cela limite la taille des mots de passe)                                                 |
| `-T <nombre de threads>`               | Spécifie le nombre de threads.                                                                                               |
| `--hwmon-disable>`                     | Désactive la lecture des températures et de la vitesse des ventilateurs. Ainsi que les alertes.                              |
| `--hwmon-temp-abort=<nombre>`          | Spécifie a quelle température l'opération est stoppée (En degrés Celsius).                                                   |
| `-s <nombre>`                          | Passe un nombre donné de mots depuis le début.                                                                               |
| `-l <nombre>`                          | Limite le nombre de mots à utiliser.                                                                                         |
| `-j <règle>`                           | Spécifie la règle appliquée depuis le dictionnaire de gauche.                                                                |
| `-k <règle>`                           | Spécifie la règle appliquée depuis le dictionnaire de droite.                                                                |
| `-r <fichier>`                         | Spécifie le fichier de règles.                                                                                               |
| `-g <nombre<`                          | Génere un nombre donné de règles aléatoires.                                                                                 |
| `--generate-rules-seed <nombre>`       | Précise la seed utilisée pour la génération de règles aléatoires.                                                            |
| `--identify`                           | Affiche tous les algorithmes supportés pour les hashs d'entrés                                                               |
| `-S`                                   | Active le mode avancé pour la désignation de candidats (plus lent).                                                          |
| `--brain-server`                       | Active le serveur cerveau.                                                                                                   |
| `--brain-client`                       | Active le client cerveau.                                                                                                    |
| `--brain-client-features <nombre>`     | Active des fonctionnalités du client cerveau.                                                                                |
| `--brain-host <serveur>`               | Précise l'adresse serveur hôte.                                                                                              |
| `--brain-port <port>`                  | Spécifie le port du serveur hôte.                                                                                            |
| `--brain-password <mot de passe>`      | Mot de passe du serveur hôte.                                                                                                |
| `--brain-session <session>`            | Spécifie la session (normalement définie automatiquement).                                                                   |
| `--brain-session-whitelist <sessions>` | Autorise certaines sessions uniquement.                                                                                      |

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

| ID type d'attaque | Description                         |
| ----------------- | ----------------------------------- |
| `1`               | hash:salt                           |
| `2`               | Texte en clair                      |
| `3`               | Hexadécimal en clair                |
| `4`               | Format spécifique aux mots de passe |
| `5`               | Horodatage absolu                   |
| `6`               | Horodatage relatif                  |

# Exemples

Crack le hash avec le dictionnaire rockyou.txt.
`hashcat -m 5600 admin:1003:aad3b435b51404eeaad3b435b51404ee:5835048ce94ad0564e29a924a03510ef::: /usr/share/wordlists/rockyou.txt `

Crack le hash en mode combinatoire avec le dictionnaire rockyou.txt et mydict.txt.
`hashcat -m 5600 -a 1 admin:1003:aad3b435b51404eeaad3b435b51404ee:5835048ce94ad0564e29a924a03510ef::: /usr/share/wordlists/rockyou.txt ./mydict.txt`

# Voir aussi

Documentation officielle et valeurs par défaut
https://hashcat.net/wiki/doku.php?id=hashcat

Les différents hash-mode avec exemples
https://hashcat.net/wiki/doku.php?id=example_hashes
