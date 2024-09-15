---
title: MailSniper
description: Module PowerShell qui permet d'effectuer des recherches de certains termes à travers les emails dans un environnements exchange. Permet aussi d'énumérer l'environnement exchange ainsi que les permissions.
published: true
date: 2024-09-15T14:44:03.175Z
tags: outil, windows, powershell
editor: markdown
dateCreated: 2024-09-15T14:22:51.764Z
---

# Introduction

MailSniper est un module PowerShell qui permet d'effectuer des recherches de certains termes à travers les emails dans un environnements exchange. MailSniper permet aussi d'énumérer l'environnement exchange ainsi que les permissions.

> MailSniper est disponible au téléchargement [ici](https://github.com/dafthack/MailSniper)
> {.is-info}

# Commande Invoke-GlobalMailSearch

Effectue une recherche sur toutes les boites mails d'un domaine.

## Syntaxe

`Invoke-GlobalMailSearch [paramètres]`

## Paramètres

| Paramètre                                                | Description                                                                                                                                                                                          |
| -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-ImpersonationAccount <[domaine\]utilisateur>`          | Spécifie l'utilisateur à qui accorder le privilège ApplicationImpersonation sur le serveur Exchange.                                                                                                 |
| `-ExchHostname <serveur exchange ou $AutoDiscoverEmail>` | Spécifie le serveur Exchange sur lequel se connecter. Si "$AutoDiscoverEmail" est indiqué, alors le serveur sera découvert automatiquement.                                                          |
| `-AutoDiscoverEmail <adresse email>`                     | Spécifie une adresse email valide pour la détection automatique du serveur Exchange (voir -ExchHostname)                                                                                             |
| `-MailsPerUser <nombre>`                                 | Spécifie le nombre de mails à retourner pour chaque boite mail.                                                                                                                                      |
| `-Terms <termes de recherche>`                           | Spécifie les termes à rechercher dans le sujet et le corp des mails. (par défaut: `"*password*","*creds*","*credentials*"`)                                                                          |
| `-OutputCsv <fichier>`                                   | Exporte les résultats de la recherche dans un fichier csv.                                                                                                                                           |
| `-ExchangeVersion <version>`                             | Spécifie la version du serveur Exchange sur lequel se connecter. (essai de Exchange2010 par défaut)                                                                                                  |
| `-AdminUserName <[domaine\]utilisateur>`                 | Nom de l'utilisateur administrateur Exchange avec lequel se connecter.                                                                                                                               |
| `-AdminPassword <mot de passe>`                          | Mot de passe de l'utilisateur administrateur Exchange avec lequel se connecter.                                                                                                                      |
| `-EmailList <fichier>`                                   | Fichier texte précisant quelles adresses email parcourir.                                                                                                                                            |
| `-Folder <dossier ou Inbox ou all>`                      | Spécifie dans quel dossier effectuer la recherche. "Inbox" pour la boite de réception (par défaut), "all" pour tous les dossiers récursivement. Il est possible de préciser un dossier personnalisé. |
| `-Regex <expression regex>`                              | Utilise une expression regex à la place de -Terms.                                                                                                                                                   |
| `-CheckAttachments`                                      | Essaye d'effectuer la recherche dans le contenu des pièces jointes (fichiers avec les extensions: .bat, .htm, .msg, .pdf, .txt, .ps1, .doc et .xls).                                                 |
| `-DownloadDir <répertoire>`                              | Télécharge les pièces jointes dans un répertoire.                                                                                                                                                    |

# Commande Invoke-SelfSearch

Effectue une recherche sur la boite mail de l'utilisateur actuel.

## Syntaxe

`Invoke-SelfSearch [paramètres]`

## Paramètres

| Paramètre                                                | Description                                                                                                                                                                                          |
| -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-ExchHostname <serveur exchange ou $AutoDiscoverEmail>` | Spécifie le serveur Exchange sur lequel se connecter. Si "$AutoDiscoverEmail" est indiqué, alors le serveur sera découvert automatiquement.                                                          |
| `-Mailbox <adresse mail>`                                | Adresse mail de l'utilisateur actuel (utilisateur auxquel le processus powershell apartient).                                                                                                        |
| `-MailsPerUser <nombre>`                                 | Spécifie le nombre de mails à retourner.                                                                                                                                                             |
| `-Terms <termes de recherche>`                           | Spécifie les termes à rechercher dans le sujet et le corp des mails. (par défaut: `"*password*","*creds*","*credentials*"`)                                                                          |
| `-OutputCsv <fichier>`                                   | Exporte les résultats de la recherche dans un fichier csv.                                                                                                                                           |
| `-ExchangeVersion <version>`                             | Spécifie la version du serveur Exchange sur lequel se connecter. (essai de Exchange2010 par défaut)                                                                                                  |
| `-Remote`                                                | Une demande d'authentification s'affichera pour l'accès au service EWS depuis Internet.                                                                                                              |
| `-Folder <dossier ou Inbox ou all>`                      | Spécifie dans quel dossier effectuer la recherche. "Inbox" pour la boite de réception (par défaut), "all" pour tous les dossiers récursivement. Il est possible de préciser un dossier personnalisé. |
| `-CheckAttachments`                                      | Essaye d'effectuer la recherche dans le contenu des pièces jointes (fichiers avec les extensions: .bat, .htm, .msg, .pdf, .txt, .ps1, .doc et .xls).                                                 |
| `-DownloadDir <répertoire>`                              | Télécharge les pièces jointes dans un répertoire.                                                                                                                                                    |
| `-OtherUserMailbox`                                      | Utiliser ce paramètre quand la boite mais précisé avec -Mailbox est différente de l'utilisateur auxquel le processus powershell apartient.                                                           |
| `-UsePrt`                                                | utilise le jeton jeton d’actualisation principal (PRT) de l'utilisateur.                                                                                                                             |
| `-AccessToken <token Oauth>`                             | Utilise un token d'accès Oauth pour l'authentification.                                                                                                                                              |
# Commande Invoke-GlobalO365MailSearch

Effectue une recherche sur toutes les boites mails d'un domaine, en se connectant à Office 365 et en utilisant une authentification SSO.

## Syntaxe

`Invoke-GlobalO365MailSearch [paramètres]`

## Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `...`     | ...         |

# Exemples

# Voir aussi

Présentation de MailSniper
https://www.blackhillsinfosec.com/introducing-mailsniper-a-tool-for-searching-every-users-email-for-sensitive-data/

Détails sur le jeton jeton d’actualisation principal (PRT)
https://learn.microsoft.com/fr-fr/entra/identity/devices/concept-primary-refresh-token
