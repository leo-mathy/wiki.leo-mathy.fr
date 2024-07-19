---
title: EoPLoadDriver
description: Active et utilise le privilège SeLoadDriverPrivilege dans le processus, puis créer les clés de registre et charge le driver en utilisant la fonction NTLoadDriver.
published: true
date: 2024-07-19T11:50:15.517Z
tags: outil, windows
editor: markdown
dateCreated: 2024-07-19T11:50:15.517Z
---

# Introduction

Active et utilise le privilège SeLoadDriverPrivilege dans le processus, puis créer la clé de registre et charge le driver en utilisant la fonction NTLoadDriver.

> EoPLoadDriver est disponible au téléchargement ici: https://github.com/TarlogicSecurity/EoPLoadDriver/
> {.is-info}

> Il ne faut pas oublier que le code source C++ doit être compilé
> {.is-warning}

# Syntaxe

`EOPLOADDRIVER.exe [chemin du registre] [chemin de l'image du driver]`

# Exemples

Active et utilise le privilège SeLoadDriverPrivilege dans le processus, puis créer la clés de registre **System\CurrentControlSet\Capcom** avec le chemin **c:\temp\Capcom.sys** et charge le driver en utilisant la fonction NTLoadDriver.

`EoPLoadDriver.exe System\CurrentControlSet\Capcom c:\temp\Capcom.sys`
