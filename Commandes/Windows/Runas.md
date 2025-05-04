---
title: Runas
description: Runas permet à un utilisateur d'exécuter des commandes et programmes en tant qu'un utilisateur différent.
published: true
date: 2025-05-04T14:52:32.024Z
tags: windows, commande
editor: markdown
dateCreated: 2024-09-08T08:57:52.613Z
---

# Introduction

Runas permet à un utilisateur d'exécuter des commandes et programmes en tant qu'un utilisateur différent.

# Syntaxe

`runas [paramètres] /user:[DOMAINE\]<utilisateur> <ligne de commande>`

# Paramètres

| Paramètre                                           | Description                                                                                                                                                       |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/profile`                                          | Charge le profil de l'utilisateur (ne charge pas les politiques de groupes, cela se produit uniquement pour les connexions interactives.). (paramètre par défaut) |
| `/no profile`                                       | Ne charge pas le profil de l'utilisateur.                                                                                                                         |
| `/env`                                              | Utilise l'environnement réseau à la place de l'environnement local de l'utilisateur. Utile pour l'accès aux ressources réseau.                                    |
| `/netonly`                                          | Indique que les informations de l'utilisateur spécifiées sont pour l'accès à distance uniquement. (limité à des sessions d'accès à distance)                      |
| `/savecred`                                         | Utilise les informations stockées dans le gestionnaire d'identification pour se connecter.                                                                        |
| `/smartcard`                                        | Utilise une carte à puce pour se connecter.                                                                                                                       |
| `/showtrustlevels`                                  | Affiche les niveau de confiance disponibles sur le système.                                                                                                       |
| `/trustlevel <niveau>`                              | Spécifie a quel niveau de confiance l'application doit être exécutée.                                                                                             |
| `/user:[DOMAINE\]<utilisateur> <ligne de commande>` | Spécifie l'utilisateur à utiliser.                                                                                                                                |
| `/?`                                                | Affiche l'aide.                                                                                                                                                   |

# Exemples

Exécute l'invite de commande "cmd" avec l'utilisateur Administrateur local et en utilisant les informations enregistrées dans le gestionnaire d'identification.
`runas /savecred /user:POSTE001\Administrateur cmd`

# Voir aussi

Documentation officielle
https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771525(v=ws.11)
