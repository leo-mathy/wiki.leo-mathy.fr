---
title: HiveNightmare
description: Aussi connu sous le nom de SeriousSam. Exploite une erreur sur certaines versions de Windows, permettant à tous les utilisateurs de lire les ruches de registre (SAM,SECURITY...). Effectue une copie de ces ruches pour une exploitation hors-ligne. 
published: true
date: 2024-08-25T15:00:53.332Z
tags: outil, windows
editor: markdown
dateCreated: 2024-08-23T13:57:13.399Z
---

# Introduction

Aussi connu sous le nom de SeriousSam. Exploite une erreur sur certaines versions de Windows, permettant à tous les utilisateurs de lire les ruches de registre (SAM,SECURITY...). Effectue une copie de ces ruches pour une exploitation hors-ligne.

> La présence d'une Shadow Copy au minimum est nécessaire à l'exploitation. Il est impossible de copier des ruches de registre, par exemple la base SAM, en direct car le fichier est verrouillé pendant que Windows est en cours d'exécution. C'est pour cela qu'il faut passer par les Shadow Copy.
> {.is-warning}

> De base la protection système est activé par défaut, donc les Shadow Copy de ces ruches doivent être présentes.
> {.is-success}

> HiveNightmare est disponible au téléchargement [ici](https://github.com/GossiTheDog/HiveNightmare)
> {.is-info}

# Syntaxe

`HiveNightmare.exe [nombre maximum de Shadow Copy à vérifier (15 par défaut)]`

# Paramètres

| Paramètre | Description    |
| --------- | -------------- |
| `/?`      | Affiche l'aide |

# Exemples

Recherche au maximum 5 Shadow Copy et enregistre les ruches trouvés dans le répertoire actuel.

`HiveNightmare.exe 5`

# Voir aussi

Article qui détaille l'exploit sur le blog de l'auteur:
https://doublepulsar.com/hivenightmare-aka-serioussam-anybody-can-read-the-registry-in-windows-10-7a871c465fa5

Fichier du repository permettant la détection et le changement des droits sur le registre pour remédier à cet exploit:
https://github.com/GossiTheDog/HiveNightmare/blob/master/Mitigation.ps1
