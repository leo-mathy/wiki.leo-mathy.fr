---
title: SharpDPAPI
description: Portage de certaines fonctionnalités DPAPI de mimikatz en C#. Contient aussi le sous projet SharpChrome (permet le déchiffrement avec DPAPI des logins et cookies).
published: true
date: 2024-09-14T12:23:46.542Z
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

`SharpDPAPI <commande> [paramètres]`

## Commandes

| Commande             | Description                                                                                                                                                                                                                                                                                                                       |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `backupkey`          | Permet de récupérer la clé de sauvegarde DPAPI d'un contrôleur de domaine. (Cette clé permet de dechiffrer toutes les clés maîtres des utilisateurs du domaine).                                                                                                                                                                                                                                                          |
| `search`             | Permet rechercher des blobs DPAPI (blocs de données chiffrés) dans le registre, fichiers, dossiers ou blobs en base64.                                                                                                                                                                                                          |
| `machinemasterkeys`  | Récupère le secret LSA "DPAPI_SYSTEM" après s'être elevé en tant que SYSTEM, et l'utilise pour déchiffrer les clés secrètes DPAPI (DPAPI masterkeys) trouvées sur la machine. Une fois les clés secrètes DPAPI déchiffrés, elles sont retournées au format "{GUID}:SHA1".                                             |
| `machinecredentials` | Récupère le secret LSA "DPAPI_SYSTEM" après s'être elevé en tant que SYSTEM, et l'utilise pour déchiffrer les clés secrètes DPAPI (DPAPI masterkeys) trouvées sur la machine. Une fois les clés secrètes DPAPI déchiffrés, elles sont utilisés pour déchiffrer les informations d'identifications trouvées sur la machine. |
| `machinevaults`      | Récupère le secret LSA "DPAPI_SYSTEM" après s'être elevé en tant que SYSTEM, et l'utilise pour déchiffrer les clés secrètes DPAPI (DPAPI masterkeys) trouvées sur la machine. Une fois les clés secrètes DPAPI déchiffrés, elles sont utilisés pour déchiffrer les coffres trouvées sur la machine.                            |
| `machinetriage`      | Exécute les commandes "machinecredentials", "machinevaults" et "certificates /machine".                                                                                                                                                                                                                                           |
| `masterkeys`         | Recherche des fichiers clés secrètes DPAPI utilisateur (DPAPI user masterkeys) et les déchiffre avec la clé de sauvegarde DPAPI d'un contrôleur de domaine.                                                                                                                                                                                  |
| `credentials`        | Recherche des fichiers d'information d'identification et les déchiffre.                                                                                                                                                                                                                                                           |
| `vaults`             | Recherche des fichiers coffre-fort et les déchiffre.                                                                                                                                                                                                                                                                              |
| `rdg`                | Recherche des fichiers "RDCMan.settings" et les déchiffre.                                                                                                                                                                                                                                                                        |
| `keepass`            | Recherche des fichiers "ProtectedUserKey.bin" et les déchiffre.                                                                                                                                                                                                                                                                   |
| `triage`             | Lance les commandes credentials, vaults, rdg et certificates.                                                                                                                                                                                                                                                                     |
| `blob`               | Effectue une description et déchiffrement du blob DPAPI indiqué.                                                                                                                                                                                                                                                                  |
| `rdg`                | Déchiffre des fichiers "PSCredential clixml" .                                                                                                                                                                                                                                                                                    |
| `certificates`       | Déchiffre des clés privées de certificats.                                                                                                                                                                                                                                                                                        |

### Paramètres de la commande backupkey

| Paramètre                     | Description                                        |
| ----------------------------- | -------------------------------------------------- |
| `/nowrap`                     | Désactive le formatage de sortie.                  |
| `/server:<serveur>.<domaine>` | Spécifie le contrôleur de domaine.                 |
| `/file:<clé.pvk>`             | Exporte la clé de sauvegarde DPAPI au format .pvk. |

