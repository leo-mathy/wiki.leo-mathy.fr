---
title: guestmount
description: Monte des systèmes de fichiers de machines virtuelles ou des images sur l'hôte.
published: true
date: 2024-10-26T18:41:21.964Z
tags: outil, linux
editor: markdown
dateCreated: 2024-10-26T18:41:21.964Z
---

# Introduction

guestmount permet de monter des systèmes de fichiers de machines virtuelles ou des images sur l'hôte.

# Syntaxe

`guestmount [paramètres] -a <image disque> [-m périphérique] [--ro] <point de montage>`

# Paramètres

| Paramètre                                                                          | Description                                                                                                                                               |
| ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-a <image/URI>, --add <image/URI>`                                                | Ajoute un disque ou une image de machine virtuelle depuis un emplacement local ou distant(via une URI). Le format est détecté automatiquement par défaut. |
| `--blocksize, --blocksize=<taille du bloc>`                                        | Spécifie la taille du secteur pour l'image disque. Par défaut, la taille est détectée automatiquement.                                                    |
| `-c <URI>, --connect <URI>`                                                        | Précise l'emplacement URI de libvirt à utiliser.                                                                                                          |
| `-d <domaine libvirt/UUID du domaine>, --domain <domaine libvirt/UUID du domaine>` | Ajoute les disques depuis le domaine libvirt indiqué.                                                                                                     |
| `--dir-cache-timeout <secondes>`                                                   | Défini le temps de timeout du cache readdir. 60 secondes par défaut.                                                                                      |
| `--echo-keys`                                                                      | Affiche les touches tapées lors des demandes de clés ou mots de passe.                                                                                    |
| `--fd=<Descripteur de fichier>`                                                    | Spécifie un canal ou eventfd comme descripteur de fichier.                                                                                                |
| `--format, --format=<format>`                                                      | Spécifie le format de l'image. Si aucune valeur n'est entrée alors le format est détecté automatiquement (par défaut).                                    |
| `--fuse-help`                                                                      | Affiche l'aide pour les options FUSE.                                                                                                                     |
| `--help`                                                                           | Affiche l'aide.                                                                                                                                           |
| `-i, --inspector`                                                                  | Inspecte les disques pour afficher des systèmes d'exploitation ou des systèmes de fichiers.                                                               |
| `--key <selecteur>`                                                                | Utilisé pour spécifier une clé pour LUKS (chiffrement des partitions).                                                                                    |
| `--keys-from-stdin`                                                                | Lis les clés ou mots de passe depuis le stdin.                                                                                                            |
| `-m périphérique[:point de montage[:options[:fstype]]]`                            | Précise le point de montage et le volume logique ainsi que les options (par exemple: -m /dev/sda1:/:acl,user_xattr).                                      |
| `--no-fork`                                                                        | Ne fait pas tourner guestmount en arrière-plan (en tant que daemon).                                                                                      |
| `-n, --no-sync`                                                                    | Ne synchronise pas le disque lorsque le point de montage FUSE est démonté.                                                                                |
| `-o <option>, --option <option>`                                                   | Passe des options à FUSE.                                                                                                                                 |
| `--pid-file <nom du fichier>`                                                      | Entre le PID du processus guestmount vers un fichier.                                                                                                     |
| `-r, --ro`                                                                         | Ajoute les périphériques et monte tout en mode lecture seule.                                                                                             |
| `--selinux`                                                                        | Paramètre obsolète présent pour la rétrocompatibilité.                                                                                                    |
| `-v, --verbose`                                                                    | Active le mode verbose.                                                                                                                                   |
| `-V, --version`                                                                    | Affiche la version de guestmount.                                                                                                                         |
| `-w, --rw`                                                                         | Ajoute les périphériques et monte tout en mode lecture/écriture.                                                                                          |
| `-x, --trace`                                                                      | Trace les appels de libguestfs dans chaque fonction FUSE.                                                                                                 |

# Exemples

Monte le disque SRV-TEST.vmdk vers /mnt/vmdk en lecture seule. Et inspecte celui-ci.
`guestmount --add SRV-TEST.vmdk -i --ro /mnt/vmdk`

Monte la partition /dev/sda1 du disque SRV-TEST.vhdx vers /mnt/vmdk en lecture seule.
`guestmount --add SRV-TEST.vhdx  --ro /mnt/vhdx/ -m /dev/sda1`

# Voir aussi

Documentation officielle
https://libguestfs.org/guestmount.1.html
