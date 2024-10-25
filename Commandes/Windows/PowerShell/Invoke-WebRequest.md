---
title: Invoke-WebRequest
description: Effectue une requête vers un page web.
published: true
date: 2024-10-25T20:33:39.048Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-10-25T19:34:05.609Z
---

# Introduction

Invoke-WebRequest est une applet PowerShell, alias de IWR, qui permet d'effectuer une requête vers un page web.

# Syntaxe

`Invoke-WebRequest [URI/body] [paramètres]`

# Paramètres

| Paramètre                                                              | Description                                                                                                                                                               |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-AllowInsecureRedirect`                                               | Autorise la redirection vers HTTP depuis une page HTTPS.                                                                                                                  |
| `-AllowUnencryptedAuthentication`                                      | Autorise l'envoi d'identifiants et de mots de passe vers une page HTTP.                                                                                                   |
| `-Authentication <None;Basic;Bearer;OAuth>`                            | Spécifie la méthode d'authentification à la page web.                                                                                                                     |
| `-Body <body>`                                                         | Spécifie le corp de la requête.                                                                                                                                           |
| `-Certificate <commande/objet certificat>`                             | Spécifie le certificat à utiliser.                                                                                                                                        |
| `-CertificateThumbprint <empreinte>`                                   | Spécifie l'empreinte du certificat autorisé, à utiliser pour la requête.                                                                                                  |
| `-ConnectionTimeoutSeconds <secondes>`                                 | Spécifie la durée du timeout. 0 pour infini. Par défaut la valeur est 0.                                                                                                  |
| `-ContentType <type>`                                                  | Spécifie l'encodage du body.                                                                                                                                              |
| `-Credential <utilisateur/objet Credential>`                           | Spécifie un utilisateur pour l'envoi des requêtes.                                                                                                                        |
| `-CustomMethod <méthode>`                                              | Précise la méthode à utiliser comme requête. Utile si le serveur prend en charge des méthodes personnalisées.                                                             |
| `-DisableKeepAlive`                                                    | Désactive le paramètre KeepAlive dans le header lors de la requête. Le KeepAlive est utilisé pour réduire le temps des prochaines requête.                                |
| `-Form <dictionnaire>`                                                 | Utilise un dictionnaire pour l'interaction avec les formulaires.                                                                                                          |
| `-Headers <header>`                                                    | Spécifie le header à utiliser lors de la requête.                                                                                                                         |
| `-HttpVersion <version HTTP>`                                          | Spécifie la version HTTP lors de la requête. 1.1 par défaut.                                                                                                              |
| `-InFile [chemin]\<fichier>`                                           | Spécifie la requête depuis un fichier.                                                                                                                                    |
| `-MaximumRedirection <nombre>`                                         | Précise le nombre de redirections maximales vers d'autres URI. 5 par défaut. Une valeur de 0 empêche toute redirection.                                                   |
| `-MaximumRetryCount <nombre>`                                          | Spécifie le nombre de tentatives lorsqu'un code 400,599,inclusive ou 304 est reçu.                                                                                        |
| `-Method <Default;Delete;Get;Head;Merge;Options;Patch;Post;Put;Trace>` | Spécifie la méthode de la requête.                                                                                                                                        |
| `-NoProxy`                                                             | N'utilise pas le proxy spécifie dans le système.                                                                                                                          |
| `-OperationTimeoutSeconds <secondes>`                                  | Précise après quelle durée la requête est annulée si aucune donnée d'un flux n'est reçu. Utilisé pour le transfert de fichiers. 0 pour une durée illimitée. 0 par défaut. |
| `-OutFile <fichier>`                                                   | Précise le fichier de sortie.                                                                                                                                             |
| `-PassThru`                                                            | Envoi les résultats dans le terminal en plus du fichier de sortie si un fichier de sortie est indiqué.                                                                    |
| `-PreserveAuthorizationOnRedirect`                                     | Conserve le header autorisation lorsque des redirections sont effectuées.                                                                                                 |
| `-PreserveHttpMethodOnRedirect`                                        | Préserve la méthode définie lors des redirections. Par défaut, les redirections sont traités avec la méthode GET.                                                         |
| `-Proxy <URI du proxy>`                                                | Précise un serveur proxy à utiliser.                                                                                                                                      |
| `-ProxyCredential <utilisateur/objet Credential>`                      | Précise les identifiants à utiliser lors de la connexion au proxy. Utilisateur actuel par défaut.                                                                         |
| `-ProxyUseDefaultCredentials`                                          | Utilise l'utilisateur actuel pour les connexions au proxy.                                                                                                                |
| `-Resume`                                                              | Essaye de reprendre le téléchargement du fichier. Ce paramètre fait reprendre le téléchargement de zéro si pour une quelconque raison cela n'est pas possible.            |
| `-RetryIntervalSec <secondes>`                                         | Spécifie l'intervalle d'envoi des tentatives lorsqu'un code 400,599,inclusive ou 304 est reçu.                                                                            |
| `-SessionVariable <$variable>`                                         | Enregistre la session dans une variable en tant qu'objet PowerShell.                                                                                                      |
| `-SkipCertificateCheck`                                                | Ne vérifie pas le certificat.                                                                                                                                             |
| `-SkipHeaderValidation`                                                | Ne valide pas les headers lors de l'envoi de la requête.                                                                                                                  |
| `-SkipHttpErrorCheck`                                                  | Ne prends pas en compte les codes d'erreurs HTTP et continue de traiter les réponses. Les erreurs sont affichés dans le pipeline comme le reste.                          |
| `-SslProtocol <Default;Tls;Tls11;Tls12;Tls13>`                         | Précise le protocole SLL/TLS autorisés. Par défaut tous les protocoles pris en charge par le système sont autorisés.                                                      |
| `-Token <token Oauth>`                                                 | Précise le token Oauth à inclure sous la forme d'une SecureString.                                                                                                        |
| `-TransferEncoding <chunked;compress;deflate;gzip;identity>`           | Précise la valeur du champ "transfer-encoding HTTP response" dans le header. Cela permet de déinir l'encodage de retour souhaité.                                         |
| `-UnixSocket <socket Unix>`                                            | Spécifie le nom du socket Unix auquel se connecter                                                                                                                        |
| `-Uri <URI>`                                                           | Spécifie l'URI (uniforme ressource identifier). Autorise HTTP et HTTPS.                                                                                                   |
| `-UseBasicParsing`                                                     | Utilise le BasicPasing. Actif par défaut et paramètre désormais obsolète.                                                                                                 |
| `-UseDefaultCredentials`                                               | Utilise les informations d'identification de l'utilisateur actuel pour envoyer la requête.                                                                                |
| `-UserAgent <userAgent>`                                               | Précise le champ UserAgent dans le header de la requête.                                                                                                                  |
| `-WebSession <session>`                                                | Utilise les informations enregistrées d'une session pour définir la requête. Voir -SessionVariable.                                                                       |

# Exemples

Effectue une requête GET vers https://google.com
`Invoke-WebRequest -URI https://google.com`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest
