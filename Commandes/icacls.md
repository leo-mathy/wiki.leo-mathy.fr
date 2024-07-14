---
title: icacls
description: Affiche ou modifie les DACL (ACL d'accès) sur des fichiers ou répertoires
published: true
date: 2024-07-14T20:04:15.570Z
tags: cmd, windows
editor: markdown
dateCreated: 2024-07-14T20:04:15.570Z
---

# Introduction

La commande icacls (en remplacement de cacls) affiche ou modifie les DACL (ACL d'accès) sur des fichiers ou répertoires.

# Syntaxe

`icacls [fichier/repertoire] [options]`

# Options

| Option                                          | Description                                                                                                                                                                                                                                      |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/t`                                            | Effectue l’opération récursivement                                                                                                                                                                                                               |
| `/save [fichier]`                               | Stocke les DACL pour tous les fichiers pour une utilisation ultérieure avec /restore.                                                                                                                                                            |
| `/setowner [utilisateur]`                       | Modifie le propriétaire de tous les fichiers                                                                                                                                                                                                     |
| `/reset`                                        | Restore les permissions hérités par défaut                                                                                                                                                                                                       |
| `/grant[:r] [utilisateur/groupe]:[permissions]` | Ajoute des droits explicites pour un groupe ou utilisateur précis. Utiliser :r indique que les autorisations sont explicites, c'est à dire que les droits indiqués ne sont pas ajoutés mais remplacés.                                           |
| `/deny [utilisateur/groupe]:[permissions]`      | Refuse explicitement les droits pour un groupe ou utilisateur précis.                                                                                                                                                                            |
| `remove [utilisateur/groupe][:g/:d]`            | Supprime un groupe ou utilisateur de la DACL. Il est possible de supprimer uniquement les droits accordés avec :g ou les droits refusés avec :d.                                                                                                 |
| `/inheritancelevel:[e/d/r]`                     | Modifie l'héritage, e pour activer l'héritage, d pour désactiver l'héritage et convertir les droits anciennement hérités en droits explicits et r pour désactiver l'héritage sans convertir les droits anciennement hérités en droits explicits. |

# Type de permissions

| Type de permission          | Description                                                                                                                                             |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Séquence de droits simples  | **F** - Accès complet                                                                                                                                   |
|                             | **M** - Accès en modification                                                                                                                           |
|                             | **RX** - Accès en lecture et exécution                                                                                                                  |
|                             | **R** - Accès en lecture seule                                                                                                                          |
|                             | **W** - Accès en écriture seule                                                                                                                         |
| Liste de droits spécifiques | **D** - Supprimer                                                                                                                                       |
|                             | **RC** - Contrôle de lecture (autorisations de lecture)                                                                                                 |
|                             | **WDAC** - DAC d’écriture (autorisations de modification)                                                                                               |
|                             | **WO** - Propriétaire d’écriture (prendre possession)                                                                                                   |
|                             | **S** - Synchroniser                                                                                                                                    |
|                             | **AS** - Sécurité du système d’accès                                                                                                                    |
|                             | **MA** - Maximum autorisé                                                                                                                               |
|                             | **GR** - Lecture générique                                                                                                                              |
|                             | **GW** - Écriture générique                                                                                                                             |
|                             | **GE** - Exécution générique                                                                                                                            |
|                             | **GA** - Tout générique                                                                                                                                 |
|                             | **RD** - Lire des données/Répertorier les répertoires                                                                                                   |
|                             | **WD** - Écrire des données/Ajouter un fichier                                                                                                          |
|                             | **AD** - Ajouter des données/Ajouter un sous-répertoire                                                                                                 |
|                             | **REA** - Lire les attributs étendus                                                                                                                    |
|                             | **WEA** - Écrire des attributs étendus                                                                                                                  |
|                             | **X** - Exécuter/Parcourir                                                                                                                              |
|                             | **DC** - Supprimer un enfant                                                                                                                            |
|                             | **RA** - Attributs de lecture                                                                                                                           |
|                             | **WA** - Attributs d’écriture                                                                                                                           |
| Droits d’héritage           | **I** - Hériter. ACE héritée du conteneur parent.                                                                                                       |
|                             | **OI** - Héritage par les objets. Les objets de ce conteneur hériteront de cette ACE.                                                                   |
|                             | **CI** - Héritage par les conteneurs. Les conteneurs de ce conteneur parent héritent de cette ACE.                                                      |
|                             | **E/S** - Hériter uniquement. ACE héritée du conteneur parent, mais ne s’applique pas à l’objet lui-même.                                               |
|                             | **NP** - Ne pas propager l’héritage. ACE héritée par les conteneurs et les objets du conteneur parent, mais ne se propage pas aux conteneurs imbriqués. |

# Exemples

Ajoute les droits d'accès complets à l'utilisateur private sur le fichier C:\temp\note.txt.

`icacls C:\temp\note.txt /grant private:F`

Remplace les droits d'accès pour des droits de lecture seule à l'utilisateur private sur le dossier C:\temp\.

`icacls C:\temp\ /grant:r private:R`

# Voir aussi

Documentation officiel de icacls:
https://learn.microsoft.com/fr-fr/windows-server/administration/windows-commands/icacls
