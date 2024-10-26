---
title: psexec
description: Outil de la suite Impacket. Ouvrir une connexion comme avec le psexec officiel...
published: true
date: 2024-10-26T16:06:48.972Z
tags: outil, rédaction incomplète, indépendant
editor: markdown
dateCreated: 2024-10-26T16:06:48.972Z
---

# Introduction
https://github.com/fortra/impacket/blob/master/examples/psexec.py

>  [lien](https://leo-mathy.fr)
{.is-info}

    parser.add_argument('target', action='store', help='[[domain/]username[:password]@]<targetName or address>')
    parser.add_argument('command', nargs='*', default = ' ', help='command (or arguments if -c is used) to execute at '
                                                                  'the target (w/o path) - (default:cmd.exe)')
    parser.add_argument('-c', action='store',metavar = "pathname",  help='copy the filename for later execution, '
                                                                         'arguments are passed in the command option')
    parser.add_argument('-path', action='store', help='path of the command to execute')
    parser.add_argument('-file', action='store', help="alternative RemCom binary (be sure it doesn't require CRT)")
    parser.add_argument('-ts', action='store_true', help='adds timestamp to every logging output')
    parser.add_argument('-debug', action='store_true', help='Turn DEBUG output ON')
    parser.add_argument('-codec', action='store', help='Sets encoding used (codec) from the target\'s output (default '
                                                       '"%s"). If errors are detected, run chcp.com at the target, '
                                                       'map the result with '
                          'https://docs.python.org/3/library/codecs.html#standard-encodings and then execute smbexec.py '
                          'again with -codec and the corresponding codec ' % CODEC)

    group = parser.add_argument_group('authentication')

    group.add_argument('-hashes', action="store", metavar = "LMHASH:NTHASH", help='NTLM hashes, format is LMHASH:NTHASH')
    group.add_argument('-no-pass', action="store_true", help='don\'t ask for password (useful for -k)')
    group.add_argument('-k', action="store_true", help='Use Kerberos authentication. Grabs credentials from ccache file '
                       '(KRB5CCNAME) based on target parameters. If valid credentials cannot be found, it will use the '
                       'ones specified in the command line')
    group.add_argument('-aesKey', action="store", metavar = "hex key", help='AES key to use for Kerberos Authentication '
                                                                            '(128 or 256 bits)')
    group.add_argument('-keytab', action="store", help='Read keys for SPN from keytab file')

    group = parser.add_argument_group('connection')

    group.add_argument('-dc-ip', action='store', metavar="ip address",
                       help='IP Address of the domain controller. If omitted it will use the domain part (FQDN) specified in '
                            'the target parameter')
    group.add_argument('-target-ip', action='store', metavar="ip address",
                       help='IP Address of the target machine. If omitted it will use whatever was specified as target. '
                            'This is useful when target is the NetBIOS name and you cannot resolve it')
    group.add_argument('-port', choices=['139', '445'], nargs='?', default='445', metavar="destination port",
                       help='Destination port to connect to SMB Server')
    group.add_argument('-service-name', action='store', metavar="service_name", default = '', help='The name of the service'
                                                                                ' used to trigger the payload')
    group.add_argument('-remote-binary-name', action='store', metavar="remote_binary_name", default = None, help='This will '
                                                            'be the name of the executable uploaded on the target')

# Syntaxe

`...`

# Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `...`     | ...         |

# Exemples

# Voir aussi
