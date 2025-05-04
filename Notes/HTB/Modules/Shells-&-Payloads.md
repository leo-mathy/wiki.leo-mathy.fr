---
title: Shells & Payloads
description: 
published: true
date: 2025-05-04T16:31:15.419Z
tags: htb, module
editor: markdown
dateCreated: 2025-05-04T16:19:33.360Z
---

# Shells & Payloads

Date de complétion: XX/XX/XXXX

# Notes

## Shells Jack Us In, Payloads Deliver Us Shells

Un shell est un programme qui fournit à un utilisateur une interface où entrer des instructions et voir la sortie texte. Les shell les plus connus étant Bash, Zsh, Powershell ou encore cmd.

### Why Get a Shell?

Le shell permet un accès direct au système d'exploitation, aux commandes système et au système de fichiers. Une fois que nous avons un shell, nous pouvons rechercher des vecteurs d'élévation de privilèges, de pivotement, de transfert de fichiers, et plus encore. Sans un shell, nos actions sur une machine cible sont limitées.

Avoir un shell permet aussi de maintenir une persistance sur le système, offrant ainsi plus de temps pour travailler et facilitant l'utilisation des outils d'attaque, l'exfiltration de données, et la documentation de l'attaque. De plus, l'accès au shell en ligne de commande (CLI) est plus discret que l'accès à un shell graphique via VNC ou RDP. Les interfaces en ligne de commande sont plus rapides, plus difficiles à détecter et plus faciles à automatiser.

Le terme de shell possède plusieurs perspectives:

| **Perspective**        | **Description**                                                                                                                                                       |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Général**           | Environnement en ligne de commande utilisé pour administrer des tâches sur un PC (ex : Bash, PowerShell).                                                              |
| **Sécurité** | Un shell peut être obtenu en exploitant une vulnérabilité pour obtenir un accès interactif à un hôte (ex: EternalBlue).                   |
| **Web**                 | Un shell web exploite des vulnérabilités, comme le téléchargement d'un fichier ou script, pour permettre à l'attaquant de donner des instructions via des requètes HTTP. |



