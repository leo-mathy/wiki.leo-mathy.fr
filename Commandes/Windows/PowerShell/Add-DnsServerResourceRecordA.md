---
title: Add-DnsServerResourceRecordA
description: Ajoute un enregistrement de type A (Nom vers Ipv4) dans une zone DNS
published: true
date: 2024-10-25T20:29:24.201Z
tags: windows, commande, powershell
editor: markdown
dateCreated: 2024-07-16T18:12:53.931Z
---

# Introduction

L'applet Powershell Add-DnsServerResourceRecordA permet d'ajouter un enregistrement de type A (Nom vers Ipv4) dans une zone DNS.

# Syntaxe

`Add-DnsServerResourceRecordA [options]`

# Options

| Option                               | Description                                                                                                                           |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| `-AgeRecord`                         | Permet d'ajouter un timestamp pour la ressource ajoutée (utile si le serveur DNS utilise cette donnée)                                |
| `-AllowUpdateAny`                    | Indique que n'importe quel utilisateur authentifié peut mettre à jour la ressource si l'enregistrement a le même nom de propriétaire. |
| `-AsJob`                             | Exécute la commande en arrière-plan                                                                                                   |
| `-CimSession [Session/ordinateur]`   | Exécute la commande sur une session spécifique ou un ordinateur                                                                       |
| `-ComputerName [ordinateur]`         | Spécifie l'ordinateur distant                                                                                                         |
| `-Confirm`                           | Demande une confirmation avant d'exécuter la commande                                                                                 |
| `-CreatePtr`                         | Indique si un enregistrement inverse associé doit être créer (IPv4 vers Nom DNS)                                                      |
| `-IPv4Address [IPv4]`                | Spécifie une ou plusieur Ipv4                                                                                                         |
| `-Name [nom]`                        | Spécifie le nom de l'enregistrement                                                                                                   |
| `-PassThru`                          | Affiche la l'enregistrement DNS après l'exécution de la commande                                                                      |
| `-TimeToLive [secondes]`             | Précise le TTL de l'enregistrement en secondes                                                                                        |
| `-VirtualizationInstance [Instance]` | Spécifie dans quelle instance l'enregistrement doit être effectué sur le serveur DNS                                                  |
| `-WhatIf`                            | N'exécute pas la commande mais indique ce qui se passerai si la commande était exécuté                                                |
| `-ZoneName [nom de la zone]`         | Spécifie le nom de la zone DNS                                                                                                        |
| `-ZoneScope [étendue]`               | Spécifie dans quelle étendue l'opération s'effectue                                                                                   |

# Exemples

Ajoute un enregistrement DNS de type A sur le serveur 10.10.10.1, dans la zone area.local et pointant myname vers 10.10.10.5

`Add-DnsServerResourceRecordA -Name wpad -ZoneName area.local -ComputerName 10.10.10.1 -IPv4Address 10.10.10.5`
