---
title: Invoke-Clipboard
description: Récupère le contenu du clipboard (presse-papiers).
published: true
date: 2024-10-26T14:53:21.394Z
tags: outil, windows, powershell
editor: markdown
dateCreated: 2024-10-26T14:49:40.702Z
---

# Introduction

> Invoke-Clipboard est disponible [ici](https://github.com/inguardians/Invoke-Clipboard)
> {.is-info}

# Syntaxe

Enregistre le contenu du presse-papiers et l'affiche dans la session PowerShell actuelle.
`Invoke-ClipboardLogger`

Établi un canal "Command and Control" (C2C) via le presse-papiers. Exécute les commandes reçues et les envoies au serveur.
`Invoke-ClipboardC2C -message <commande>`

Établi un canal "Command and Control" (C2C) via le presse-papiers. Reçois la sortie des commandes.
`Invoke-ClipboardC2V`

# Exemples

Lance l'enregistrement du presse-papiers et l'affiche dans la session PowerShell actuelle.
`Invoke-ClipboardLogger`
