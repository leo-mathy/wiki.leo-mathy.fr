---
title: keepass2john
description: Extrait un hash utilisable par HashCat/John depuis une base KeePass 1.x/2.x.
published: true
date: 2024-09-14T11:09:25.842Z
tags: outil, windows
editor: markdown
dateCreated: 2024-09-14T11:08:05.830Z
---

# Introduction

keepass2john est un script python qui extrait un hash utilisable par HashCat/John depuis une base KeePass 1.x/2.x. Cela permet par la suite de cracker le hash avec Hashcat par exemple.

> keepass2john est disponible au téléchargement [ici](https://gist.github.com/HarmJ0y/116fa1b559372804877e604d7d367bbc)
> {.is-info}

# Syntaxe

`keepass2john.py <base keepass au format .kdbx>`

# Exemples

Extrait le hash au format utilisable pas HashCast/John depuis la base "MyPasswords.kdbx".
`keepass2john.py MyPasswords.kdbx`
