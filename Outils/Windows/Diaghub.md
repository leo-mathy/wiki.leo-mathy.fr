---
title: Diaghub
description: Diaghub est un service qui donne des informations de debug en collectant des données de trace. Il est possible d'interagir avec ce service pour le forcer à charger un DLL arbitraire.
published: true
date: 2024-08-27T17:40:20.084Z
tags: outil, windows, élévation des privilèges
editor: markdown
dateCreated: 2024-08-27T17:34:30.407Z
---

# Introduction

Microsoft (R) Diagnostics Hub Standard Collector Service (ou diaghub) est un service qui donne des informations de debug en collectant des données de trace. Ces fonctionnalités sont exposés depuis un objet DCOM. Il est possible d'intéragir avec cet objet pour le forcer à charger un DLL arbitraire situé dans C:\Windows\System32\.

> L'exploit est disponible au téléchargement [ici](https://github.com/xct/diaghub)
> {.is-info}

# Syntaxe

`diaghub.exe [chemin valide] [nom du DLL situé dans System32]`

# Voir aussi

Explications en résumé de l'exploit
https://vuln.dev/2019/03/06/abusing-diaghub/

Explications en détails de l'exploit
https://googleprojectzero.blogspot.com/2018/04/windows-exploitation-tricks-exploiting.html
