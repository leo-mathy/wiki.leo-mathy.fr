---
title: Bypass-UAC
description: Permet de contourner l'UAC (User Account Control) en effectuant de appels de méthodes à l'interface (objet COM) "IFileOperation".
published: true
date: 2024-10-25T20:41:55.278Z
tags: outil, windows, powershell
editor: markdown
dateCreated: 2024-09-29T13:35:58.450Z
---

# Introduction

Bypass-UAC est un module PowerShell qui permet de contourner l'UAC (User Account Control) en effectuant de appels de méthodes à l'interface (objet COM) "IFileOperation".

La méthode traditionnelle pour effectuer cela est d'injecter un DLL (Dynamic Link Library) dans le processus explorer.exe. Cette méthode n'est pas conseillé car l'injection dans le processus explorer.exe est bruyante et peut déclencher des alertes de sécurité. Et que la gestion de DLL non managés est peu flexible.

La méthode alternative est de réécrire le PEB (Process Environnent Block) de PowerShell pour lui donner l'apparence du processus explorer.exe. Cela fonctionne puisque l'objet COM se base uniquement sur PSAPI (Windows's Process Status API) (PSAPI lis le PEB du processus, donc si deux processus ont le même PEB, alors l'objet COM ne fera aucune différence.)

> Bypass-UAC est disponible au téléchargement [ici](https://github.com/FuzzySecurity/PowerShell-Suite/tree/master/Bypass-UAC)
> {.is-info}

# Syntaxe

`Bypass-UAC -Method <méthode>`

# Méthodes

| Méthode             | Description                                             |
| ------------------- | ------------------------------------------------------- |
| `UacMethodSysprep`  | sysprep -> cryptbase.dll                                |
| `ucmDismMethod`     | PkgMgr -> DISM -> dismcore.dll                          |
| `UacMethodMMC2`     | mmc -> rsop.msc -> wbemcomn.dll                         |
| `UacMethodTcmsetup` | tcmsetup -> tcmsetup.exe.local -> comctl32.dll          |
| `UacMethodNetOle32` | mmc some.msc -> Microsoft.NET\Framework[64]..\ole32.dll |

# Exemples

Utilise la méthode UacMethodSysprep pour contourner l'UAC.

- se faire passer pour explorer.exe en changeant le PEB du processus par le même que explorer.exe.
- Ajout d'un DLL dans le processus.
- Appel de la méthode MoveItem sur l'interface de l'objet COM "IFileOperation".
- lancement de Sysprep
- Shell exécuté lors du lancement du DLL appelé lors du lancement du Sysprep.

`Bypass-UAC -Method UacMethodSysprep`

# Voir aussi

Détails sur les attaques UAC
https://fuzzysecurity.com/tutorials/27.html

Détails sur l'interface (objet COM) "IFileOperation".
https://learn.microsoft.com/fr-fr/windows/win32/api/shobjidl_core/nn-shobjidl_core-ifileoperation
