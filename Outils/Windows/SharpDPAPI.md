---
title: SharpDPAPI
description: Portage de certaines fonctionnalités DPAPI de mimikatz en C#. Contient aussi le sous projet SharpChrome (permet le déchiffrement avec DPAPI des logins et cookies).
published: true
date: 2024-09-14T07:57:02.726Z
tags: outil, windows, rédaction incomplète
editor: markdown
dateCreated: 2024-09-12T08:51:59.511Z
---

# Introduction

Portage de certaines fonctionnalités DPAPI de mimikatz en C#. Contient aussi le sous projet SharpChrome (permet le déchiffrement avec DPAPI des logins et cookies).

> SharpDPAPI et SharpChrome sont disponible au téléchargement [ici](https://github.com/GhostPack/SharpDPAPI)
> {.is-info}

# SharpDPAPI

## Syntaxe

`SharpDPAPI <module|triage> [paramètres]`

### Paramètres du module backupkey

Le module backupkey permet de récupérer la clé de sauvegarde DPAPI d'un contrôleur de domaine.

| Paramètre                     | Description                                        |
| ----------------------------- | -------------------------------------------------- |
| `/nowrap`                     | Désactive le formatage de sortie.                  |
| `/server:<serveur>.<domaine>` | Spécifie le contrôleur de domaine.                 |
| `/file:<clé.pvk>`             | Exporte la clé de sauvegarde DPAPI au format .pvk. |

### Paramètres du module search

Le module search permet rechercher des blobs DPAPI (blocs de données chiffrées) dans le registre, fichiers, dossiers ou blobs en base64.

| Paramètre                     | Description                                                                             |
| ----------------------------- | --------------------------------------------------------------------------------------- | ---- | -------- | ---------------------------------------- |
| `/type:<registry              | folder                                                                                  | file | base64>` | Spécifie quel type d'élément  rechercher. |
| `/path:<chemin>`              | Spécifie le chemin vers une clé, un dossier ou un fichier.                              |
| `/showErrors`                 | Affiche les erreurs pour les recherches de type registre ou dossier.                    |
| `/maxBytes:<taille en bytes>` | Précise la taille maximum d'un fichier lors d'une recherche de type dossier ou fichier. |
| `/base:<chaine base64>`       | Spécifie la chaine base64 lors d'une recherche de type base64.                          |

### Types de triage

Comme énoncé dans la syntaxe, il est possible de choisir le triage, pour récupérer des informations chiffrées.

| Paramètre            | Description                                                                                                                                                                                                                                                                                                               |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `machinemasterkeys`  | Récupère la clé "DPAPI_SYSTEM LSA" et l'utilise pour déchiffrer les clés DPAPI maîtres (DPAPI masterkeys) présentes sur la machine, les clés maîtres sont retournées au format "{GUID}:SHA1". (des droits administrateurs sont requis pour récupérer la clé "DPAPI_SYSTEM LSA").                                           |
| `machinecredentials` | Récupère la clé "DPAPI_SYSTEM LSA" et l'utilise pour déchiffrer les clés DPAPI maîtres (DPAPI masterkeys) présentes sur la machine, ces clés sont ensuite utilisées pour déchiffrer tous les fichiers d'informations d'identification trouvés. (des droits administrateurs sont requis pour récupérer la clé "DPAPI_SYSTEM LSA"). |
| `machinevaults` | Récupère la clé "DPAPI_SYSTEM LSA" et l'utilise pour déchiffrer les clés DPAPI maîtres (DPAPI masterkeys) présentes sur la machine, ces clés sont ensuite utilisées pour déchiffrer tous les coffres-forts trouvés. (des droits administrateurs sont requis pour récupérer la clé "DPAPI_SYSTEM LSA"). |
| `machinetriage` | Exécute les commandes "machinecredentials", "machinevaults" et "certificates /machine".  |

# Voir aussi

Détails sur DPAPI
https://blog.harmj0y.net/redteaming/operational-guidance-for-offensive-user-dpapi-abuse/
