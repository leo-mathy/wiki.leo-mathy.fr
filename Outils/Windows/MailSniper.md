---
title: MailSniper
description: Module PowerShell qui permet d'effectuer des recherches de certains termes à travers les emails dans un environnements exchange. Permet aussi d'énumérer l'environnement exchange ainsi que les permissions.
published: true
date: 2024-09-15T15:06:36.476Z
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
| `-UsePrt`                                                | Utilise le jeton jeton d’actualisation principal (PRT) de l'utilisateur pour l'authentification.                                                                                                     |
| `-AccessToken <token Oauth>`                             | Utilise un token d'accès Oauth pour l'authentification.                                                                                                                                              |

# Commande Invoke-GlobalO365MailSearch

Effectue une recherche sur toutes les boites mails d'un domaine, en se connectant à Office 365 et en utilisant une authentification SSO.

## Syntaxe

`Invoke-GlobalO365MailSearch [paramètres]`

## Paramètres

| Paramètre                                        | Description                                                                                                                   |
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| `-UsePrtImperonsationAccount`                    | Utilise le jeton jeton d’actualisation principal (PRT) de l'utilisateur pour s'authentifier en tant que ImperonsationAccount. |
| `-AccessTokenImpersonationAccount <token Oauth>` | Utilise un token d'accès Oauth pour s'authentifier en tant que ImperonsationAccount.                                          |
| `-UsePrtAdminAccount`                            | Utilise le jeton jeton d’actualisation principal (PRT) de l'utilisateur pour s'authentifier en tant que AdminAccount.         |
| `-AccessTokenAdminAccount <token Oauth>`         | Utilise un token d'accès Oauth pour s'authentifier en tant que AdminAccount.                                                  |

# Commande Get-GlobalAddressList

Récupère la Liste d'Adresses Globale (GAL) en utilisant l'OWA ou l'EWS (Exchange 2013 minimum).

## Syntaxe

`Get-GlobalAddressList [paramètres]`

# Commande Get-MailboxFolders

Récupère la Liste des dossiers d'une boite mail en utilisant EWS.

## Syntaxe

`Get-MailboxFolders [paramètres]`

# Commande Invoke-PasswordSprayOWA

Depuis un portail OWA, essaye de se connecter à une liste d'utilisateurs avec un seul mot de passe (Password Spraying Attack).

## Syntaxe

`Invoke-PasswordSprayOWA`

# Commande Invoke-PasswordSprayEWS

Depuis un portail EWS, essaye de se connecter à une liste d'utilisateurs avec un seul mot de passe (Password Spraying Attack).

## Syntaxe

`Invoke-PasswordSprayEWS [paramètres]`

# Commande Invoke-PasswordSprayGmail

Depuis un portail Gmail, essaye de se connecter à une liste d'utilisateurs avec un seul mot de passe (Password Spraying Attack).

## Syntaxe

`Invoke-PasswordSprayGmail`

# Commande Invoke-DomainHarvestOWA

Depuis un portail OWA, essaye de déterminer un nom de domaine valide pour se connecter au portail (en utilisant le header WWW-Authenticate ou en se basant sur des différences de temps entre chaque tentative).

## Syntaxe

`Invoke-DomainHarvestOWA`

# Commande Invoke-UsernameHarvestOWA

Depuis un portail OWA, essaye de déterminer un nom d'utilisateur valide pour se connecter au portail (en se basant sur des différences de temps entre chaque tentative).

## Syntaxe

`Invoke-UsernameHarvestOWA`

# Commande Invoke-UsernameHarvestGmail

Essaye d'énumérer les comptes Google et potentiellement identifier les comptes qui n'utilisent pas de solution d'authentification à deux facteurs (2FA).

## Syntaxe

`Invoke-UsernameHarvestGmail`

# Commande Invoke-OpenInboxFinder

Essaye de déterminer si l'utilisateur actuel à accès à des boites mail contenues une liste.

## Syntaxe

`Invoke-OpenInboxFinder`

# Commande Get-ADUsernameFromEWS

Essaye de trouver les utilisateur Active Directory à qui est attribué l'adresse mail dans une liste.

## Syntaxe

`Get-ADUsernameFromEWS`


# Voir aussi

Présentation de MailSniper
https://www.blackhillsinfosec.com/introducing-mailsniper-a-tool-for-searching-every-users-email-for-sensitive-data/

Détails sur le jeton jeton d’actualisation principal (PRT)
https://learn.microsoft.com/fr-fr/entra/identity/devices/concept-primary-refresh-token
