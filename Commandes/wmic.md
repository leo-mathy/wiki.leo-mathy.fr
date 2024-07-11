---
title: wmic
description: Windows Management Instrumentation Command-line (WMIC) est un système de gestion interne de Windows qui permet de contrôler et surveiller les ressources systèmes
published: true
date: 2024-07-11T11:45:10.201Z
tags: cmd, windows
editor: markdown
dateCreated: 2024-07-11T11:35:49.137Z
---

# Introduction

Windows Management Instrumentation Command-line (WMIC) est un système de gestion interne de Windows qui permet de contrôler et surveiller les ressources systèmes. Il est possible d'utilser cette commande pour obtenir des informations accessibles sous forme d'alias.

# Syntaxe

`wmic [alias] [options]`

# Alias

| ALIAS               | Accès aux alias disponibles sur l'ordinateur local                                                                        |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| BASEBOARD           | Gestion de la carte de base (également appelée carte mère ou carte système).                                              |
| BIOS                | Gestion des services d'entrées/sorties (E/S) de base (BIOS).                                                              |
| BOOTCONFIG          | Gestion de la configuration du démarrage.                                                                                 |
| CDROM               | Gestion des CD-ROM.                                                                                                       |
| COMPUTERSYSTEM      | Gestion de systèmes informatiques.                                                                                        |
| CPU                 | Gestion du processeur.                                                                                                    |
| CSPRODUCT           | Informations sur l'ordinateur issues du SMBIOS.                                                                           |
| DATAFILE            | Gestion des fichiers de données.                                                                                          |
| DCOMAPP             | Gestion d'applications.                                                                                                   |
| DESKTOP             | Gestion du Bureau de l'utilisateur.                                                                                       |
| DESKTOPMONITOR      | Gestion du moniteur de bureau.                                                                                            |
| DEVICEMEMORYADDRESS | Gestion des adresses mémoire pour périphériques.                                                                          |
| DISKDRIVE           | Gestion des disques durs physiques.                                                                                       |
| DISKQUOTA           | Gestion de l'utilisation de l'espace disque sur les volumes NTFS.                                                         |
| DMACHANNEL          | Gestion du canal DMA (Accès direct à la mémoire).                                                                         |
| ENVIRONMENT         | Gestion des paramètres d'environnement système.                                                                           |
| FSDIR               | Gestion des entrées de répertoires du système de fichiers.                                                                |
| GROUP               | Gestion des comptes de groupes.                                                                                           |
| IDECONTROLLER       | Gestion de contrôleurs IDE.                                                                                               |
| IRQ                 | Gestion des requêtes d'interruption (IRQ).                                                                                |
| JOB                 | Permet l'accès aux tâches planifiées à l'aide du service de planification.                                                |
| LOADORDER           | Gestion des services système définissant les dépendances d'exécution.                                                     |
| LOGICALDISK         | Gestion des périphériques de stockage locaux.                                                                             |
| LOGON               | Sessions LOGON.                                                                                                           |
| MEMCACHE            | Gestion de la mémoire cache.                                                                                              |
| MEMORYCHIP          | Informations sur la puce mémoire.                                                                                         |
| MEMPHYSICAL         | Gestion de la mémoire physique d'un ordinateur.                                                                           |
| NETCLIENT           | Gestion des clients réseau.                                                                                               |
| NETLOGIN            | Gestion des informations d'ouverture de session réseau (d'un utilisateur précis).                                         |
| NETPROTOCOL         | Gestion des protocoles et de leurs caractéristiques réseau.                                                               |
| NETUSE              | Gestion des connexion réseau actives.                                                                                     |
| NIC                 | Gestion des contrôleurs réseau NIC (Network Interface Controller).                                                        |
| NICCONFIG           | Gestion des cartes réseau.                                                                                                |
| NTDOMAIN            | Gestion de l'arborescence du domaine.                                                                                     |
| NTEVENT             | Entrées dans le journal d'événements NT.                                                                                  |
| NTEVENTLOG          | Gestion du fichier journal d'événements NT.                                                                               |
| ONBOARDDEVICE       | Gestion des périphériques carte communs intégrés dans la carte mère.                                                      |
| OS                  | Gestion des systèmes d'exploitation installés.                                                                            |
| PAGEFILE            | Gestion des paramètres du fichier d'échange de mémoire virtuelle.                                                         |
| PAGEFILESET         | Gestion des paramètres de fichier d'échange.                                                                              |
| PARTITION           | Gestion des zones partitionnées d'un disque physique.                                                                     |
| PORT                | Gestion des ports d'E/S.                                                                                                  |
| PORTCONNECTOR       | Gestion des ports de connexion physique.                                                                                  |
| PRINTER             | Gestion des périphériques d'impression.                                                                                   |
| PRINTERCONFIG       | Gestion de la configuration des périphériques d'impression.                                                               |
| PRINTJOB            | Gestion des travaux d'impression.                                                                                         |
| PROCESS             | Gestion des processus.                                                                                                    |
| PRODUCT             | Gestion des tâches des packages d'installation.                                                                           |
| QFE                 | Ingénierie de correctifs à chaud.                                                                                         |
| QUOTASETTING        | Gestion des informations de quotas de disque sur un volume.                                                               |
| RDACCOUNT           | Gestion d'autorisation de connexion du Bureau distant.                                                                    |
| RDNIC               | Gestion de connexion du Bureau distant sur une carte réseau spécifique.                                                   |
| RDPERMISSIONS       | Autorisations pour une connexion du Bureau distant spécifique.                                                            |
| RDTOGGLE            | Active ou désactive à distance l'écoute du Bureau distant.                                                                |
| RECOVEROS           | Informations recueillies en mémoire en cas de dysfonctionnement du système d'exploitation.                                |
| REGISTRY            | Gestion du Registre système.                                                                                              |
| SCSICONTROLLER      | Gestion de contrôleurs SCSI.                                                                                              |
| SERVER              | Gestion des informations sur le serveur.                                                                                  |
| SERVICE             | Gestion des applications de services.                                                                                     |
| SHADOWCOPY          | Gestion des clichés instantanés.                                                                                          |
| SHADOWSTORAGE       | Gestion de la zone de stockage des copies shadow.                                                                         |
| SHARE               | Gestion des ressources partagées.                                                                                         |
| SOFTWAREELEMENT     | Gestion des éléments d'un logiciel installé sur un ordinateur.                                                            |
| SOFTWAREFEATURE     | Gestion des logiciels sous-ensembles de SoftwareElement.                                                                  |
| SOUNDDEV            | Gestion des périphériques audio.                                                                                          |
| STARTUP             | Gestion des commandes qui s'exécutent dès que l'utilisateur ouvre une session sur l'ordinateur.                           |
| SYSACCOUNT          | Gestion des comptes système.                                                                                              |
| SYSDRIVER           | Gestion du pilote système pour un service de base.                                                                        |
| SYSTEMENCLOSURE     | Gestion de la mise en armoire du système.                                                                                 |
| SYSTEMSLOT          | Gestion de des points de connexion physiques : ports, connecteurs et périphériques, et points de connexion propriétaires. |
| TAPEDRIVE           | Gestion de lecteurs de bandes.                                                                                            |
| TEMPERATURE         | Gestion d'un capteur de température (thermomètre électronique).                                                           |
| TIMEZONE            | Gestion des données de fuseau horaire.                                                                                    |
| UPS                 | Gestion de l'alimentation de secours (UPS).                                                                               |
| USERACCOUNT         | Auditer la gestion des comptes.                                                                                           |
| VOLTAGE             | Gestion des données de capteurs de tension (tensiomètre électronique).                                                    |
| VOLUME              | Gestion des volumes de stockage locaux.                                                                                   |
| VOLUMEQUOTASETTING  | Associe le paramètre de quota de disque à un volume précis.                                                               |
| VOLUMEUSERQUOTA     | Gestion de quota de volume de stockage par utilisateur.                                                                   |
| WMISET              | Gestion des paramètres opérationnels du service WMI.                                                                      |

# Options

| Option                       | Description             |
| ---------------------------- | ----------------------- |
| `/namespace:[espace de nom]` | Change l'espace de nom. |
| `GET [propriété]` | Récupère une propriété particulière |

> Par défaut, l'espace de nom s’agit de "root\cimv2"
> {.is-info}

# Exemples

Pour obtenir les informations concernant les mises à jour de Windows

`wmic qfe`

Récupérer le nom des produits installés

`wmic product get name`
