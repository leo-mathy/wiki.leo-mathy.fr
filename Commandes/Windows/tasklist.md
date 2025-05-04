---
title: tasklist
description: Affiche une liste des processus actuellement en cours sur un ordinateur local ou un ordinateur distant
published: true
date: 2025-05-04T14:53:15.509Z
tags: windows, commande
editor: markdown
dateCreated: 2024-07-11T11:01:52.293Z
---

# Introduction

La commande tasklist permet d'afficher la liste des processus en cours sur le système.

> pour rappel,
>
> Une application est un programme avec lequel on interagit par le bureau.
> Un processus est une instance d'un éxecutable (il est possible d'avoir plusieurs processus pour un seul éxecutable, une instance.)
> Un service est un processus qui est actif en arrière plan et qui n'interagi pas avec le bureau.
> {.is-info}

# Syntaxe

`tasklist [options]`

# Options

| Option         | Description                                         |
| -------------- | --------------------------------------------------- |
| `/S`           | Spécifie le système auquel se connecter             |
| `/SVC`         | Affiche les services hébergés dans chaque processus |
| `/FI [filtre]` | Utilise un filtre personnalisé                      |

# Exemples

Affiche les processus et les services associés

`tasklist /SVC`

Affiche les processus et les services associés dans l'état suspendu

`tasklist /SVC /FI "STATUS eq SUSPENDED"`

Affiche les processus et les services dont le Process ID (PID) est 2800

`tasklist /SVC /FI "PID eq 2800"`

Affiche les processus et les services dont le nom du service est "Dhcp"

`tasklist /SVC /FI "SERVICES eq Dhcp"`
