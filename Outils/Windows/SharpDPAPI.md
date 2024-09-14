---
title: SharpDPAPI
description: Portage de certaines fonctionnalités DPAPI de mimikatz en C#. Contient aussi le sous projet SharpChrome (permet le déchiffrement avec DPAPI des logins et cookies).
published: true
date: 2024-09-14T12:58:41.848Z
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
| `masterkeys`         | Recherche des fichiers clés secrètes DPAPI utilisateur (DPAPI user masterkeys) et les déchiffre.                                                                                                                                                                                  |
| `credentials`        | Recherche des fichiers d'informations d'identification (credential files) et les déchiffre.                                                                                                                                                                                                                                                          |
| `vaults`             | Recherche des coffres (Vaults) et les déchiffre.                                                                                                                                                                                                                                                                              |
| `rdg`                | Recherche des fichiers "RDCMan.settings" (fichiers contenant les identifiants pour les connexions ave RDCMan) et les déchiffre. (utilisateur actif uniquement, si l'opération se déroule sans elévation)                                                                                                                                                                                                                                                                        |
| `keepass`            | Recherche des fichiers "ProtectedUserKey.bin" et les déchiffre.                                                                                                                                                                                                                                                                   |
| `triage`             | Lance les commandes credentials, vaults, rdg et certificates.                                                                                                                                                                                                                                                                     |
| `blob`               | Effectue une description et un déchiffrement du blob DPAPI indiqué (Les blobs sont souvent dans des fichiers ou seulement quelques informations sont chiffrées).                                                                                                                                                                                                                                                             |
| `ps`                | Effectue une description et un déchiffrement du fichier "PSCredential clixml" indiqué (voir Export-Clixml).                                                                                                                                                                                                                                                                                    |
| `certificates`       | Recherche des certificats contenant des clés privées chiffrées avec DPAPI et les déchiffre.                                                                                                                                                                                                                                                                                        |

### Paramètres de la commande backupkey

| Paramètre                     | Description                                        |
| ----------------------------- | -------------------------------------------------- |
| `/nowrap`                     | Désactive le formatage de sortie pour la clé au format base64.                 |
| `/server:<serveur>.<domaine>` | Spécifie le contrôleur de domaine sur lequel récupérer la clé.                 |
| `/file:<clé.pvk>`             | Exporte la clé de sauvegarde DPAPI d'un contrôleur de domaine au format pvk. |

### Paramètres de la commande search

| Paramètre                             | Description                                                                             |
| ------------------------------------- | --------------------------------------------------------------------------------------- |
| `/type:<registry/folder/file/base64>` | Spécifie quel type d'élément rechercher (registre par défaut).                                                |
| `/path:<chemin>`                      | Spécifie le chemin vers une clé, un dossier ou un fichier.                              |
| `/showErrors`                         | Affiche les erreurs durant l'énumération pour les recherches de type registre ou dossier.                    |
| `/maxBytes:<taille en bytes>`         | Précise le nombre de bytes à lire pour chaque fichier (1024 par défaut) |
| `/base:<chaine base64>`               | Spécifie la chaine base64 lors d'une recherche de type base64.                          |

### Paramètres de la commande masterkeys

| Paramètre                                        | Description                                                                                         |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| `/target:<fichier/dossier>`                      | Spécifie un fichier ou un dossier contenant des clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                      |
| `/pvk:<chaîne base64/fichier clé au format pvk>` | Utilise la clé de sauvegarde DPAPI d'un contrôleur de domaine pour déchifrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                      |
| `/password:<mot de passse>`                      | Utilise le mot de passe en clair de l'utilisateur pour déchifrer les clés secrètes DPAPI utilisateur. |
| `/ntlm:<hash NTLM>`                              | Utilise le hash NTLM de l'utilisateur pour déchifrer les clés secrètes DPAPI utilisateur.             |
| `/credkey:<clé DPAPI>`                           | Utilise une clé DPAPI (du domaine ou locale) pour déchifrer les clés secrètes DPAPI utilisateur.                             |
| `/rpc`                                           | Demande au controleur de domaine de déchifrer les clés secrètes DPAPI utilisateur.                   |
| `/server:<serveur>`                              | Spécifie le serveur.                                                                                |
| `/hashes`                                        | Ne déchiffre pas mais affiche les hashs des fichiers clés secrètes DPAPI utilisateur.                 |

### Paramètres des commandes credentials, vaults, rdg, keepass, triage, blob et ps

| Paramètre                                        | Description                                                                                         |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| `/unprotect`                                     | Force l'usage de la fonction CryptUnprotectData() sur le fichier (modifie le fichier). (utilisable avec ps, rdg et blob)                                                  |
| `/pvk:<chaîne base64/fichier clé au format pvk>` |  Utilise la clé de sauvegarde DPAPI d'un contrôleur de domaine pour déchifrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                        |
| `/password:<mot de passse>`                      | Utilise le mot de passe en clair de l'utilisateur pour déchifrer les clés secrètes DPAPI utilisateur. |
| `/ntlm:<hash NTLM>`                              | Utilise le hash NTLM de l'utilisateur pour déchifrer les clés secrètes DPAPI utilisateur.             |
| `/credkey:<clé DPAPI>`                           | Utilise une clé DPAPI (du domaine ou locale) pour déchifrer les clés secrètes DPAPI utilisateur.                             |
| `/rpc`                                           | Demande au controleur de domaine de déchifrer les clés secrètes DPAPI utilisateur.                    |
| `<GUID>:<SHA1>`                      |  Utilise la clé de sauvegarde DPAPI au format GUID:SHA1 d'un contrôleur de domaine pour déchifrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                      |
| `/mkfile:<fichier>`                      | Utilise la/les clé(s) de sauvegarde DPAPI au format GUID:SHA1 d'un contrôleur de domaine contenues dans un fichier pour déchifrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                       |
| `/target:<fichier/dossier>`                      | Spécifie un fichier ou un dossier contenant des clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                       |
| `/server:<serveur>`                              | Spécifie le serveur.                                                                                |

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
