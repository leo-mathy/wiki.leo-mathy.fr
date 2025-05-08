---
title: Shells & Payloads
description: 
published: true
date: 2025-05-08T12:50:02.242Z
tags: htb, module
editor: markdown
dateCreated: 2025-05-04T16:19:33.360Z
---

# Shells & Payloads

Date de complétion: XX/XX/XXXX

# Shells Jack Us In, Payloads Deliver Us Shells

Un shell est un programme qui fournit à un utilisateur une interface où entrer des instructions et voir la sortie texte. Les shell les plus connus étant Bash, Zsh, PowerShell ou encore cmd.

## Why Get a Shell?

Le shell permet un accès direct au système d'exploitation, aux commandes système et au système de fichiers. Une fois que nous avons un shell, nous pouvons rechercher des vecteurs d'élévation de privilèges, de pivotement, de transfert de fichiers, et plus encore. Sans un shell, nos actions sur une machine cible sont limitées.

Avoir un shell permet aussi de maintenir une persistance sur le système, offrant ainsi plus de temps pour travailler et facilitant l'utilisation des outils d'attaque, l'exfiltration de données, et la documentation de l'attaque. De plus, l'accès au shell en ligne de commande (CLI) est plus discret que l'accès à un shell graphique via VNC ou RDP. Les interfaces en ligne de commande sont plus rapides, plus difficiles à détecter et plus faciles à automatiser.

Le terme de shell possède plusieurs perspectives:

| **Perspective** | **Description**                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Général**     | Environnement en ligne de commande utilisé pour administrer des tâches sur un PC (ex : Bash, PowerShell).                                                                |
| **Sécurité**    | Un shell peut être obtenu en exploitant une vulnérabilité pour obtenir un accès interactif à un hôte (ex: EternalBlue).                                                  |
| **Web**         | Un shell web exploite des vulnérabilités, comme le téléchargement d'un fichier ou script, pour permettre à l'attaquant de donner des instructions via des requêtes HTTP. |

## Payloads Deliver us Shells

Le terme "payload" peut être défini de différentes manières:

- Réseau : La partie contenant les données d'un paquet.
- Général: La partie d'un jeu d'instructions qui définit l'action à entreprendre.
- Programmation: La portion de données transportée par une instruction dans un langage de programmation.
- Sécurité: Le code créé pour exploiter une vulnérabilité dans un système informatique, incluant différents types de malwares.

# Anatomy of a Shell

Chaque système d'exploitation dispose d'un ou plusieurs shell. Pour intéragir avec un shell il faut utiliser un programme appellé émulateur de terminal (Terminal Emulator).

Voici quelques émulateurs de terminaux:

| **Émulateur de terminal** | **Système d'exploitation** |
| ------------------------- | -------------------------- |
| Windows Terminal          | Windows                    |
| cmder                     | Windows                    |
| PuTTY                     | Windows                    |
| kitty                     | Windows, Linux et MacOS    |
| Alacritty                 | Windows, Linux et MacOS    |
| xterm                     | Linux                      |
| GNOME Terminal            | Linux                      |
| MATE Terminal             | Linux                      |
| Konsole                   | Linux                      |
| Terminal                  | MacOS                      |
| iTerm2                    | MacOS                      |

Cette liste ne recense pas tous les émulateurs de terminal existants, mais elle présente certains des plus utilisés.
Beaucoup étant open source, il est possible de les installer sur d'autres systèmes d'exploitation que ceux prévus à l'origine. Le choix d’un émulateur de terminal dépend avant tout des préférences personnelles et du style de travail.
Sur les machines cibles, l’émulateur disponible dépendra généralement de celui intégré nativement au système.

## Command Language Interpreters

Un interpréteur de langage de commande (Command Language Interpreter) traduit en temps réel les instructions données par l'utilisateur pour les transmettre au système d'exploitation. Une interface en ligne de commande (CLI) fait donc référence au système d’exploitation, l’émulateur de terminal et l’interpréteur de commandes.

Il en existe plusieurs types, aussi appelés langages de script shell (shell scripting languages) ou interpréteurs de commandes et de scripts (Command and Scripting interpreters).

Connaître l’interpréteur utilisé sur un système donné nous aide aussi à savoir quelles commandes et quels scripts employer.

## Hands-on with Terminal Emulators and Shells

Dès l'ouverture de l'application MATE Terminal, celle-ci s'est ouverte avec un interpréteur de commandes préconfiguré.
Le symbole `$`, visible dans l'invite de commande, indique l'utilisation probable de Bash (ou d’un shell similaire comme Ksh ou POSIX).
Lorsque du texte aléatoire est saisi, Bash répond qu’il ne reconnaît pas la commande, ce qui montre que chaque interpréteur a ses propres commandes.

Une autre manière d’identifier l’interpréteur utilisé est de consulter les processus en cours d'exécution sur la machine avec `ps` ou de regarder la variable d'environnement `SHELL`.

Il est aussi possible d'ouvrir PowerShell avec l'application MATE Terminal, Cela montre qu'il est possible d'utiliser des interpréteurs de commandes différents pour un émulateur de terminal.

# Bind Shells
