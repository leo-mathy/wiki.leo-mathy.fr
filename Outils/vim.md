---
title: Vim
description: Vim est un éditeur de texte, c’est-à-dire un logiciel permettant la manipulation de fichiers texte.
published: true
date: 2024-07-11T09:38:06.092Z
tags: outil, linux
editor: markdown
dateCreated: 2024-04-15T06:57:26.511Z
---

# Introduction

Vim est un puissant éditeur de texte, il est utile de connaitre cet outil puisqu'il est présent sur la plupart des distributions linux par défaut.

# Syntaxe

`vim [options] [fichier]`

# Raccourcis

Vim étant utilisé en ligne de commande, il est utilisé avec des raccourcis clavier.

| Raccourci | Description              |
| --------- | ------------------------ |
| ESC       | Passer en mode normal    |
| I         | Passer en mode insertion |

Les raccourcis en mode normal sont les suivants.

| Raccourci | Description                             |
| --------- | --------------------------------------- |
| X         | Couper                                  |
| Dw        | Couper le mot                           |
| Dd        | Couper la ligne                         |
| Yw        | Copier le mot                           |
| Yy        | Copier la ligne                         |
| P         | Coller                                  |
| :1        | Se rendre à la ligne 1                  |
| :w        | Ecrire le fichier                       |
| :q        | Quitter                                 |
| :q!       | Quitter sans écrire le fichier (forcer) |

Il est possible de combiner certains raccourcis, pour ne pas avoir à passer en mode normal plusieures fois.

| Raccourci | Description                  |
| --------- | ---------------------------- |
| :wq       | Ecrire le fichier et quitter |

# Exemples

Éditer un fichier

`vim monfichier.conf`

> Si le fichier spécifié n'éxiste pas, il sera créer après son enregistrement.
> {.is-info}
