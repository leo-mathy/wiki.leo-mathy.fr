---
title: SharpDPAPI
description: Portage de certaines fonctionnalités DPAPI de mimikatz en C#. Contient aussi le sous projet SharpChrome (permet le déchiffrement avec DPAPI des logins et cookies).
published: true
date: 2024-09-14T13:37:41.063Z
tags: outil, windows
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

| Commande             | Description                                                                                                                                                                                                                                                                                                                |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `backupkey`          | Permet de récupérer la clé de sauvegarde DPAPI d'un contrôleur de domaine. (Cette clé permet de déchiffrer toutes les clés secrètes DPAPI utilisateur du domaine).                                                                                                                                                         |
| `search`             | Permet rechercher des blobs DPAPI (blocs de données chiffrés) dans le registre, fichiers, dossiers ou blobs en base64.                                                                                                                                                                                                     |
| `machinemasterkeys`  | Récupère le secret LSA "DPAPI_SYSTEM" après s'être élevé en tant que SYSTEM, et l'utilise pour déchiffrer les clés secrètes DPAPI (DPAPI masterkeys) trouvées sur la machine. Une fois les clés secrètes DPAPI déchiffrés, elles sont retournées au format "{GUID}:SHA1".                                                  |
| `machinecredentials` | Récupère le secret LSA "DPAPI_SYSTEM" après s'être élevé en tant que SYSTEM, et l'utilise pour déchiffrer les clés secrètes DPAPI (DPAPI masterkeys) trouvées sur la machine. Une fois les clés secrètes DPAPI déchiffrés, elles sont utilisés pour déchiffrer les informations d'identifications trouvées sur la machine. |
| `machinevaults`      | Récupère le secret LSA "DPAPI_SYSTEM" après s'être élevé en tant que SYSTEM, et l'utilise pour déchiffrer les clés secrètes DPAPI (DPAPI masterkeys) trouvées sur la machine. Une fois les clés secrètes DPAPI déchiffrés, elles sont utilisés pour déchiffrer les coffres trouvées sur la machine.                        |
| `machinetriage`      | Exécute les commandes "machinecredentials", "machinevaults" et "certificates /machine".                                                                                                                                                                                                                                    |
| `masterkeys`         | Recherche des fichiers clés secrètes DPAPI utilisateur (DPAPI user masterkeys) et les déchiffre.                                                                                                                                                                                                                           |
| `credentials`        | Recherche des fichiers d'informations d'identification (credential files) et les déchiffre.                                                                                                                                                                                                                                |
| `vaults`             | Recherche des coffres (Vaults) et les déchiffre.                                                                                                                                                                                                                                                                           |
| `rdg`                | Recherche des fichiers "RDCMan.settings" (fichiers contenant les identifiants pour les connexions ave RDCMan) et les déchiffre. (utilisateur actif uniquement, si l'opération se déroule sans élévation)                                                                                                                   |
| `keepass`            | Recherche des fichiers "ProtectedUserKey.bin" et les déchiffre.                                                                                                                                                                                                                                                            |
| `triage`             | Lance les commandes credentials, vaults, rdg et certificates.                                                                                                                                                                                                                                                              |
| `blob`               | Effectue une description et un déchiffrement du blob DPAPI indiqué (Les blobs sont souvent dans des fichiers ou seulement quelques informations sont chiffrées).                                                                                                                                                           |
| `ps`                 | Effectue une description et un déchiffrement du fichier "PSCredential clixml" indiqué (voir Export-Clixml).                                                                                                                                                                                                                |
| `certificates`       | Recherche des certificats contenant des clés privées chiffrées avec DPAPI et les déchiffre.                                                                                                                                                                                                                                |

### Paramètres de la commande backupkey

| Paramètre                     | Description                                                                  |
| ----------------------------- | ---------------------------------------------------------------------------- |
| `/nowrap`                     | Désactive le formatage de sortie pour la clé au format base64.               |
| `/server:<serveur>.<domaine>` | Spécifie le contrôleur de domaine sur lequel récupérer la clé.               |
| `/file:<clé.pvk>`             | Exporte la clé de sauvegarde DPAPI d'un contrôleur de domaine au format pvk. |

### Paramètres de la commande search

| Paramètre                             | Description                                                                               |
| ------------------------------------- | ----------------------------------------------------------------------------------------- |
| `/type:<registry/folder/file/base64>` | Spécifie quel type d'élément rechercher (registre par défaut).                            |
| `/path:<chemin>`                      | Spécifie le chemin vers une clé, un dossier ou un fichier.                                |
| `/showErrors`                         | Affiche les erreurs durant l'énumération pour les recherches de type registre ou dossier. |
| `/maxBytes:<taille en bytes>`         | Précise le nombre de bytes à lire pour chaque fichier (1024 par défaut)                   |
| `/base:<chaine base64>`               | Spécifie la chaine base64 lors d'une recherche de type base64.                            |

### Paramètres de la commande masterkeys

| Paramètre                                        | Description                                                                                                                                |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `/target:<fichier/dossier>`                      | Spécifie un fichier ou un dossier contenant des clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                                   |
| `/pvk:<chaîne base64/fichier clé au format pvk>` | Utilise la clé de sauvegarde DPAPI d'un contrôleur de domaine pour déchiffrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys). |
| `/password:<mot de passse>`                      | Utilise le mot de passe en clair de l'utilisateur pour déchiffrer les clés secrètes DPAPI utilisateur.                                     |
| `/ntlm:<hash NTLM>`                              | Utilise le hash NTLM de l'utilisateur pour déchiffrer les clés secrètes DPAPI utilisateur.                                                 |
| `/credkey:<clé DPAPI>`                           | Utilise une clé DPAPI (du domaine ou locale) pour déchiffrer les clés secrètes DPAPI utilisateur.                                          |
| `/rpc`                                           | Demande au contrôleur de domaine de déchiffrer les clés secrètes DPAPI utilisateur.                                                        |
| `/server:<serveur>`                              | Spécifie le serveur.                                                                                                                       |
| `/hashes`                                        | Ne déchiffre pas mais affiche les hashs des fichiers clés secrètes DPAPI utilisateur.                                                      |

### Paramètres des commandes credentials, vaults, rdg, keepass, triage, blob et ps

| Paramètre                                        | Description                                                                                                                                                                                     |
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/unprotect`                                     | Force l'usage de la fonction CryptUnprotectData() sur le fichier (modifie le fichier). (utilisable avec ps, rdg et blob)                                                                        |
| `/pvk:<chaîne base64/fichier clé au format pvk>` | Utilise la clé de sauvegarde DPAPI d'un contrôleur de domaine pour déchiffrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                                                      |
| `/password:<mot de passse>`                      | Utilise le mot de passe en clair de l'utilisateur pour déchiffrer les clés secrètes DPAPI utilisateur.                                                                                          |
| `/ntlm:<hash NTLM>`                              | Utilise le hash NTLM de l'utilisateur pour déchiffrer les clés secrètes DPAPI utilisateur.                                                                                                      |
| `/credkey:<clé DPAPI>`                           | Utilise une clé DPAPI (du domaine ou locale) pour déchiffrer les clés secrètes DPAPI utilisateur.                                                                                               |
| `/rpc`                                           | Demande au contrôleur de domaine de déchiffrer les clés secrètes DPAPI utilisateur.                                                                                                             |
| `<GUID>:<SHA1>`                                  | Utilise la clé de sauvegarde DPAPI au format GUID:SHA1 d'un contrôleur de domaine pour déchiffrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                                  |
| `/mkfile:<fichier>`                              | Utilise la/les clé(s) de sauvegarde DPAPI au format GUID:SHA1 d'un contrôleur de domaine contenues dans un fichier pour déchiffrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys). |
| `/target:<fichier/dossier>`                      | Spécifie un fichier ou un dossier contenant des clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                                                                                        |
| `/server:<serveur>`                              | Spécifie le serveur.                                                                                                                                                                            |

### Paramètres de la commande certificates

| Paramètre           | Description                                                                                                                                                                          |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/showall`          | Affiche touts les fichiers certificats contenant des clés privées chiffrées avec DPAPI, même si le certificat n'est pas installé.                                                    |
| `/machine`          | Recherche des certificats contenant des clés privées chiffrées avec DPAPI et les déchiffre.                                                                                          |
| `/mkfile:<fichier>` | Utilise la/les clé(s) de sauvegarde DPAPI au format GUID:SHA1 d'un contrôleur de domaine contenues dans un fichier pour déchiffrer clés privées de certificats chiffrées avec DPAPI. |

# SharpChrome

## Syntaxe

`SharpChrome <commande> [paramètres]`

## Commandes

| Commande    | Description                                                                                                                                                      |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `backupkey` | Permet de récupérer la clé de sauvegarde DPAPI d'un contrôleur de domaine. (Cette clé permet de déchiffrer toutes les clés maîtres des utilisateurs du domaine). |
| `cookies`   | Spécifie le chemin vers une clé, un dossier ou un fichier.                                                                                                       |
| `logins`    | Affiche les erreurs durant l'énumération pour les recherches de type registre ou dossier.                                                                        |
| `statekeys` | Recherche les applications basées sur Chromium, cherche l'emplacement des fichiers AES statekey et les déchiffre.                                                |

### Paramètres de la commande backupkey

| Paramètre                     | Description                                                                  |
| ----------------------------- | ---------------------------------------------------------------------------- |
| `/nowrap`                     | Désactive le formatage de sortie pour la clé au format base64.               |
| `/server:<serveur>.<domaine>` | Spécifie le contrôleur de domaine sur lequel récupérer la clé.               |
| `/file:<clé.pvk>`             | Exporte la clé de sauvegarde DPAPI d'un contrôleur de domaine au format pvk. |

### Paramètres des commandes cookies, logins et statekeys

| Paramètre                                        | Description                                                                                                                                                    |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/unprotect`                                     | Force l'usage de la fonction CryptUnprotectData() sur le fichier (modifie le fichier). (utilisable avec ps, rdg et blob)                                       |
| `/pvk:<chaîne base64/fichier clé au format pvk>` | Utilise la clé de sauvegarde DPAPI d'un contrôleur de domaine pour déchiffrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys).                     |
| `/password:<mot de passse>`                      | Utilise le mot de passe en clair de l'utilisateur pour déchiffrer les clés secrètes DPAPI utilisateur.                                                         |
| `/ntlm:<hash NTLM>`                              | Utilise le hash NTLM de l'utilisateur pour déchiffrer les clés secrètes DPAPI utilisateur.                                                                     |
| `/prekey:<clé DPAPI>`                            | Utilise une clé DPAPI (du domaine ou locale) pour déchiffrer les clés secrètes DPAPI utilisateur.                                                              |
| `/rpc`                                           | Demande au contrôleur de domaine de déchiffrer les clés secrètes DPAPI utilisateur.                                                                            |
| `<GUID>:<SHA1>`                                  | Utilise la clé de sauvegarde DPAPI au format GUID:SHA1 d'un contrôleur de domaine pour déchiffrer les clés secrètes DPAPI utilisateur (DPAPI user masterkeys). |
| `/statekey:<fichier statekey> `                  | Spécifie le fichier statekey (obtenu depuis la commande statekey).                                                                                             |
| `/target:<fichier/dossier>`                      | Spécifie l'emplacement du fichier (fichiers Cookies, Login Data ou Local State) ou d'un répertoire utilisateur.                                                |
| `/browser:<chrome/edge/slack>`                   | Précise le navigateur.                                                                                                                                         |
| `/format:<csv/table>`                            | Défini le format de sortie (par défaut csv).                                                                                                                   |
| `/showall`                                       | Affiche les entrées avec des mots de passe vide et des cookies expirés à la place de les filtrer (par défaut).                                                 |
| `/consoleoutfile:<fichier>`                      | Précise le fichier de sortie.                                                                                                                                  |

### Paramètres de la commande cookies

| Paramètre           | Description                                                                                     |
| ------------------- | ----------------------------------------------------------------------------------------------- |
| `/cookie:"<regex>"` | Affiche uniquement les cookies où le nom correspond au regex.                                   |
| `/url:"<regex>" `   | Affiche uniquement les cookies où l'url correspond au regex.                                    |
| `/format:json`      | Exporte les valeurs des cookies au format json EditThisCookie.                                  |
| `/setneverexpire`   | Défini la date d'expiration des cookies en sortie pour dans 100ans. (Uniquement pour la sortie) |

# Voir aussi

Détails sur DPAPI
https://blog.harmj0y.net/redteaming/operational-guidance-for-offensive-user-dpapi-abuse/

Clés de sauvegarde DPAPI sur les contrôleurs de domaine Active Directory
https://learn.microsoft.com/en-us/windows/win32/seccng/cng-dpapi-backup-keys-on-ad-domain-controllers
