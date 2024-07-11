---
title: Tmux (Terminal Multiplexer)
description: tmux est un multiplexeur de terminaux libre en mode texte. Il permet d'utiliser plusieurs terminaux virtuels dans une seule fenêtre de terminal ou une session sur un terminal
published: true
date: 2024-07-11T09:13:01.851Z
tags: outil, linux
editor: markdown
dateCreated: 2024-04-15T06:39:11.320Z
---

# Introduction

Tmux est un multiplexeur de terminal, c'est à dire qu'il est possible avec un seul terminal d'avoir plusieurs fenêtres où entrer des commandes. Cela est extrêmement utile pour avoir plusieurs terminaux sans initier une nouvelle connexion.

# Syntaxe

`tmux [paramètres]`

# Options

> le préfixe de commande est CTRL + B , c'est à dire que pour gérer tmux, il faut tout d'abord presser ces touches.
> {.is-info}

| Raccourci                       | Description                         |
| ------------------------------- | ----------------------------------- |
| `Préfixe + C`                   | Ouvrir une nouvelle fenêtre         |
| `Préfixe + [Numéro de fenêtre]` | Changer de fenêtre                  |
| `Préfixe + SHIFT + %`           | Séparer le terminal verticalement   |
| `Préfixe + SHIFT + "`           | Séparer le terminal horizontalement |

# Exemples

Ouvrir tmux

`tmux`
