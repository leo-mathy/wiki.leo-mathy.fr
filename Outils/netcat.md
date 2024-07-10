---
title: Netcat
description: Netcat est un utilitaire permettant d'ouvrir des connexions réseau, cet outil peut être utilisé pour de nombreux usages
published: true
date: 2024-04-15T06:50:52.076Z
tags: outil, linux
editor: markdown
dateCreated: 2024-04-15T06:48:30.391Z
---

# Introduction

Netcat est un puissant outil permetttant l'écoute de ports ou encore l'ouverture de connexion réseau, cet outil est principalement utilisé pour se connecter à une une connexion inverse ou backdoor, mais il a d'autres nombreux usages.

# Usage
`netcat [ip/port/les deux]`

# Options
Mode écoute (listen), attendre une connexion entrante
`-l`
Mode verbose, affiche des informations supplémentaires
`-v`
Désactive la résolution DNS (permet d'augmenter la vitesse de connexion)
`-n`
Spécifie un port d'écoute et aussi là où la connexion est envoyé
`-p`
