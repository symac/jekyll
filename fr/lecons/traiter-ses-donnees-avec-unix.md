---
title: Analyser ses données de recherche avec Unix
layout: lesson
date: 2014-09-20
authors: 
- James Baker
- Ian Milligan
reviewers:
- Melodee Beals
- Allison Hegel
editors:
- Adam Crymble
translator:
- Sylvain Machefert
translation-editor:
- X
translation-reviewer:
- X
translation_date: 2018-02-05
difficulty: 2
activity: transforming
topics: [data-manipulation]
abstract: "Cette leçon va s'attacher à montrer comment, avec des données clairement organisées, il est possible d'utiliser le terminal pour analyser les données et mieux les comprendre."
previous: bash-intro
redirect_from: /fr/lessons/research-data-with-unix
---

{% include toc.html %}


# XXXXXXXXXXXXXXXXX Counting and mining research data with Unix

## Introduction

Cette leçon va s'attacher à montrer comment, avec des données de recherche organisées selon une structure claire et prédéfinie, peuvent être dénombrées et analysées à l'aide du shell Unix. La leçon se base sur les connaissances apprises dans les leçons "[Preserving Your Research Data: Documenting and Structuring Data](/lessons/preserving-your-research-data)" [en anglais] et l'"[Introduction à la ligne de commande](/fr/lecons/bash-intro)". Si vous disposez des bases concernant le shell Unix, cette leçon peut aussi être envisagée de manière autonome.

Un historien qui reviendra sur ses données de recherche a posteriori, dans le cadre du travail sur un autre projet par exemple, se posera sûrement un certain nombre de questions sur ces données. Si ces données sont réparties en plusieurs fichiers - une série de données tabulées, une transcription d'un texte, une collection d'images - elles peuvent être analysées à l'aide de commandes Unix.

Le shell (ou terminal) Unix vous donne accès à plusieurs commandes puissantes qui peuvent transformer la manière dont vous analysez vos données. Cette leçon, bien qu'elle se contente de gratter la surface du sujet, va vous apprendre plusieurs solutions que le terminal va vous proposer pour analyser vos fichiers. En apprenant simplement quelques options, vous allez pouvoir effectuer des opérations que LibreOffice Calc, Microsoft ou des tableurs équivalents ne vous fourniront qu'au prix d'efforts démesurés. Ces commandes peuvent facilement être adaptées pour des données non tabulées.

Dans cette leçon, vous verrez aussi que les options pour manipuler les fichiers vont aussi dépendre du volume de données auquel vous allez devoir faire face, ainsi que des métadonnées et du texte disponible dans les différents fichiers. Et bien entendu des commandes dont vous aurez connaissance en lien avec le shell. Même si ce n'est pas un prérequis pour travailler avec le shell, prendre le temps de structurer vos données de recherche et réfléchir aux règles de nommage des fichiers, vous fera gagner en efficacité par la suite. Pour des réflexions plus poussées sur ces questions, n'hésitez pas à lire la leçon "[Preserving Your Research Data: Documenting and Structuring Data](../lessons/preserving-your-research-data)" [en anglais].

_____

## Environnement logiciel

Si ce n'est pas déjà fait, les utilisateurs de Windows devront installer Git Bash, les instructions pour cela sont disponibles dans l'[introduction à Bash](/fr/lecons/bash-intro). C'est aussi dans cette leçon que les utilisateurs de Linux et OS X trouveront les instructions pour lancer le terminal, déjà disponible sur leur système.

Cette leçon a été écrite à l'aide de Git Bash 1.9.0 sur Windows 7. Les chemins équivalents pour OS X/Linux ont été fournis autant que possible. Cependant les options et la manière de les appeler peut changer sensiblement entre les sytèmes, les utilisateurs d'OS X et Linux sont donc invités à consulter l'ouvrage de Deborah S. Ray et Eric J. Ray, "[*Unix and Linux: Visual Quickstart Guide*](https://www.worldcat.org/title/unix-and-linux/oclc/308171076&referer=brief_results)", 4th edition (2009) qui couvre en détail les questions d'interopérabilité.

