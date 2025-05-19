---
title: smbmap
description: Outil permettant d'énumérer les partages SMB.
published: true
date: 2025-05-19T19:15:00.793Z
tags: outil, linux
editor: markdown
dateCreated: 2025-05-19T19:15:00.793Z
---

# Introduction

Outil permettant d'énumérer les partages SMB.

> smbmap est disponible [ici](https://github.com/ShawnDEvans/smbmap)
{.is-info}

# Syntaxe

`smbmap [-H <adresse>] [-u <utilisateur>] [-p <mot de passe>] [-d <domaine>]`

# Exemples

Lister les partages sur la machine `192.168.0.1` avec l'utilisateur `workgroup\jsmith`:

```
smbmap -u jsmith -p password1 -d workgroup -H 192.168.0.1
```
