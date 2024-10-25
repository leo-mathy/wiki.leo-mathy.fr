---
title: robocopy
description: permet de copier des fichiers et dossiers d'un emplacement à un autre
published: true
date: 2024-10-25T20:25:08.356Z
tags: windows, commande
editor: markdown
dateCreated: 2024-07-15T13:16:58.176Z
---

# Introduction

Robocopy permet de copier des fichiers et dossiers d'un emplacement à un autre.

# Syntaxe

`robocopy [source] [desination] [fichiers] [options]`

# Options

| Option          | Description                                                                                                                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/s`            | Copie les sous-répertoires. Cette option exclut automatiquement les répertoires vides.                                                                                                                       |
| `/e`            | Copie les sous-répertoires. Cette option inclut automatiquement les répertoires vides.                                                                                                                       |
| `/lev:[niveau]` | Copie uniquement le nombre de niveau indiqué supérieurs de l'arborescence                                                                                                                                    |
| `/z`            | Copie les fichiers en mode de redémarrage. En mode de redémarrage, si une copie de fichier est interrompue, robocopy peut reprendre là où elle s’était arrêtée au lieu de recopier l’intégralité du fichier. |
| `/b`            | Copie les fichiers en mode de sauvegarde. En mode de sauvegarde, robocopy remplace les paramètres d’autorisation de fichier et de dossier (ACL), qui peuvent autrement bloquer l’accès.                      |
| `/copyall`      | Copie toutes les informations de fichier (équivalent à /copy:DATSOU).                                                                                                                                        |
| `/j`            | Copie à l’aide d’E/S non mises en mémoire tampon (recommandé pour les fichiers volumineux).                                                                                                                  |
| `/s`            | Copie les fichiers avec sécurité (équivalent à /copy:DATS).                                                                                                                                                  |
| `/mov`          | Déplace les fichiers et les supprime de la source après leur copie.                                                                                                                                          |
| `/move`         | Déplace les fichiers et les répertoires, et les supprime de la source après leur copie.                                                                                                                      |
| `/a`            | Copie uniquement les fichiers pour lesquels l’attribut Archive est défini.                                                                                                                                   |
| `/m`            | Copie uniquement les fichiers pour lesquels l’attribut Archive est défini et réinitialise l’attribut Archive.                                                                                                |
|                 |

# Exemples

Copier le fichier E:\temp\ntds.dit vers l'emplacement C:\temp\ en mode backup.
`robocopy /B E:\temp\ C:\temp\ ntds.dit`

# Voir aussi

Documentation complète:
https://learn.microsoft.com/fr-fr/windows-server/administration/windows-commands/robocopy