Les fichiers de données utilisés ici sont disponibles sur "[Figshare](http://dx.doi.org/10.6084/m9.figshare.1172094)". Les fichiers proposés contiennent les métadonnées pour les articles affectés à la catégorie 'History' de la base de données British Library ESTAR. Les données sont distribuées sous licence CC0. 

Téléchargez les fichiers, enregistrez les sur votre ordinateur et dézippez les. Si vous n'avez pas de logiciel pour extraire les fichiers .zip, nous vous conseillons [7-zip](http://www.7-zip.org/). Sur Windows, nous vous conseillons de mettre les fichiers sur C:. Le dossier concerné sera donc `c:\proghist\`. N'importe quel autre dossier ferait l'affaire mais dans ce cas là, il faudra adapter les commandes proposées dans cette leçon pour refléter votre choix. Sur OS X et Linux, nous vous recommandons de créer un dossier à la racine de votre dossier utilisateur. Les fichiers de la leçon apparaîtront donc sous `/user/USERNAME/proghist`. Dans tous les cas, l'idée et qu'à l'ouverture du terminal, vous n'ayez qu'à taper `cd proghist` pour vous rendre dans le répertoire de la leçon.

_____

## Dénombrer les fichiers

Nous allons commencer cette leçon en dénombrant le contenu des fichiers à l'aide du shell Unix. Celui-ci peut être utilisé pour compter facilement les informations disponibles dans un ensemble de fichiers, opération difficilement réalisable à l'aide des suites bureautiques classiques. 

Sur Unix, la commande `wc` est utilisée pour compter le contenu d'un fichier ou d'une série de fichiers.

Ouvrez le terminal et naviguez dans le répertoire contenant vos données : le sous-répertoire `data` de `proghist`. Souvenez-vous, il est toujours possible de vérifier que vous êtes dans le bon dossier à l'aide de la commande `pwd`. Et à partir de là, utiliser `cd` pour vous déplacer si besoin. Le chemin pour accéder au bon répertoire va varier selon que vous êtes sur OS X/Linux ou Windows. Dans le premier cas vous aurez quelque chose du style `~/users/USERNAME/proghist/data` et sur Windows cela devrait être `c:\proghist\data`.

Tapez `ls` et appuyez sur entrée. Vous verrez apparaître une liste qui inclut deux fichiers et un sous-dossier. 

Les fichiers de ce dossiers sont les jeux de données `2014-01_JA.csv` qui contient les métadonnées sur les articles et le fichier `2014-01_JA.txt` qui document le contenu de ce fichier .csv.

