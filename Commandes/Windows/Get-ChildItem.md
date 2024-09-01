---
title: Get-ChildItem
description: (alias de gci), permet d'obtenir les éléments enfants d'un élément spécifié (fichiers et dossier, registre, certificats...).
published: true
date: 2024-09-01T12:40:16.019Z
tags: windows, powershell
editor: markdown
dateCreated: 2024-08-31T18:20:06.615Z
---

# Introduction

L'applet Get-ChildItem (alias de gci) permet d'obtenir les éléments enfants d'un élément spécifié (fichiers et dossier, registre, certificats...).

# Syntaxe

`Get-ChildItem [chemin] [paramètres]`

> Par défaut, Get-ChildItem retourne le contenu du répertoire actuel.
> {.is-info}

# Paramètres

| Paramètre                               | Description                                                                                                                                                                               |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-Attributes <attribut>`                | Obtient uniquement les fichiers et dossiers avec les attributs spécifiés (Archive;Chiffré;Hidden;Lecture Seule...). Il est possible d'utiliser différents opérateurs ou des abréviations. |
| `-CodeSigningCert`                      | Obtient les certificats qui ont comme valeur "Code Signing" dans la propriété EnhancedKeyUsageList.                                                                                       |
| `-Depth <profondeur>`                   | Spécifie la profondeur de récursivité.                                                                                                                                                    |
| `-Directory`                            | Obtient uniquement les répertoires.                                                                                                                                                       |
| `-DnsName <propriété DNSNameList>`      | Obtient les certificats avec la valeur DNSNameList indiquée. Il est possible d'utiliser des wildcards.                                                                                    |
| `-DocumentEncryptionCert`               | Obtient les certificats qui ont comme valeur "Document Encryption" dans la propriété EnhancedKeyUsageList.                                                                                |
| `-Eku <propriété EnhancedKeyUsageList>` | Obtient les certificats avec la valeur EnhancedKeyUsageList indiquée. Il est possible d'utiliser des wildcards.                                                                           |
| `-Exclude <éléments à exclure>`         | Exclu des éléments de la sortie. Il est possible d'utiliser des wildcards.                                                                                                                |
| `-ExpiringInDays <nombre de jours>`     | Obtient les certificats qui expirent avant le nombre de jours indiqué. Une valeure de 0 obtient les certificats déjà expirés.                                                             |
| `-File`                                 | Obtenir uniquement des fichiers.                                                                                                                                                          |
| `-Filter <filtre>`                      | Utilise un filtre pour désigner le chemin. Il est possible d'utiliser des wildcards.                                                                                                      |
| `-FollowSymlink`                        | Suit les liens symboliques vers les répertoires.                                                                                                                                          |
| `-Force`                                | Obtient les éléments comme les fichiers masqués ou encore les fichiers système.                                                                                                           |
| `-Hidden`                               | Obtenir uniquement les éléments masqués.                                                                                                                                                  |
| `-Include <éléments à inclure>`         | Inclus des éléments de la sortie. Il est possible d'utiliser des wildcards.                                                                                                               |
| `-LiteralPath <chemin>`                 | Indique le chemin d'accès à l'emplacement littéralement (la valeur est utilisée exactement comme elle est tapée).                                                                         |
| `-Name`                                 | Obtenir uniquement le nom des éléments comme sortie.                                                                                                                                      |
| `-Path <chemin>`                        | Indique le chemin d'accès à l'emplacement.                                                                                                                                                |
| `-ReadOnly`                             | Obtenir uniquement les éléments en lecture seule.                                                                                                                                         |
| `-Recurse`                              | Obtient les éléments récursivement.                                                                                                                                                       |
| `-SSLServerAuthentication`              | Obtient les certificats qui ont comme valeur "Server Authentication" dans la propriété EnhancedKeyUsageList.                                                                              |
| `-System`                               | Obtenir uniquement les fichiers et repertoires système.                                                                                                                                   |

# Exemples

Obtenir récursivement les fichiers et dossiers en lecture seule à l'emplacement C:\tmp.
`Get-ChildItem -Path C:\tmp -Recurse -ReadOnly`

Obtenir les clés de registre contenues dans HKEY_LOCAL_MACHINE\HARDWARE.
`Get-ChildItem -Path HKLM:\HARDWARE`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.management/get-childitem

Détails sur les différents attribus des fichiers
https://learn.microsoft.com/fr-fr/dotnet/api/system.io.fileattributes
