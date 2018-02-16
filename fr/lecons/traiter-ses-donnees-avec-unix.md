---
title: Analyser ses données de recherche avec le terminal
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


# Analyser ses données avec le terminal

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

Si vous êtes davantage intéressés par le nombre d'entrées (ou de lignes) que le nombre de mots, il existe un paramètre "nombre de lignes". Entrez `wc -l 2014-01-31_JA_africa.tsv` et appuyez sur entrée. En combinaison avec `wc`, le paramètre `-l` affiche le nombre de lignes et le nom du fichier.

Pour finir, tapez `wc -c 2014-01-31_JA_africa.tsv` et appuyez sur entrée. Le paramètre `-c` permet d'obtenir le nombre de caractères présents dans le fichier `2014-01-31_JA_africa.tsv`.

*Note : les utilisateurs d'OS X et Linux devront remplacer le paramètre `-c` par `-m`.*

Une fois connus ces trois paramètres, le chercheur pourra utiliser la commande `wc` pour comparer facilement le contenu de différentes sources disponibles au format numérique - par exemple le nombre de mots par page dans un livre, la distribution du nombre de caractères par page dans une collection de journaux ou encore la taille moyenne des vers d'un poète. Il est aussi possible d'utiliser `wc` en combinant plusieurs paramètres et en utilisant des caractères joker. Si vous tapez par exemple la commande `wc -l 2014-01-31_JA_a*.tsv`, vous obtiendrez le nombre de lignes dans les fichiers `2014-01-31_JA_africa.tsv` et `2014-01-31_JA_america.tsv` et pourrez ainsi facilement comparer ces deux jeux de données. Vous pouvez bien entendu faire la même chose pour ces deux fichiers avec LibreOffice Calc, Microsoft Excel ou n'importe quel tableur, mais si vous devez comparer des centaines ou des milliers de documents, vous comprendrez rapidement que le terminal présent de grands avantages.

De plus, si les jeux de données augmentent, vous pourrez utiliser le terminal et être plus efficace qu'en copiant / collant à la main les résultats ou en faisant une capture d'écran. En utilisant le signe de redirection `>` vous pouvez exporter les résultats dans un nouveau fichier. En tapant `wc -l 2014-01-31_JA_a*.tsv > results/2014-01-31_JA_a_wc.txt` vous effectuerez la même commande que précédemment mais au lieu d'afficher les résultats dans le terminal, ils seront enregistrés dans le fichier `2014-01-31_JA_a_wc.txt`. Le préfixe `results/` implique que le fichier créé le sera dans le sous-répertoire `results`. Pour vérifier cela, déplacez vous dans le répertoire `results` puis tapez `ls` pour voir les fichiers qui se trouvent dans ce dossier (`c:\proghist\data\derived_data\results` sur Windows ou `/users/USERNAME/proghist/data/derived_data/results` su OS X/Linux).

## Analyser les fichiers

Le terminal peut faire bien plus que compter des mots, caractères ou lignes dans un fichier. La commande `grep` (pour `global regular expression print`) permet de chercher à travers plusieurs fichiers une chaîne de caractères. Grep permet de faire ces recherches de manière beaucoup plus efficace qu'avec les outils fournis par l'interface graphique de votre système d'exploitation. En la combinant avec l'opérateur `>`, la commande `grep` peut-être devenir un puissant outil d'analyse pour identifier les caractéristiques du texte ou identifier des regroupements de mots apparaissant dans plusieurs fichiers. La seule limitation est ici votre imagination, la forme des données, et - si vous devez travailler sur des milliers ou des millions de fichiers - la puissance de calcul à votre disposition. 

Pour commencer à utiliser `grep`, commencez à vous placer dans le dossier `derived_data` (`cd ..`). Ici, tapez `grep 1999 *.tsv` et appuyez sur entrée. Cette requête va chercher dans l'ensemble des fichiers correspondant au modèle (les fichiers .tsv) les occurences de la chaîne passée en paramètre : '1999'. Les lignes qui correspondent sont affichées dans le terminal.

*Note : étant donné qu'un certains nombre de lignes correspondent à la recherche, si vous vous lassez de voir défiler les résultats à l'écran, appuyez sur `ctrl+c` pour annuler l'action. Ctrl+c est le raccourci à utiliser dans le terminal pour terminer le processus en cours.*

Pressez maintenant sur la flèche "haut" pour remonter à l'action précédente. Remplacez `grep 1999 *.tsv` par `grep -c 1999 *.tsv` et appuyez sur entrée. Le terminal va maintenant afficher le nombre de fois où le terme 1999 apparaît dans chaque fichier .tsv. Remontez à nouveau à l'instruction précédente et remplacez la par : `grep -c 1999 2014-01-31_JA_*.tsv > results/2014-01-31_JA_1999.txt`avant d'appuyer sur entrée. Cette commande va rechercher les occurences de '1999' dans les fichiers tsv sur dossier et enregistré les résultats dans le fichier `2014-01-31_JA_1999.txt` sur répertoire `results`.


Dans les exemples précédents on a cherché un nombre, mais la commande grep s'applique à tous les types de chaînes de caractères. `grep -c revolution 2014-01-31_JA_america.tsv 2014-02-02_JA_britain.tsv` va par exemple chercher toutes les occurences du mot 'revolution' dans les fichiers passés en paramètre. Après avoir essayé cette commande, remplacez la par `grep -ci revolution 2014-01-31_JA_america.tsv 2014-02-02_JA_britain.tsv`. Cette nouvelle commande va effectuer une recherche insensible à la casse, et retourner les lignes qui contiennent `revolution` mais aussi `Revolution`, soit 30 fois plus de résultats dans le cas présent. Comme tout à l'heure, on peut enregistrer le résultat en ajoutant `> results/` suivi d'un nom de fichier.

