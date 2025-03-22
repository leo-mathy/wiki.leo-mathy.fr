---
title: File Transfers
description: 
published: true
date: 2025-03-22T14:02:46.286Z
tags: notes, htb, module
editor: markdown
dateCreated: 2025-03-16T15:21:30.098Z
---

# File Transfers

Date de complétion: XX/XX/XX

# Notes

## Windows File Transfer Methods


### Introduction

Les nouvelles versions de Windows comportent de nombreux outils pour le transfert de fichiers.
Les attaquants utilisent le transfert de fichier pour opérer et éviter de se faire détecter.
Les défenseurs doivent connaitre ces méthodes et leur fonctionnement pour surveiller et créer les politiques correspondantes.

Le post [Microsoft Astaroth Attack](https://www.microsoft.com/security/blog/2019/07/08/dismantling-a-fileless-campaign-microsoft-defender-atp-next-gen-protection-exposes-astaroth-attack/) donne un exemple d'APT et des [menaces sans fichier](https://learn.microsoft.com/fr-fr/defender-endpoint/malware/fileless-threats).

Les menaces fileless, n'existent pas sous forme de fichiers mais exploitent des outils légitimes du système pour exécuter des attaques.

L'attaque Astaroth commence par un lien malveillant dans un e-mail de phishing, menant à un fichier LNK.
Celui-ci déclenche l'exécution de WMIC avec l'option "/Format" pour télécharger du code JavaScript malveillant.
Ce dernier utilise Bitsadmin pour récupérer des charges utiles encodées en base64, qui sont ensuite décodées avec Certutil.
Enfin, Regsvr32 charge un DLL permettant d'injecter le malware Astaroth dans le processus Userinit.

Voici les étapes de l'attaque Astaroth:
![fig1a-astaroth-attack-chain.png](/images/fig1a-astaroth-attack-chain.png){.align-center}

Pour plus d'informations sur les fileless threats:
[now-you-see-me-exposing-fileless-malware](https://www.microsoft.com/en-us/security/blog/2018/01/24/now-you-see-me-exposing-fileless-malware/)

