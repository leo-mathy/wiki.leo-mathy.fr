---
title: UACMe
description: permet de contourner la fonctionnalité User Account Control pour obtenir un token avec des privilèges élevés en utilisant la fonctionnalité d'auto-élévation.
published: true
date: 2024-07-30T18:50:41.911Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-30T18:50:41.911Z
---

# Introduction

UACMe permet de contourner la fonctionnalité User Account Control pour obtenir un token avec des privilèges élevés en utilisant la fonctionnalité d'auto-élévation.

> UACMe est disponible au téléchargement ici: https://github.com/hfiref0x/UACME
> {.is-info}

> Il est possible que certaines méthodes soient supprimées pour des raisons d'obsolescence. Il est possible d'utiliser une version antèrieure de UACme pour utiliser ces méthodes sur des systèmes plus anciens.
> {.is-warning}

> Les éxecutables doivent être compilés avant utilisation
> {.is-info}

# Syntaxe

Éxecutable principal pour les systèmes x64 ou x86-32

`akagi32.exe [clé] <options>`

`akagi64.exe [clé] <options>`

> Les options dépendent de méthode (désignée en utilisant la clé correspondante). Certaines méthodes n'ont aucune options à préciser.
> {.is-info}

> Les méthodes avec les clés associés sont disponibles ici: https://raw.githubusercontent.com/hfiref0x/UACME/master/README.md
> {.is-info}

# Exemples

Éxecute akagi.exe avec la méthode correspond à la clé 23.

`akagi32.exe 23`

Éxecute akagi.exe avec la méthode correspond à la clé 23 et un payload comme option.

`akagi32.exe 23 c:\tmp\payload.exe`

# Voir aussi

Exemple d'utilisation

https://infra.newerasec.com/infrastructure-testing/tools/uacme
