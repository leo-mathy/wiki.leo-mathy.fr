---
title: sc
description: Communique avec le Controlleur de Services et les services installés, permet d'interagir avec les services
published: true
date: 2024-10-25T20:26:18.417Z
tags: windows, commande, rédaction incomplète
editor: markdown
dateCreated: 2024-07-16T18:09:23.569Z
---

# Introduction

La commande sc permet de communiquer avec le Controlleur de Services et les services installés, permet d'interagir avec les services.

# Syntaxe

`sc.exe [ordinateur] [commande] [options]`

# Commandes

| Commande                                                          | Description                                                                                                                                    |
| ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `boot [ok/bad]`                                                   | Indique si le dernier démarrage doit être enregistré en tant que dernière bonne configuration connue ou non.                                   |
| `config`                                                          | Modifie les valeures des entrés des services dans le registre et la base SCM                                                                   |
| `continue [nom du service]`                                       | Résume le service qui était en pause                                                                                                           |
| `create`                                                          | Créer les sous clés et les entrées dans la base SCM pour un nouveau service                                                                    |
| `delete [nom du service]`                                         | Supprime les clés et entrées dans la base SCM pour le service indiqué. Si le service est en cours d'éxecution la procédure est mise en attente |
| `description [nom du service] [description]`                      | Modifie la description d'un service                                                                                                            |
| `enumdepend [nom du service]`                                     | Affiche les services qui dépendent du service indiqué                                                                                          |
| `failure`                                                         | Spécifie les actions à prendre lorsqu'un service échoue                                                                                        |
| `getdisplayname [nom du service]`                                 | Affiche le nom d'affiche d'un service                                                                                                          |
| `getkeyname [nom d'affichage du service]`                         | Affiche le nom du service à partir du nom d'affichage du service                                                                               |
| `interrogate [nom du service]`                                    | Envoi un contrôle INTERROGATE à un service (permet aussi de mettre à jour son statut au controlleur des services                               |
| `lock`                                                            | Bloque temporairement la base SCM, ce qui empèche de nouveaux services de s'éxecuter                                                           |
| `pause [nom du service]`                                          | Envoi un contrôle PAUSE à un service                                                                                                           |
| `qc [nom du service]`                                             | Affiche les informations de configuration d'un service                                                                                         |
| `qdescription [nom du service]`                                   | Affiche la description d'un service                                                                                                            |
| `qfailure [nom du service]`                                       | Affiche les actions éxecutés si le service spécifie échoue                                                                                     |
| `querylock`                                                       | Affiche le statut du vérouillage de la base SCM                                                                                                |
| `sdset [nom du service] [Descripteur de sécurité au format SDLL]` | Modifie le Descripteur de sécurité pour un service en utilisant le language SDDL                                                               |
| `sdshow [nom du service]`                                         | Affiche le Descripteur de sécurité pour un service en utilisant le language SDD                                                                |
| `start [nom du service] [arguments]`                              | Démarre un service avec des arguments facultatifs                                                                                              |
| `stop [nom du service]`                                           | Envoi un contrôle STOP à un service                                                                                                            |

> Pour les commandes plus complèxes, une partie de cette documentation est assignée pour chaque commande
> {.is-info}

# Options

| Option    | Description |
| --------- | ----------- |
| `config`  | /           |
| `create`  | /           |
| `failure` | /           |

# Exemples

Envoi un contrôle STOP au service nommé tapisrv

`sc.exe stop tapisrv`

Affiche les informations de configuration du service tapisrv

`sc.exe qc tapisrv`
