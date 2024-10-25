---
title: EoPLoadDriver
description: Active et utilise le privilège SeLoadDriverPrivilege dans le processus, puis créer les clés de registre et charge le driver en utilisant la fonction NTLoadDriver.
published: true
date: 2024-07-19T11:52:52.794Z
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

> Depuis Windows 10 Version 1803, le privilège SeLoadDriverPrivilege n'est plus exploitable, depuis qu'il n'est plus possible d'inclure des references aux clés de registre depuis HKEY_CURRENT_USER (HKCU)
> {.is-danger}

# Syntaxe

`EOPLOADDRIVER.exe [chemin du registre] [chemin de l'image du driver]`

# Exemples

Active et utilise le privilège SeLoadDriverPrivilege dans le processus, puis créer la clés de registre **System\CurrentControlSet\Capcom** avec le chemin **c:\temp\Capcom.sys** et charge le driver en utilisant la fonction NTLoadDriver.

`EoPLoadDriver.exe System\CurrentControlSet\Capcom c:\temp\Capcom.sys`
