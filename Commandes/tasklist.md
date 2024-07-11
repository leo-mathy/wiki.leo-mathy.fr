---
title: tasklist
description: Affiche une liste des processus actuellement en cours sur un ordinateur local ou un ordinateur distant
published: true
date: 2024-07-11T11:01:52.293Z
tags: cmd, windows
editor: markdown
dateCreated: 2024-07-11T11:01:52.293Z
---

# Introduction

La commande tasklist permet d'afficher la liste des processus en cours sur le système.

# Syntaxe

`tasklist [options]`

# Options

| Option   | Description                          |
| -------- | ------------------------------------ |
| `/S` | Spécifie le système auquel se connecter |
| `/SVC` | Affiche les services hébergés dans chaque processus |
| `/FI [filtre]` | Utilise un filtre personnalisé |

# Exemples

Affiche les processus et les services associés

`tasklist /SVC`

Affiche les processus et les services associés dans l'état suspendu

`tasklist /SVC /FI "STATUS eq SUSPENDED"`

Affiche les processus et les services dont le Process ID (PID) est 2800

`tasklist /SVC /FI "PID eq 2800"`

Affiche les processus et les services dont le nom du service est "Dhcp"

`tasklist /SVC /FI "SERVICES eq Dhcp"`