### Paramètres de la commande search

| Paramètre                             | Description                                                                             |
| ------------------------------------- | --------------------------------------------------------------------------------------- |
| `/type:<registry/folder/file/base64>` | Spécifie quel type d'élément rechercher.                                                |
| `/path:<chemin>`                      | Spécifie le chemin vers une clé, un dossier ou un fichier.                              |
| `/showErrors`                         | Affiche les erreurs durant l'énumération pour les recherches de type registre ou dossier.                    |
| `/maxBytes:<taille en bytes>`         | Précise le nombre de bytes à lire pour chaque fichier (1024 par défaut) |
| `/base:<chaine base64>`               | Spécifie la chaine base64 lors d'une recherche de type base64.                          |

### Paramètres de la commande masterkeys

| Paramètre                                        | Description                                                                                         |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| `/target:<fichier/dossier>`                      | Spécifie un fichier ou un dossier contenant des clés maître de l'utilisateur.                       |
| `/pvk:<chaîne base64/fichier clé au format pvk>` | Utilise la clé privée DPAPI pour déchifrer les clés maîtres de l'utilisateur.                       |
| `/password:<mot de passse>`                      | Utilise le mot de passe en clair de l'utilisateur pour déchifrer les clés maîtres de l'utilisateur. |
| `/ntlm:<hash NTLM>`                              | Utilise le hash NTLM de l'utilisateur pour déchifrer les clés maîtres de l'utilisateur.             |
| `/credkey:<clé DPAPI>`                           | Utilise une clé DPAPI pour déchifrer les clés maîtres de l'utilisateur.                             |
| `/rpc`                                           | Demande au controleur de domaine de déchifrer les clés maîtres de l'utilisateur.                    |
| `/server:<serveur>`                              | Spécifie le serveur.                                                                                |
| `/hashes`                                        | Ne déchiffre pas mais affiche les hashs des fichiers clés maîtres de l'utilisateur.                 |

### Paramètres des commandes credentials, vaults, rdg, keepass, triage, blob et ps

| Paramètre                                        | Description                                                                                         |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| `/unprotect`                                     | Force l'usage de la fonction CryptUnprotectData().                                                  |
| `/pvk:<chaîne base64/fichier clé au format pvk>` | Utilise la clé privée DPAPI pour déchifrer les clés maîtres de l'utilisateur.                       |
| `/password:<mot de passse>`                      | Utilise le mot de passe en clair de l'utilisateur pour déchifrer les clés maîtres de l'utilisateur. |
| `/credkey:<clé DPAPI>`                           | Utilise une clé DPAPI pour déchifrer les clés maîtres de l'utilisateur.                             |
| `/rpc`                                           | Demande au controleur de domaine de déchifrer les clés maîtres de l'utilisateur.                    |
| `/server:<serveur>`                              | Spécifie le serveur.                                                                                |
| `/target:<fichier/dossier>`                      | Spécifie un fichier ou un dossier contenant des clés maître de l'utilisateur.                       |

### Paramètres de la commande certificates

| Paramètre  | Description                                                                               |
| ---------- | ----------------------------------------------------------------------------------------- |
| `/showall` | Affiche touts les fichiers de clés privées, même si ils ne sont pas liés à un certificat. |
| `/machine` | Utilise le magasin de certificats local pour la recherche.                                |
| `/mkfile`  | Utilisé avec /machine                                                                     |

# SharpChrome

## Syntaxe

`SharpChrome <commande> [paramètres]`

## Commandes

# Voir aussi

Détails sur DPAPI
https://blog.harmj0y.net/redteaming/operational-guidance-for-offensive-user-dpapi-abuse/

Clés de sauvegarde DPAPI sur les contrôleurs de domaine Active Directory
https://learn.microsoft.com/en-us/windows/win32/seccng/cng-dpapi-backup-keys-on-ad-domain-controllers
