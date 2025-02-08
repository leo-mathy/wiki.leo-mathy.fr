---
title: Information Gathering - Web Edition
description: 
published: true
date: 2025-02-08T15:52:36.953Z
tags: notes, htb, module
editor: markdown
dateCreated: 2025-02-08T15:33:50.601Z
---

# Footprinting

Date de complétion: XX/XX/2025

# Notes

## Introduction

La reconaissance web est la fondation d'une évaluation de sécurité complète.
Ce prrocessus doit systématiquement et de manière méticuleuse, collecter des informations sur une application ou un site web.

C'est la phase préparatoire avant l'analyse poussée et l'exploitation.

La reconnaissance web est une partie de la phase de collecte d'information lors du processus de pentest.

Le but de la reconnaissance web est:
- D'identifier les actifs: Définir les composants de la cible accessibles publiquement (pages web, domaines, adresses, technologies...), ce qui permet d'avoir une vue globale de la présence en ligne de la cible.
- Découvrir les informations cachées: Localiser les informations sensibles qui peuvent être exposés par inadvertance (fichiers,configurations,documentation...). Ces fichiers peuvent réveler des informations précieuses et des points d'entrés potentiels aux attaques.
- Analyser la surface d'attaque: Analyser la surface d'attaque permet d'identifier les vulnérabilités et failles potentielles. Cela correspond à l'évaluation des technologies utilisées, des configurations et des possibles points d'entrés.
- Collecter les renseignements (Intelligence gathering): Collecter les informations qui peuvent être utilisées pour l'exploitation ou les attaques sociales. Cela correspond à l'identification du personnel clé, adresses mail... ou encore des modèles ou comportements pouvant être exploités.

Toutes ces informations sont utilisées par les attaquants pour façonner leurs attaques en ciblant des faiblesses spécifiques et en contournant les mesures de sécurité.
En revanches, les défenseurs utilisent ces informations pour proactivement identifier et corriger les vulnérabilitées avant leurs exploitation.

