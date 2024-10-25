---
title: UsoDllLoader
description: UsoDllLoader est un PoC d'une vulnérabilité exploitant le chargement d'un DLL inexistant par le service exécuté en tant que NT AUTHORITY\System: "Update Session Orchestrator" (USO).
published: true
date: 2024-10-25T20:48:56.663Z
tags: outil, windows
editor: markdown
dateCreated: 2024-08-27T17:22:22.853Z
---

# Introduction

UsoDllLoader est un PoC d'une vulnérabilité exploitant le chargement d'un DLL inexistant par le service "Update Session Orchestrator" (USO).

N'importe quel utilisateur peut demander une vérification ou le téléchargement des mises à jour grâce à usoclient.exe (usoclient StartInteractiveScan par exemple). Ce qui va démarrer le service "Update Session Orchestrator" (exécuté en tant que NT AUTHORITY\System) et charger le DLL windowscoredeviceinfo.dll situé dans C:\Windows\Sytem32\.

En résumé, exploit se base sur l'ajout d'un DLL malveillant dans C:\Windows\Sytem32\.

> La méthode peut ne pas fonctionner si des mises à jours sont en attentes d'installation ou en cours d'installation
> {.is-warning}

> le PoC est disponible au téléchargement [ici](https://github.com/itm4n/UsoDllLoader)
> {.is-info}

# Syntaxe

`UsoDllLoader.exe`

# Voir aussi

Détails sur la vulnérabilité:
https://itm4n.github.io/usodllloader-part1/
https://itm4n.github.io/usodllloader-part2/
