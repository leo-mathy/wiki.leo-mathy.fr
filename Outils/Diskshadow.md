---
title: Diskshadow
description: Commande permettant d'interagir avec le service VSS (Volume Shadow Copy Service), cela permet d'effectuer des sauvegardes de disques ou fichiers même si ils sont en cours d'utilisation
published: true
date: 2024-07-15T11:23:06.422Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-15T11:23:06.422Z
---

# Introduction

Diskshadow est une commande permettant d'interagir avec le service VSS (Volume Shadow Copy Service), cela permet d'effectuer des sauvegardes de disques ou fichiers même si ils sont en cours d'utilisation.

# Syntaxe de lancement

`diskshadow.exe`

# Commandes

| Commande                   | Description           |
| -------------------------- | --------------------- |
| `set [commande] [options]` | Défini les paramètres |

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

# Voir aussi

Documentation officielle:
https://learn.microsoft.com/fr-fr/windows-server/administration/windows-commands/diskshadow
