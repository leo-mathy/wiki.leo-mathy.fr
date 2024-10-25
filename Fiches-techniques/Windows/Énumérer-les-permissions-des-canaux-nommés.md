---
title: Énumérer les permissions des canaux nommés
description: Les canaux sont utilisés pour la communication entre deux applications ou processus en utilisant de la mémoire partagée.
published: true
date: 2024-10-25T20:36:45.026Z
tags: windows, fiche technique
editor: markdown
dateCreated: 2024-07-11T16:57:58.359Z
---

# Introduction

Les canaux sont utilisés pour la communication entre deux applications ou processus en utilisant de la mémoire partagée. Il est possible de voir les permissions assignés à un canal nommé en regardant la Discretionary Access List (DACL) assignée au canal.

> Un exemple de canal nommé est \\.\PipeName\\ExampleNamedPipeServer
> {.is-info}

# Énumérer les permissions avec AccessChk

## Introduction

Il est possible d'énumérer les permissions des canaux nommés avec AccessChk, un outil de la suite Sysinternals de Microsoft.

> Disponible au téléchargement ici: https://learn.microsoft.com/en-us/sysinternals/downloads/accesschk
> {.is-success}

## Syntaxe

`.\accesschk.exe /accepteula [canal nommé]`

## Options

| Option | Description            |
| ------ | ---------------------- |
| `-v`   | Active le mode verbose |

## Exemples

Voir les permissions de tous les canaux nommés dans \\.\Pipe\

`.\accesschk.exe /accepteula \\.\Pipe\`

Voir les permissions du canal nommé lsass en mode verbose

`accesschk.exe /accepteula \\.\Pipe\lsass -v`
