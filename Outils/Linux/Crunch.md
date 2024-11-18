---
title: Crunch
description: Permet de générer des listes de mots en fonction de paramètres comme la longueur, les mots, les caractères ou encore un patron.Permet de générer des listes de mots en fonction de paramètres comme la longueur, les mots, les caractères ou encore un patern.
published: true
date: 2024-11-18T18:38:25.613Z
tags: outil, linux
editor: markdown
dateCreated: 2024-11-18T18:36:06.762Z
---

# Introduction

Crunch permet de générer des listes de mots en fonction de paramètres comme la longueur, les mots, les caractères ou encore un patron.

> Crunch est disponible au téléchargement [ici](https://sourceforge.net/projects/crunch-wordlist/)
{.is-info}

# Syntaxe

`crunch <from-len> <to-len> [-f <path to charset.lst> charset-name] [-o wordlist.txt or START] [-t [FIXED]@@@@] [-s startblock]`

# Paramètres

| Paramètre | Description |
| --------- | ----------- |
| `...`     | ...         |


-b          : maximum bytes to write to output file. depending on the blocksize
 *                files may be some bytes smaller than specified but never bigger.
 *  -c          : numbers of lines to write to output file, only works if "-o START"
 *                is used, eg: 60  The output files will be in the format of starting
 *                letter - ending letter for example:
 *                crunch 1 5 -f /pentest/password/charset.lst mixalpha -o START -c 52
 *                will result in 2 files: a-7.txt and 8-\ .txt  The reason for the
 *                slash in the second filename is the ending character is space and
 *                ls has to escape it to print it.  Yes you will need to put in
 *                the \ when specifying the filename.
 *  -d          : specify -d [n][@,%^] to suppress generation of strings with more
 *                than [n] adjacent duplicates from the given character set. For example:
 *                ./crunch 5 5 -d 2@
 *                Will print all combinations with 2 or less adjacent lowercase duplicates.
 *  -e          : tells crunch to stop generating words at string.  Useful when piping
 *                crunch to another program.
 *  -f          : path to a file containing a list of character sets, eg: charset.lst
 *                name of the character set in the above file eg:
 *                mixalpha-numeric-all-space
 *  -i          : inverts the output so the first character will change very often
 *  -l          : literal characters to use in -t @,%^
 *  -o          : allows you to specify the file to write the output to, eg:
 *                wordlist.txt
 *  -p          : prints permutations without repeating characters.  This option
 *                CANNOT be used with -s.  It also ignores min and max lengths.
 *  -q          : Like the -p option except it reads the strings from the specified
 *                file.  It CANNOT be used with -s.  It also ignores min and max.
 *  -r          : resume a previous session.  You must use the same command line as
 *                the previous session.
 *  -s          : allows you to specify the starting string, eg: 03god22fs
 *  -t [FIXED]@,%^  : allows you to specify a pattern, eg: @@god@@@@
 *                where the only the @'s will change with lowercase letters
 *                the ,'s will change with uppercase letters
 *                the %'s will change with numbers
 *                the ^'s will change with symbols
 *  -u          : The -u option disables the printpercentage thread.  This should be the last option.
 *  -z          : adds support to compress the generated output.  Must be used
 *                with -o option.  Only supports gzip, bzip, lzma, and 7z.

# Exemples

# Voir aussi
