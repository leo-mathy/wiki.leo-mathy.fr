---
title: ProxyChains
description: Redirige toutes les connexions TCP effectuées par n'importe quelle application vers un proxy.
published: true
date: 2024-11-26T19:00:08.002Z
tags: outil, linux, synthèse
editor: markdown
dateCreated: 2024-11-26T18:59:57.304Z
---

# Introduction

ProxyChains permet de rediriger toutes les connexions TCP effectuées par n'importe quelle application vers un proxy.

> Les types de proxy suivants sont actuellement supportés: TOR/SOCKS4/SOCKS5/HTTP/HTTPS
> {.is-info}

> ProxyChains est disponible au téléchargement [ici](https://proxychains.sourceforge.net/)
> {.is-info}

ProxyChains va chercher le fichier de configuration proxychains.conf dans

- `./proxychains.conf`
- `$(HOME)/.proxychains/proxychains.conf`
- `/etc/proxychains.conf`
- `/etc/proxychains4.conf`

# Syntaxe

`ProxyChains [paramètres] <commande>`

# Exemples

Redirige l'outil msfconsole vers le proxy indiqué dans le fichier de configuration.
`ProxyChains msfconsole`

# Voir aussi

Page github officielle
https://github.com/haad/proxychains

Fichier de configuration par défaut
https://github.com/haad/proxychains/blob/master/src/proxychains.conf
