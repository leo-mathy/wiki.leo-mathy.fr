---
title: Information Gathering - Web Edition
description: 
published: true
date: 2025-02-08T16:34:19.253Z
tags: notes, htb, module
editor: markdown
dateCreated: 2025-02-08T15:33:50.601Z
---

# Footprinting

Date de complétion: XX/XX/2025

[information_gathering_web_edition_module_cheat_sheet.pdf](/cheat_sheet/information_gathering_web_edition_module_cheat_sheet.pdf)

# Notes

## Introduction

La reconnaissance web est une partie de la phase de collecte d'information lors du processus de pentest.
Ce processus doit systématiquement et de manière méticuleuse, collecter des informations sur une application ou un site web.

C'est la phase préparatoire avant l'analyse poussée et l'exploitation.

Le but de la reconnaissance web est:
- D'identifier les actifs: Définir les composants de la cible accessibles publiquement (pages web, domaines, adresses, technologies...), ce qui permet d'avoir une vue globale de la présence en ligne de la cible.
- Découvrir les informations cachées: Localiser les informations sensibles qui peuvent être exposés par inadvertance (fichiers,configurations,documentation...). Ces fichiers peuvent réveler des informations précieuses et des points d'entrés potentiels aux attaques.
- Analyser la surface d'attaque: Analyser la surface d'attaque permet d'identifier les vulnérabilités et failles potentielles. Cela correspond à l'évaluation des technologies utilisées, des configurations et des possibles points d'entrés.
- Collecter les renseignements (Intelligence gathering): Collecter les informations qui peuvent être utilisées pour l'exploitation ou les attaques sociales. Cela correspond à l'identification du personnel clé, adresses mail... ou encore des modèles ou comportements pouvant être exploités.

Toutes ces informations sont utilisées par les attaquants pour façonner leurs attaques en ciblant des faiblesses spécifiques et en contournant les mesures de sécurité.
En revanche, les défenseurs utilisent ces informations pour proactivement identifier et corriger les vulnérabilitées avant leurs exploitation.

Il y a deux types de méthodologies de reconnaissance, active et passive.

Dans une reconnaissance active, l'attaquant intérragi directement avec le système cible pour récupérer des informations (scan de ports/vulnérabilités, cartographie réseau, banner grabing, OS fingerprinting, spidering), dans la pluspart des cas, la reconnaissance active est associée à un risque de détection plus grand.

Dans une reconnaissance passive, l'attaquant n'intéragi pas directement avec la cible pour récupérer des informations. Cela se base sur l'analyse des informations et ressources disponibles publiquement (Moteurs de recherche,WHOIS,DNS,Archives web, Réseaux sociaux, repos de code...).
La reconnaissance passive est donc plus discrète.

## WHOIS

WHOIS est un protocole créé pour acceder aux bases de données stockant les informations concernant les ressources Internet enregistrées. En plus d'être associé aux noms de domaines, WHOIS peut aussi fournir les détails sur les blocks d'IP et les systèmes autonomes.

WHOIS peut être représenté comme un annuaire pour Internet, qui permet de voir qui est responsable ou propriétaire pour de nombreux types de ressources en ligne.

WHOIS est apparu dans les années 70 pour surveiller et administrer les ressources sur le réseau Arpanet. Le successeur de WHOIS est RDAP.

`whois <domaine.tld>`

WHOIS est important dans la reconnaissance web, il permet de:
- Identifier le personnel clé: les enregistrements WHOIS révèlent souvent des informations sur le personnel clé (nom, adresses mail, numéros de téléphone...) qui est responsable de l'administration du domaine.
- Découvrir l'infrastructure réseau: des détails techniques comme les serveurs DNS et adresses IP donnent des indices sur le réseau de la cible.
- Analyse des données historiques: Les anciens enregistrements WHOIS peuvent être consultés sur des services comme [WhoisFreaks](https://whoisfreaks.com/). Les anciens enregistrements peuvent être utilisés pour voir les changement de propriétaires, informations de contact ou détails techniques, dans le temps (permet de voir l'évolution de la présence en ligne de la cible).

