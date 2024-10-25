---
title: ProcDump
description: Outil permettant de créer un fichier de vidage contenant la mémoire d'un processus
published: true
date: 2024-07-16T17:12:34.559Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-14T12:42:37.505Z
---

# Introduction

ProcDump est un outil de la suite Sysinternals de Microsoft permettant de créer un fichier de vidage contenant la mémoire d'un processus.

> ProcDump est disponible au téléchargement ici: https://learn.microsoft.com/fr-fr/sysinternals/downloads/procdump
> {.is-info}

> Si pour une raison quelconque, il est impossible d'avoir accès à cet outil, il est possible d'effectuer un vidage depuis le gestionnaire de tâches (Details>processus>Créer un fichier de vidage).
> {.is-success}

# Syntaxe

`procdump.exe -accepteula [options] [PID/nom processus] [fichier de vidage au format .dmp]`

# Options

| Option | Description                                         |
| ------ | --------------------------------------------------- |
| `-mm`  | Écrivez un fichier de vidage « Mini ». (par défaut) |
| `-ma`  | Écrivez un fichier de vidage « Complet ».           |

# Exemples

Effectue vidage de la mémoire complet du processus lsass.exe vers le fichier lsass.dmp

`procdump.exe -accepteula -ma lsass.exe lsass.dmp`
