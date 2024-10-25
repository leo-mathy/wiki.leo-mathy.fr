---
title: rundll32
description: Permet de charger des DLL (Bibliothèques de liens dynamiques)
published: true
date: 2024-10-25T20:26:03.014Z
tags: windows, commande
editor: markdown
dateCreated: 2024-07-30T19:32:19.223Z
---

# Introduction

rundll32 permet de charger des DLL (Bibliothèques de liens dynamiques) et d'éxecuter une fonction contenue dans celui-ci. Il est aussi possible de passer des arguments.

# Syntaxe

> Le nom du fichier DLL ne doit contenir aucun espace.
> {.is-warning}

`rundll32.exe [nom du DLL],[fonction] <argument>`

# Exemples

Charge le DLL shell32.dll avec comme argument C:\temp\mydll.dll et appel la fonction Control_RunDLL à l'intérieur de celui-ci. Cette commande permet de charger le DLL C:\temp\mydll.dll dans le shell.

`rundll32.exe shell32.dll,Control_RunDLL C:\temp\mydll.dll`

# Voir aussi

Détails de l'interface rundll32 (archive)

https://web.archive.org/web/20150109234931/http://support.microsoft.com/kb/164787
