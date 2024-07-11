---
title: whoami
description: Cette commande peut être employé pour obtenir le nom d’utilisateur, les informations de groupe ainsi que les identificateurs de sécurité (SID)
published: true
date: 2024-07-11T12:25:15.553Z
tags: cmd, windows
editor: markdown
dateCreated: 2024-07-11T12:25:15.553Z
---

# Introduction

Cette commande peut être employé pour obtenir le nom d’utilisateur, les informations de groupe ainsi que les identificateurs de sécurité (SID).

# Syntaxe

whoami [options]

# Options

| Option    | Description                                                                                    |
| --------- | ---------------------------------------------------------------------------------------------- |
| `/UPN`    | Affiche le nom d’utilisateur au format UPN                                                     |
| `/FQDN`   | Affiche le nom d’utilisateur au format FQDN                                                    |
| `/USER`   | Affiche les informations de l’utilisateur actuel ainsi que l’identificateur de sécurité (SID). |
| `/GROUPS` | Affiche l’appartenance de groupe de l’utilisateur actuel                                       |
| `/PRIV`   | Affiche les privilèges de sécurité de l’utilisateur actuel dans le contexte actuel             |
| `/ALL`    | Affiche toutes les informations concernant l'utilisateur                                       |

# Exemples

Affiche les privilèges de l'utilisateur dans le contexte actuel

`whoami /priv`
