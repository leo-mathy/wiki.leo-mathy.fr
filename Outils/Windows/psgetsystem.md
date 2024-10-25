---
title: psgetsystem
description: Module Powershell qui permet d'utiliser le privilège SeDebugPrivilege pour élever les privilèges. lancer un processus enfant privilégié, parent d'un processus SYSTEM.
published: true
date: 2024-10-25T20:45:56.341Z
tags: outil, windows, powershell
editor: markdown
dateCreated: 2024-07-14T14:11:03.531Z
---

# Introduction

Psgetsystem est un module Powershell qui permet d'utiliser le privilège SeDebugPrivilege pour élever les privilèges.
Le script powershell va lancer un processus enfant, parent d'un processus SYSTEM précisé, le processus enfant héritant du token du processus parent, il est maintenant possible d'utiliser ce token grace au privilège SeDebugPrivilege, pour exécuter des commandes en tant que l'utilisateur du processus parent.

> psgetsystem est disponible au téléchargement ici: https://github.com/decoder-it/psgetsystem/
> {.is-info}

# Syntaxe

`psgetsys.ps1; ImpersonateFromParentPid -ppid [PID du processus parent] -command [commande] -cmdargs [arguments de la commande]
`

# Exemples

Utilise le processus avec le PID 1068 comme processus parent, puis exécute la commande "cmd.exe shutdown /s"

`psgetsys.ps1; ImpersonateFromParentPid -ppid 1068 -command c:\Windows\System32\cmd.exe -cmdargs "shutdown /s"`