Combiné avec le paramètre `-c` grep nous a permis de faire des comptages dans les fichiers mais la commande peut aussi être utilisée pour créer des sous-corpus. Tapez `grep -i revolution 2014-01-31_JA_america.tsv 2014-02-02_JA_britain.tsv > ANNNEE-MOIS-JOUR_JA_america_britain_i_revolution.tsv` (where `ANNEE-MOIS-JOUR` correspond à la date à laquelle vous effectuez l'opération) et appuyez sur entrée. Cette commande va isoler les lignes contenant 'revolution' (ou 'Revolution', 'REVOLUTION' et toutes les combinaisons de casse possible) et les enregistrer dans le fichier .tsv daté du jour.

Nous n'avons pas enregistré ce nouveau fichier dans le répertoire `results` car ce n'est pas un résultat à proprement parler mais plutôt un fichier dérivé. Selon votre méthode de travail vous souhaiterez peut-être sauver ces fichiers dérivés dans un dossier spécifique. Pour le moment, vérifiez que le fichier correspond bien à vos attentes et si c'est bon, vous pouvez le supprimer à l'aide de la commande `rm`. *Note : la commande `rm` est très puissant et doit être utilisée avec prudence. Consultez l'"[introduction à Bash](bash-intro)" pour comprendre comment l'utiliser au mieux.*

Un autre paramètre utile de la commande `grep` est `v` qui permet d'exclure certaines lignes d'un résultat. Par exemple `grep -iv revolution 2014*_JA_a*.tsv > 2014_JA_iv_revolution.csv` va regarder dans les trois fichiers correspondant au schéma proposé (`2014-01-31_JA_africa.tsv, `2014-02-01_JA_art.tsv` et `2014-01-31_JA_america.tsv` mais pas `2014-02-02_JA_britain.tsv` car on demande les fichiers dans lesquels le mot après JA_ commence par un a) les lignes qui ne contiennent par `revolution` ou `Revolution`. Le résultat est enregistré dans `c:\proghist\data\derived_data\2014_JA_iv_revolution.csv` (sur Windows, ou le chemin correspondant sur un autre système).

Vous noterez dans cette dernière opération que l'on a choisi d'exporter les données dans un fichier .csv plutôt que .tsv. S'il ne change pas le contenu du fichier car `grep` se contente de recopier les lignes qui correspond au schéma choisi, cette différence d'extension risque d'avoir une influence sur la manière dont d'autres programmes vont comprendre le document. Lancez la même commande que précédemment en sauvant les résultats en .tsv (`grep -iv revolution 2014*_JA_a*.tsv > 2014_JA_iv_revolution.tsv`), vous aurez donc deux fichiers identiques à l'exception de l'extension. Si vous ouvrez ces deux fichiers dans un tableur, ce dernier cherchera un délimiteur de colonnes différents selon l'extension et le résultat à l'affichage risque de ne pas correspondre à vos attentes, selon le délimiteur effectivement utilisé dans le fichier.

*Résumé*

Avec le terminal vous savez désormais :

- utiliser la commande `wc` avec les paramètres `-w` et `-l` pour compter mots et lignes à l'intérieur d'un fichier ou d'une série de fichiers;
- utiliser les redirections et leur forme `> subdirectory/filename` pour enregistrer des résultats dans un sous-dossier; 
- utiliser la commande `grep` pour rechercher des chaînes de caractères;
- utiliser la commande `grep` avec les paramètres `-c` pour compter les occurences d'une chaîne, `i` pour faire une recherche non sensible à la casse et `v` pour exclure certaines chaînes de résultats.
- combiner ces commandes et leurs paramètres pour construire des requêtes complexes qui vous permettront de commencer à utiliser au mieux le potentiel du terminal pour analyser vos fichiers.

_____

#### Conclusion

À travers cette leçon, vous avez appris quelques bases pour analyser des fichiers et enregistrer les résultats. Nous nous sommes contentés ici d'exemples sur des fichiers tabulés mais ces fonctions peuvent être utilisés sur n'importe quel fichier texte, y-compris pour du texte libre. Pour cela, nous vous recommandons deux guides rédigés par William Turkel (en anglais) : 

- William Turkel, '[Basic Text Analysis with Command Line Tools in Linux](http://williamjturkel.net/2013/06/15/basic-text-analysis-with-command-line-tools-in-linux/)' (15 June 2013)  
- William Turkel, '[Pattern Matching and Permuted Term Indexing with Command Line Tools in Linux](http://williamjturkel.net/2013/06/20/pattern-matching-and-permuted-term-indexing-with-command-line-tools-in-linux/)' (20 June 2013)  

Cette leçon se contente de survoler les possibilités offertes par le terminal dans l'analyse de fichiers, en espérant vous donner envie d'aller plus loin pour devenir pleinement efficace dans cet environnement.

C'est en intégrant ces outils à un projet de recherche concret, dans lequel les résultats s'accumulant, il deviendra primordial de pouvoir manipuler des milliers de fichiers à la fois. Si vous continuez à vous renseigner sur ces outils, vous verrez que même si vous devez travailler sur des fichiers ne contenant pas d'information textuelle (des images par exemple), le terminal vous permettra de les rechercher, de faire des tris, etc.