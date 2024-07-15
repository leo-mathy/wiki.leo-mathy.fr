---
title: Diskshadow
description: Commande permettant d'interagir avec le service VSS (Volume Shadow Copy Service), cela permet d'effectuer des sauvegardes de disques ou fichiers même si ils sont en cours d'utilisation
published: true
date: 2024-07-15T11:36:55.305Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-15T11:23:06.422Z
---

# Introduction

Diskshadow est une commande permettant d'interagir avec le service VSS (Volume Shadow Copy Service), cela permet d'effectuer des sauvegardes de disques ou fichiers même si ils sont en cours d'utilisation.

# Syntaxe de lancement

`diskshadow.exe`

# Commandes

| Commande                            | Description                                                                                                      |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `set [commande] [options]`          | Défini les paramètres                                                                                            |
| `begin backup`                      | Lance une session de sauvegarde complète                                                                         |
| `add [commande] [options]`          | Ajoute des volumes aux volumes qui doivent être sauvegardés                                                      |
| `create`                            | Démarre le processus de création de cliché instantané avec les paramètres actuels                                |
| `expose [ShadowID/Alias] [options]` | Expose un cliché instantané persistant sous la forme d’une lettre de lecteur, de partage ou de point de montage. |
| `end backup`                        | Met fin à la session de création de cliché instantané                                                            |
| `exit`                              | Quitte Diskshadow                                                                                                |

# Commandes set context

| Commande                              | Description                                                                                                                   |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `set context clientaccessible`        | Spécifie que le cliché instantané est utilisable par les versions clientes de Windows. Ce contexte est persistant par défaut. |
| `set persistent`                      | Spécifie que le cliché instantané persiste après avoir quitté DiskShadow                                                      |
| `set volatile`                        | Supprime le cliché instantané lors de la sortie ou de la réinitialisation.                                                    |
| `set [persistent/volatile] nowriters` | Spécifie que tous les rédacteurs sont exclus.                                                                                 |

# Commandes set metadata

| Commande                                                            | Description                                                                                     |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `set metadata [disque]:\[chemin]\[fichier metadata au format .cab]` | Définit le nom et l’emplacement du fichier où stocker les métadonnées de la création de cliché. |

# Commandes set verbose

| Commande               | Description                                               |
| ---------------------- | --------------------------------------------------------- |
| `set verbose [on/off]` | Active le mode verbose pour fournir une sortie détaillée. |

# Commandes add

| Commande                                | Description                                                                            |
| --------------------------------------- | -------------------------------------------------------------------------------------- |
| `add volume [volume]`                   | Ajoute un volume aux volumes qui doivent être sauvegardés.                             |
| `add volume [volume] alias [nom alias]` | Ajoute un volume aux volumes qui doivent être sauvegardés et donne un alias au volume. |
| `add alias [nom alias] [valeur alias]`  | Ajoute un nom et une valeur à l'environnement d'alias                                  |

# Commandes expose

| Commande                                     | Description                                                                            |
| -------------------------------------------- | -------------------------------------------------------------------------------------- |
| `expose [ShadowID/Alias] [disque]`           | Expose le cliché instantané sous forme de disque (par exemple E:)                      |
| `expose [ShadowID/Alias] [disque]`           | Expose le cliché instantané sous forme de partage (par exemple \\\share)               |
| `expose [ShadowID/Alias] [point de montage]` | Expose le cliché instantané sous forme de point de montage (par exemple c:\shadowcopy) |

# Voir aussi

Documentation officielle:
https://learn.microsoft.com/fr-fr/windows-server/administration/windows-commands/diskshadow
