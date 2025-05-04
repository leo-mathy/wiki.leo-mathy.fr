---
title: Lister les canaux nommés
description: Les canaux sont utilisés pour la communication entre deux applications ou processus en utilisant de la mémoire partagée.
published: true
date: 2025-05-04T14:53:33.132Z
tags: windows, fiche technique
editor: markdown
dateCreated: 2024-07-11T16:42:14.911Z
---

# Introduction

Les canaux sont utilisés pour la communication entre deux applications ou processus en utilisant de la mémoire partagée. Les canaux nommés peuvent communiquer en mode half-duplex ou duplex. C'est à dire, que le client et le serveur peuvent communiquer dans un sens unique ou dans les deux sens.

> Un exemple de canal nommé est \\.\PipeName\\ExampleNamedPipeServer
> {.is-info}

# Liste avec Pipelist

## Introduction

Il est possible de lister les canaux nommés avec Pipelist, un outil de la suite Sysinternals de Microsoft.

> Disponible au téléchargement ici: https://learn.microsoft.com/fr-fr/sysinternals/downloads/pipelist
> {.is-success}

## Syntaxe

`pipelist.exe /accepteula`

# Liste avec Get-ChildItem

## Introduction

Il est possible de lister les canaux nommés avec l'applet powershell Get-ChildItem.

> L'alias de Get-ChildItem est gci
> {.is-info}

## Syntaxe

`gci \\.\pipe\`
