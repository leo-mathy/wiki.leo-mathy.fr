---
title: Invoke-WebRequest
description: Effectue une requête vers un page web.
published: true
date: 2024-10-25T19:34:05.609Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-10-25T19:34:05.609Z
---

# Introduction

Invoke-WebRequest est une applet PowerShell, alias de IWR, qui permet d'effectuer une requête vers un page web.

# Syntaxe

`Invoke-WebRequest [URI/body] [paramètres]`

# Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `-AllowInsecureRedirect`     | Autorise la redirection vers HTTP depuis une page HTTPS.         |
| `-AllowUnencryptedAuthentication`     | Autorise l'envoi d'identifiants et de mots de passe vers une page HTTP.         |
| `-Authentication <None;Basic;Bearer;OAuth>`     | Spécifie la méthode d'authentification à la page web.         |
| `-Body <body>`     | Spécifie le corp de la requète.         |
| `-Certificate <commande/objet certificat>`     | Spécifie le certificat à utiliser.         |
| `-CertificateThumbprint <empreinte>`     | Spécifie l'empreinte du certificat autorisé, à utiliser pour la requète.       |
| `-ConnectionTimeoutSeconds <secondes>`     | Spécifie la durée du timeout. 0 pour infini. Par défaut la valeur est 0.         |
| `-ContentType <type>`     | Spécifie l'encodage du body.         |
| `-Credential <utilisateur/objet Credential>`     | Spécifie un utilisateur pour l'envoi des requètes.         |
| `-CustomMethod <méthode>`     | Précise la méthode à utiliser comme requète. Utile si le serveur prend en charge des méthodes personnalisées.        |
| `-DisableKeepAlive`     | Désactive le paramètre KeepAlive dans le header lors de la requète. Le KeepAlive est utilisé pour réduire le temps des prochaines requètes.         |
| `-Form <dictionnaire>`     | Utilise un dictionnaire pour l'intéraction avec les formulaires.         |
| `-Headers <header>`     | Spécifie le header à utiliser lors de la requète.         |
| `-HttpVersion <version HTTP>`     | Spécifie la version HTTP lors de la requète. 1.1 par défaut.         |
| `-InFile [chemin]\<fichier>`     | Spécifie la requète depuis un fichier.      |
| `-MaximumRedirection <nombre>`     | Précise le nombre de redirections maximales vers d'autres URI. 5 par défaut. Une valeure de 0 empèche toute redirection.         |
| `-MaximumRetryCount <nombre>`     | Spécifie le nombre de tentatives lorsqu'un code 400,599,inclusive ou 304 est reçu.         |
| `-Method <Default;Delete;Get;Head;Merge;Options;Patch;Post;Put;Trace>`     | Spécifie la méthode de la requète.         |
| `-AllowInsecureRedirect`     | Autorise la redirection vers HTTP depuis une page HTTPS.         |
| `-AllowInsecureRedirect`     | Autorise la redirection vers HTTP depuis une page HTTPS.         |
| `-AllowInsecureRedirect`     | Autorise la redirection vers HTTP depuis une page HTTPS.         |
| `-AllowInsecureRedirect`     | Autorise la redirection vers HTTP depuis une page HTTPS.         |

# Exemples

# Voir aussi