Le sous-dossier se nomme `derived_data`. It contient quatre fichiers [.tsv](https://fr.wikipedia.org/wiki/Tabulation-separated_values) dérivés de `2014-01_JA.csv`. Chacun de ces fichiers .tsv convient les entrées du fichier source qui contiennent une valeur donnée dans le champ 'Title' (`africa`, `america` ...). Ce répertoire `derived_data` contint aussi une sous-dossier intitulé `results`.

*Note : les fichiers [CSV](http://fr.wikipedia.org/wiki/Comma-separated_values) sont ceux pour lesquels les colonnes sont séparées par des virgules (comma en anglais, comma-separated-values) et les fichiers TSV sont ceux dans lesquels les colonnes sont séparées par des tabulations. Les deux peuvent se lire avec un simple éditeur de texte ou avec un tableau tel que LibreOffice Calc ou Microsoft Excel.*

Avant de commencer, déplacez vous dans le répertoire qui contient les fichiers : `c:\proghist\data\derived_data` sur Windows ou `~/users/USERNAME/proghist/data/derived_data` sur OS X.

Maintenant que vous êtes là, vous pouvez compter ce qui se trouve dans ces fichiers.

La commande Unix pour faire ce type d'analyse est `wc`. Tapez `wc -w 2014-01-31_JA_africa.tsv` et appuyez sur entrée. Le paramètre `-w` associé à la commande `wc` demande à la machine d'afficher le nombre de mots et le nom du fichier dans le terminal.

Comme nous l'avons vu dans la leçon "[Introduction à la ligne de commande avec Bash](bash-intro)", les paramètres tels que `w` sont essentiels pour tirer le meilleur parti des commandes Unix.

Si vous êtes plus intéressés par le nombre d'entrées (ou de lignes) que le nombre de mots, il existe un paramètre "nombre de lignes". Entrez `wc -l 2014-01-31_JA_africa.tsv` et appuyez sur entrée. En combinaison avec `wc`, le paramètre `-l` affiche le nombre de lignes et le nom du fichier.

Pour finir, tapez `wc -c 2014-01-31_JA_africa.tsv` et appuyez sur entrée. Le paramètre `-c` permet d'obtenir le nombre de caractères présents dans le fichier `2014-01-31_JA_africa.tsv`.

*Note : les utilisateurs d'OS X et Linux devront remplacer le paramètre `-c` par `-m`.*

With these three flags, the most obvious thing historians can use `wc` for is to quickly compare the shape of sources in digital format - for example word counts per page of a book, the distribution of characters per page across a collection of newspapers, the average line lengths used by poets. You can also use `wc` with a combination of wildcards and flags to build more complex queries. Type `wc -l 2014-01-31_JA_a*.tsv` and hit enter. This prints the line counts for `2014-01-31_JA_africa.tsv` and `2014-01-31_JA_america.tsv`, offering a simple means of comparing these two sets of research data. Of course, it may be faster to compare the line count for the two documents in Libre Office Calc, Microsoft Excel, or a similar spreadsheet program. But when wishing to compare the line count for tens, hundreds, or thousands of documents, the Unix shell has a clear speed advantage.

Moreover, as our datasets increase in size you can use the Unix shell to do more than copy these line counts by hand, by the use of print screen, or by copy and paste methods. Using the `>` redirect operator you can export your query results to a new file. Type `wc -l 2014-01-31_JA_a*.tsv > results/2014-01-31_JA_a_wc.txt` and hit enter. This runs the same query as before, but rather than print the results within the Unix shell it saves the results as `2014-01-31_JA_a_wc.txt`. By prefacing this with `results/` it moves the .txt file to the `results` sub-directory. To check this, navigate to the `results` subdirectory, hit enter, type `ls`, and hit enter again to see this file listed within `c:\proghist\data\derived_data\results` on Windows or `/users/USERNAME/proghist/data/derived_data/results` on OS X/Linux.

## Mining files

The Unix shell can do much more than count the words, characters, and lines within a file. The `grep` command (meaning 'global regular expression print') is used to search across multiple files for specific strings of characters. It is able to do so much faster than the graphical search interface offered by most operating systems or office suites. And combined with the `>` operator, the `grep` command becomes a powerful research tool can be used to mine your data for characteristics or word clusters that appear across multiple files and then export that data to a new file. The only limitations here are your imagination, the shape of your data, and - when working with thousands or millions of files - the processing power at your disposal.

To begin using `grep`, first navigate to the `derived_data` directory (`cd ..`). Here type `grep 1999 *.tsv` and hit enter. This query looks across all files in the directory that fit the given criteria (the .tsv files) for instances of the string, or character cluster, '1999'. It then prints them within the shell.

*Note: there is a large amount of data to print, so if you get bored hit `ctrl+c` to cancel the action. Ctrl+c is used to cancel any process in the Unix shell.*

Press the up arrow once in order to cycle back to your most recent action. Amend `grep 1999 *.tsv` to `grep -c 1999 *.tsv` and hit enter. The shell now prints the number of times the string 1999 appeared in each .tsv file. Cycle to the previous line again and amend this to `grep -c 1999 2014-01-31_JA_*.tsv > results/2014-01-31_JA_1999.txt` and hit enter. This query looks for instances of the string '1999' across all documents that fit the criteria and saves them as `2014-01-31_JA_1999.txt` in the `results` subdirectory.

Strings need not be numbers. `grep -c revolution 2014-01-31_JA_america.tsv 2014-02-02_JA_britain.tsv`, for example, counts the instances of the string `revolution` within the defined files and prints those counts to the shell. Run this and then amend it to `grep -ci revolution 2014-01-31_JA_america.tsv 2014-02-02_JA_britain.tsv`. This repeats the query, but prints a case insensitive count (including instances of both `revolution` and `Revolution`). Note how the count has increased nearly 30 fold for those journal article titles that contain the keyword 'revolution'. As before, cycling back and adding `> results/`, followed by a filename (ideally in .txt format), will save the results to a data file.

You can also use `grep` to create subsets of tabulated data. Type `grep -i revolution 2014-01-31_JA_america.tsv 2014-02-02_JA_britain.tsv > YEAR-MONTH-DAY_JA_america_britain_i_revolution.tsv` (where `YEAR-MONTH-DAY` is the date you are completing this lesson) and hit enter. This command looks in both of the defined files and exports any lines containing `revolution` (without regard to case) to the specified .tsv file.

The data has not been saved to to the `results` directory because it isn't strictly a result; it is derived data. Depending on your research project it may be easier to save this to another subdirectory. For now have a look at this file to verify its contents and when you are happy, delete it using the `rm` command. *Note: the `rm` common is very powerful and should be used with caution. Please refer to "[Introduction to the Bash Command Line](../lessons/intro-to-bash)" for instructions on how to use this command correctly.*

Finally, you can use another flag, `-v`, to exclude data elements when using the `grep` command. Type `grep -iv revolution 2014*_JA_a*.tsv > 2014_JA_iv_revolution.csv` and hit enter. This query looks in the defined files (three in total) and exports all lines that do not contain `revolution` or `Revolution` to `c:\proghist\data\derived_data\2014_JA_iv_revolution.csv`.

Note that you have transformed the data from one format to another - from .tsv to .csv. Often there is a loss of data structure when undertaking such transformations. To observe this for yourself, run `grep -iv revolution 2014*_JA_a*.tsv > 2014_JA_iv_revolution.tsv` and open both the .csv and .tsv files in Libre Office Calc, Microsoft Excel, or a similar spreadsheet program. Note the differences in column delineation between the two files.

*Summary*

Within the Unix shell you can now:

- use the `wc` command with the flags `-w` and `-l` to count the words and lines in a file or a series of files.
- use the redirector and structure `> subdirectory/filename` to save results into a subdirectory.
- use the `grep` command to search for instances of a string.
- use with `grep` the `-c` flag to count instances of a string, the `-i` flag to return a case insensitive search for a string, and the `-v` flag to exclude a string from the results.
- combine these commands and flags to build complex queries in a way that suggests the potential for using the Unix shell to count and mine your research data and research projects.

_____

#### Conclusion

In this lesson you have learnt to undertake some basic file counting, to query across research data for common strings, and to save results and derived data. Though this lesson is restricted to using the Unix shell to count and mine tabulated data, the processes can be easily extended to free text. For this we recommend two guides written by William Turkel:

- William Turkel, '[Basic Text Analysis with Command Line Tools in Linux](http://williamjturkel.net/2013/06/15/basic-text-analysis-with-command-line-tools-in-linux/)' (15 June 2013)  
- William Turkel, '[Pattern Matching and Permuted Term Indexing with Command Line Tools in Linux](http://williamjturkel.net/2013/06/20/pattern-matching-and-permuted-term-indexing-with-command-line-tools-in-linux/)' (20 June 2013)  

As these recommendations suggest, the present lesson only scratches the surface of what the Unix shell environment is capable of. It is hoped, however, that this lesson has provided a taster sufficient to prompt further investigation and productive play. 

For many historians, the full potential of these tools may only emerge upon embedding these skills into a real research project. Once your research grows, and, with it, your research data, being able to manipulate, count and mine thousands of files will be extremely useful. For if you choose to build on this lesson and investigate the Unix shell further you will find that even a large collection of files which do not contain any alpha-numeric data elements, such as image files, can be easily sorted, selected and queried in the Unix shell.
