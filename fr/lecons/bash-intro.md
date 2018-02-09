---
title: Introduction à la ligne de commande avec Bash
layout: lesson
date: 2014-09-20
authors: 
- Ian Milligan
- James Baker
reviewers:
- Melodee Beals
- Allison Hegel
- Charlotte Tupman
editors:
- Adam Crymble
translator:
- Sylvain Machefert
translation-editor:
- X
translation-reviewer:
- X
translation_date: 2018-02-05
difficulty: 1
activity: transforming
topics: [data-manipulation, get-ready]
abstract: "Cette leçon va vous expliquer comment transmettre des commandes à l'ordinateur à l'aide d'une interface en ligne de commande plutôt qu'avec une interface graphique. Les interfaces en ligne de commande présentent plusieurs avantages pour les utilisateurs ayant des besoins précis et peuvent ainsi être utiles dans le cadre des humanités numériques. Ces interfaces en ligne de commande permettent de préciser certaines actions à l'aide de paramètres passés au programme. Enfin, ces outils ont pour avantage de pouvoir être automatisés à l'aide de scripts."
next: research-data-with-unix
redirect_from: /fr/lessons/intro-to-bash
---

{% include toc.html %}

# Introduction à la ligne de commande en Bash

## Introduction

De nombreuses leçons de *Programming Historian* impliquent que vous saisissiez des commandes à travers une *interface en ligne de commande*, en opposition avec l'habitude la plus courante aujoud'hui qui passe par des *interfaces graphiques*, ou GUI (Graphical User Interface). Cela signifie que pour entrer dans un dossier, vous cliquez sur l'image d'un dossier, pour exécuter un programme, vous double-cliquez sur son icône, pour naviguer sur le web, la souris vous permet d'interagir avec les éléments de la page. Avant l'émergence des interfaces graphiques à la fin des années 80, la principale manière de communiquer avec l'ordinateur était la ligne de commande.

{% include figure.html filename="GUI.png" caption="Interface graphique disponible sur l'ordinateur d'une chercheur (Ian Milligan)" %}

Les interfaces en ligne de commande présentent plusieurs avantages pour les utilisateurs qui ont besoin d'effectuer des opérations précises dans le cadre de leur travail. Elles permettent, à l'aide de paramètres, de définir préciséments les traitements à effectuer ou d'obtenir des informations détaillées sur les résultats de ces traitements. De plus, elles peuvent facilement être automatisées à l'aide de [scripts](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/chap_01.html).

Il existe principalement deux interfaces principales pour la ligne de commande, aussi appelées 'shells', utilisées dans les humanités numériques. Sur OS X et plusieurs distributions Linux, le shell utilisé est `bash` ('Bourne-again shell'). Les utilisateurs de Windows disposent par défaut d'un shell `basé sur MS-DOS`, qui utilise des commandes et une syntaxe différentes mais permet de résoudre des problèmes similaires. Ce tutoriel propose une introduction à `bash`, les utilisateurs Windows pourront facilement suivre les instructions données en utilisant un shell proche de bash et disponible sur Windows tel que [Cygwin](https://www.cygwin.com/) ou Git Bash (voir plus bas).

Cette leçon utilise un **[shell Unix](https://fr.wikipedia.org/wiki/Shell_Unix)**, un interpréteur de ligne de commandes qui offre une interface utilisateur sur Unix et les sytèmes associés. À la fin de cette leçon, vous serez capable de naviguer dans l'arborescence de documents de votre machine, trouver des fichiers, les ouvrir et effectuer des opérations de base telles que copier et combiner des fichiers, les lire et y effectuer des modifications de base. Ces commandes constituent la base sur laquelle des commandes plus complexes pourront être construites pour mener à bien vos projets de recherche. Le lecteur intéressé par une approche plus approfondie du sujet, pourra se diriger vers Deborah S. Ray et Eric J. Ray, *Unix and Linux: Visual Quickstart Guide*, 4ème édition (2009).

## Pour les utilisateurs de Windows : Installation de Git Bash

Si vous utilisez OS X ou la plupart des distributions Linux, vous avez de la chance, le shell bash est déjà disponible. Si vous êtes sur Windows, il vous reste une petite manipulation à faire en installant Git Bash en téléchargeant le fichier d'installation sur [cette page](https://git-for-windows.github.io/).

## Ouvrir le shell

Commençons par démarrer le shell. Sur Windows, exécutez Git Bash depuis le répertoire d'installation. Vous devrez le démarrer en tant qu'administrateur. Pour cela, faites un clic droit et choisissez "Exécuter en tant qu'administrateur". Sur OS X, le shell est par défaut disponible dans : 

`Applications -> Utilitaires -> Terminal` 

{% include figure.html filename="Terminal.png" caption="Le programme Terminal.app sur OS X" %}

En le lançant, vous verrez cette fenêtre.

{% include figure.html filename="Blank-Terminal.png" caption="Écran de terminal vide sur un poste de travail OS X" %}

Vous aurez peut-être envie de modifier l'apparence visuel de ce terminal pour éviter de vos fatiguer les yeux sur du texte noir sur fond blanc. Dans l'application par défaut sur OS X, vous pouvez ouvrir les préférences dans le menu paramètres du terminal. Cliquez sur l'onglet "Profils" et choisissez un nouveau mode de couleur. Les auteurs de cet article privilégient des palettes avec un contraste moins marqué entre arrière-plan et premier plan. 'Novel' répond assez bien à ces exigences, tout comme les populaires [Solarized](http://ethanschoonover.com/solarized). Sur Windows un effet similaire peut être réalisé à l'aide de l'onglet `propriétés` de Git Bash. Pour y accéder, faites un clic droit n'importe où dans la fenêtre et choisissez `Propriétés`.

{% include figure.html filename="Settings.png" caption="Sélection d'un profil dans le shell d'OS X" %}

Dès que votre interface correspond à vos attentes, passez à la suite.

## Se déplacer dans l'arborescende de son système

Lorsque vous ouvrez le terminal, si vous n'êtes pas sûr de l'emplacement dans lequel vous vous trouvez sur le disque dur, la première étape est donc de l'identifier. La commande permettant de le faire est `pwd`, le sigle pour "Print Working Directory" (Afficher le répertoire de travail). Essayez donc de saisir : 

`pwd`

puis taper sur la touche entrée. Si vous êtes sur OS X ou Linux, vous verrez sûrement quelque chose comme `/users/UTILISATEUR` avec votre login à la place d'UTILISATEUR. Par exemple sur le poste de Ian : `/users/ianmilligan1/`.

Dès cette première étape, on observera des différences entre les utilisateurs sur OS X/Linux et ceux sous Windows. Pour ces derniers, le résultat de la commande donnera quelque chose comme : 

`c/users/jbaker`

Il existe quelques petites différences de ce type mais ne vous inquiétez pas, dès que vous commencerez à déplacer et manipuler des fichiers, ces variations deviendront assez annexes.

Pour mieux se repérer, poursuivons en identifiant les fichiers qui se trouvent dans le répertoire courant. Tapez : 

`ls`

et en tapant sur la touche entrée vous verrez une liste des fichiers qui se trouvent dans le répertoire courant. Selon votre organisation ce répertoire pourra être plus ou moins rempli, mais vos devriez au minimum reconnaître quelques dossiers ou fichiers habituels. Sur OS X par exemple :  `Applications`, `Bureau`, `Documents`, `Téléchargements`, etc. 

Si vous avez besoin de plus d'informations qu'une simple liste de fichiers, il est possible de passer des *paramètres* à cette commande pour spécifier ce que l'on souhaite obtenir comme informations. Pour obtenir une liste des paramètres disponibles, il est possible pour les utilisateurs d'OS X et Linux de se trouver vers l'aide interne, qui peut être appelée à l'aide de la commande : 

`man ls`

{% include figure.html filename="man-ls.png" caption="La page `manual` pour la commande ls" %}

Dans cette page, vous retrouvez le nom de la commande, les options pour formater la sortie et sélectionner les fichiers à afficher. **Nombre de ces options vous paraîtront sûrement obscures pour le moment, ne vous inquiétez pas, tout s'éclaircira au fil des leçons**. Vous pouvez parcourir cette page de plusieurs manières différentes : la barre espace vous permet de passer à la page suivante, les flèches haut et bas vous permettent de faire défiler le document.

Pour quitter le manuel, appuyez sur la touche :

`q`

et vous serez renvoyé à la ligne de commande où vous vous trouviez précédemment.

Vous pouvez essayer d'utiliser `man` pour l'autre commande que nous avons vu jusqu'ici, `pwd`.

Les utilisateurs de Windows peuvent utiliser la commande `help`, mais cette option propose une information moins riche que ce qui est disponible sur OS X/Linux. Entrez la comand `help` pour voir l'aide disponible, et `help pwd` pour un exemple sur la commande `pwd` par exemple.

Nous allons maintenant pouvoir essayer quelques options que nous avons vu dans le `man` de la commande ls. Si par exemple vous souhaitez voir la liste des fichiers TCT de votre répertoire racine, tapez : 

`ls *.txt`

qui vous affichera la liste des fichiers correspondants s'il en existe dans le répertoire en question. Le \* correspond à un **joker** (ou **métacaractère**) et signifie 'n'importe quoi'. Dans le cas présent, cela signifie que l'on recherche les fichiers dont le nom correspond au modèle : 

[quelquechose.txt]

Faites différents essais avec ce principe. Si par exemple vous avez plusieurs fichiers suivant le modèle de nommage : `1-Canadian.txt`, `2-Canadian.txt`, etc, la commande `ls *-Canadian.txt` les afficherait tous, en excluant les fichiers qui ne correspond pas à ce modèle de [quelquechose]-Canadian.txt.

Imaginons que l'on souhaite obtenir plus d'informations sur les fichiers sélectionnés. Dans le `man`, on trouve une option qui peut être utile :  

>     -l      En plus du nom, afficher le type du fichier, les
>             permissions d'accès, le nombre de liens  physiques,
>             le nom du propriétaire et du groupe, la taille en
>             octets, et l'horodatage

Donc avec la commande :

`ls -l`

vous obtenez dans le terminal une longue liste de fichiers avec des informations similaires à ce que vous trouveriez dans votre explorateur de documents : la taille des fichiers en octets, la date de création, de modification et le nom de fichier. Cette vue n'est pas forcément des plus lisibles, si l'on observe par exemple un fichier test.html donc la taille est de '6020' octets. On est en général plus habitués à des tailles en 

the computer returns a long list of files that contains information similar to what you'd find in your finder or explorer: the size of the files in bites, the date it was created or last modified, and the file name. However, this can be a bit confusing: you see that a file test.html is '6020' bits large. In commonplace language, you are more used to units of measurement like bytes, kilooctet, mégaoctet, et gigaoctet. 

Heureusement, il existe un paramètre pour cela : 

>     -h      Ajouter une lettre indiquant l'unité de taille, 
>             comme M pour méga-octets. (Nouveauté dans fileutils-4.0). 

Si vous souhaitez combiner deux paramètres, il suffit de les utiliser en même temps, par exemple :

`ls -lh`

vous affichera une liste détaillée, dans un format "humain". Vous verrez ainsi que le fichier évoqué précédemment de 6020 octets fait en fait 5,9 ko, qu'un autre fait 1 Mo, etc.

Ces options sont *très* importantes et vous les verrez, adaptées à d'autres commandes, dans d'autres leçons de *Programming historian** : [Wget](/fr/lessons/automated-downloading-with-wget), [MALLET](/lessons/topic-modeling-and-mallet) *[leçon en anglais]*, et [Pandoc](/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown) *[leçon en anglais]*. 

Nous avons maintenant passé un peu de temps dans notre répertoire de base, il est temps d'aller voir ailleurs. Pour cela il existe la commande `cd` (*change directory*) qui va nous permettre de nous déplacer.

Si vous tapez :
`cd desktop` (ou `cd Bureau` selon la langue utilisée par le système)

vous serez maintenant dans le répertoire correspondant à votre bureau. C'est l'équivalent du clic sur un dossier dans l'explorateur de documents. Pour contrôler que tout s'est bien passé, tapez la commande `pwd` et vous devriez voir quelque chose comme : 

`/Users/ianmilligan1/desktop`

Vous pouvez alors explorer l'arborescence de fichiers en combinant cette commande `cd` avec la commande `ls`.

Si vous voulez remonter d'un niveau dans l'arboresence, il suffit d'utiliser la commande :

`cd ..`

Cela aura pour effet de 'remonter' d'un répertoire, et dans l'exemple présent, nous renvoyer dans `/Users/ianmilligan1/`. Si jamais vous voulez revenir directement à votre répertoire racine, il suffit d'utiliser la commande :

`cd --` 

Continuez à explorer, entrez dans le répertoire contenant vos documents, celui contenant les images, etc. Prenez l'habitude de vous déplacer dans les répertoires, en imaginant que vous êtes en train de naviguer dans une [arboresence](https://fr.wikipedia.org/wiki/Arborescence). Si vous êtes dans le répertoire Bureau, il vous sera ainsi impossible de taper `cd documents` car le répertoire racine est un sous-dossier de votre répertoire racine, alors que le Bureau est un dossier frère du répertoire documents. Pour passer d'un répertoire à un répertoire frère, il va falloir repasser par le dossier parent (`cd ..`) et redescendre dans le répertoire désiré (`cd documents`).

Être capable de se déplacer dans l'arborescence à l'aide de la ligne de commande est une compétence importante pour de nombreuses leçons de *Programming historian*. Au fur et à mesure que vous développerez cette compétence vous vous déplacerez directement dans le répertoire désiré. Si l'on reprend l'exemple donné précédemment, on pourrait imaginer se déplacer depuis n'importe quel endroit du système vers le répertoire que l'on souhaite en tapant : 

`cd /users/ianmilligan1/mallet-2.0.7` 

ou sur Windows : 

`cd c:\mallet-2.0.7\`

Ces commandes auraient pou effet de nous envoyer dans le répertoire MALLET utilisé dans la leçon [modèle thématique avec MALLET](/lessons/topic-modeling-and-mallet) *[leçon en anglais]*.

Finalement, tapez : 

`open .` 

sur OS X ou 

`explorer .` 

sur Windows ou

`nautilus .`

sur Linux avec Gnome et cet explorateur de documents installé. 

Cette commande ouvrira l'explorateur dans le répertoire courant. Faites attention à bien laisser un espace entre la commande (open, explorer, nautilus) et le point.

## Interagir avec les fichiers

La ligne de commande ne permet pas seulement de naviguer dans l'arborescence, elle permet aussi d'interagir avec les fichiers : les lire, ouvrir, exécuter et même les éditer, le plus souvent sans même avoir à quitter le terminal.

On est en droit de se demander quel est l'intérêt d'utiliser le terminal pour cela à l'heure des interfaces graphiques. La principale raison est que vous n'avez pas à attraper la souris pour effectuer l'action, et si la courbe d'apprentissage peut être un peu raide, le shell peut devenir un environnement complet de travail. Qui plus est, certains programmes impliquent que vous utilisiez le terminal pour communiquer avec eux. Dès lors que vous allez utilisé la ligne de commande, vous verrez qu'il peut être facile de faire des petites opérations sur les fichiers sans basculer entre différents logiciels. Pour d'autres arguments sur le sujet, vous pourrez lire l'article de Jon Beltran de Heredia : ["Why, oh WHY, do those #?@! nutheads use vi?"](http://www.viemu.com/a-why-vi-vim.html). 

Voici quelques opérations simples pour interagir avec les fichiers.

Vous pouvez commencer par créer un répertoire. Nous allons le créer sur le Bureau, vous pourrez toujours le déplacer plus tard. Après vous être déplacé sur le bureau (`cd`), tapez : 

`mkdir ProgHist-Text`

Cela aura pour effet de créer un répertoire nommé, vous l'aurez deviné, 'ProgHist-Text'. De manière générale, il est préférale d'éviter les espaces dans les noms de fichiers et de répertoires (il existe des solutions de contournement bien entendu, mais l'approche sans espace est la plus simple). Vous pouvez regarder votre bureau pour vérifier que tout s'est bien déroulé. Entrez maintenant dans le répertoire nouvellement créé (en tapant quelque chose qui devrait ressembler à `cd ProgHist-Text`).

Mais attendez ! Il y a une astuce pour faciliter les choses. Remontez dans le répertoire parent (`cd ..`, qui va vous ramener au bureau). Pour naviguer vers le répertoire `ProgHist-Text` vous pouvez bien entendu taper `cd ProgHist-Text` mais vous pouvez aussi taper `cd Prog` puis appuyer sur la touche tabulation. Vous verrez alors que l'interface complète la ligne en `cd ProgHist-Text`. **Utiliser la tabulation va activer l'[auto-complétion](https://fr.wikipedia.org/wiki/Compl%C3%A8tement) grâce à laquelle le terminal va essayer de compléter la chaîne en cours de frappe en fonction du contexte (fichiers disponibles, commandes existantes ...). Attention, le terminal est sensible à la case (dans l'exemple suivant, `cd prog` ne complètera par exemple par en `ProgHist-Text` car il manque la majuscule initiale). Si plusieurs fichiers partagent le même début de nom, l'autocomplétion ne se fera que jusqu'au point de divergence, laissant à l'utilisateur le soit de taper le caractère suivant pour spécifier son choix. Nous vous encourageons à utiliser cette méthode au cours de la leçon pour l'apprivoiser**.

Vous allez maintenant devoir trouver un fichier texte basique sur lequel exécuter les exemples. Le mieux est d'utiliser un ouvrage que l'on sait assez conséquent, on vous propose donc de partir sur *Guerre et Paix* de Léon Tolstoï. Le fichier texte est disponible via le [Projet Gutenberg](http://www.gutenberg.org/ebooks/2600). Si vous avez déjà installé [wget](/fr/lessons/automated-downloading-with-wget), il vous suffit de taper :

`wget http://www.gutenberg.org/cache/epub/2600/pg2600.txt`

Si wget n'est pas installé, téléchargez le fichier en utilisateur votre navigateur web. Suivez le lien ci-dessus en, dans votre navigateur, utilisez la fonction "Enregistrer sous" du menu "Fichier". Choisissez le répertoire ProgHist-Text comme lieu d'enregistrement du fichier. Si maintenant vous tapez dans le terminal :

`ls -lh`

vous verrez quelque chose du type : 

>> -rw-r--r--+ 1 ianmilligan1  staff   3.1M  1 May 10:03 pg2600.txt

Vous pouvez lire le texte contenu dans ce fichier de plusieurs manières. Vous pouvez tout d'abord indiquer à votre système de le lire avec l'outil standard de lecture de fichiers texte. Par défaut ce sera TextEdit sur OS X et Notepad sous Windows. Pour ouvrir un fichier, tapez donc : 

`open pg2600.txt` 

sur OS X, ou 

`explorer pg2600.txt`

sur Windows. 

Cela a pour effet de sélectionner le programme par défaut et d'ouvrir le fichier avec.

Cependant, on souhaitera souvent consulter un fichier sans quitter le terminal. C'est possible et il suffit de taper :

`cat pg2600.txt`

The terminal window erupts and *War and Peace* cascades by. That's great, in theory, but you can't really make any sense of that amount of text? Instead, you may want to just look at the first or the last bit of the file. 

`head pg2600.txt`

Provides a view of the first ten lines, whereas

`tail pg2600.txt`

provides a perspective on the last ten lines. This is a good way to quickly determine the contents of the file. You could add a command to change the amount of lines displayed: `head -20 pg2600.txt`, for example, would show the first twenty lines.

You may also want to change the file name to something more descriptive. You can 'move' it to a new name by typing

`mv pg2600.txt tolstoy.txt`

Afterwards, when you perform a `ls` command, you will see that it is now `tolstoy.txt`. Had you wanted to duplicate it, you could also have run the copy command by typing

`cp pg2600.txt tolstoy.txt`

you will revisit these commands shortly.

Now that you have used several new commands, it's time for another trick. Hit the up arrow on your keyboard. Notice that `cp pg2600.txt tolstoy.txt` appears before your cursor. You can continue pressing the up arrow to cycle through your previous commands. The down arrow cycles back toward your most recent command.

After having read and renamed several files, you may wish to bring their text together into one file. To combine, or concatenate, two or more files, you can use the `cat` command. First, let's duplicate the Tolstoy file ( `cp tolstoy.txt tolstoy2.txt`). Now that you have two copies of *War and Peace*, let's put them together to make an **even longer** book. 

To combine, or concatenate, two or more files use the `cat` command. Type 

`cat tolstoy.txt tolstoy2.txt` 

and press enter. This prints, or displays, the combined files within the shell. However, it is too long to read on this window! Luckily, by using the `>` command, you can send the output to a new file, rather than the terminal window. Type 

`cat tolstoy.txt tolstoy2.txt > tolstoy-twice.txt`. 

Now, when you type `ls` you'll see `tolstoy-twice.txt` appear in your directory.

When combining more than two files, using a wildcard can help avoid having to write out each filename individually. As you have seen above, `*`, is a place holder for zero or more characters or numbers. So, if you type 

`cat *.txt > everything-together.txt` 

and hit enter, a combination of all the .txt files in the current directory are combined in alphabetical order as `everything-together.txt`. This can be very useful if you need to combine a large number of smaller files within a directory so that you can work with them in a text analysis program. Another wildcard worth remembering is `?` which is a place holder for a single character or number.

## Editing Text Files Directly on the Command Line

If you want to read a file in its entirety without leaving the command line, you can fire up [vim](http://en.wikipedia.org/wiki/Vim_%28text_editor%29). Vim is a very powerful text editor, which is perfect for using with programs such as [Pandoc](http://johnmacfarlane.net/pandoc/) to do word processing, or for editing your code without having to switch to another program. Best of all, it comes included with bash on both OS X and Windows. Vim has a fairly steep learning curve, so we will just touch on a few minor points. 

Type 

`vim tolstoy.txt`

You should see vim come to life before you, a command-line based text editor.

{% include figure.html filename="vim.png" caption="Vim" %}

If you really want to get into Vim, there is a [good Vim guide](http://vimdoc.sourceforge.net/htmldoc/quickref.html) available. 

Using Vim to read files is relatively simple. You can use the arrow keys to navigate around and could theoretically read *War and Peace* through the command line (one should get an achievement for doing that). Some quick basic navigational commands are as follows:

`Ctrl+F` (that is, holding down your 'control key' and pressing the letter F) will move you down a page (`Shift+UpArrow` for Windows).

`Ctrl+B` will move you up a page. (`Shift+DownArrow` for Windows users). 

If you want to rapidly move to the end of a line, you can press: `$` and to move to the start of one, `0`. You can also move between sentences by typing `)` (forward) or `(` (backwards). For paragraphs, use `}` and `{`. Since you are doing everything with your keyboard, rather than having to hold your arrow key down to move around a document, this lets you zip quickly back and forth.

Let's scroll to the top and do a minor change, such as adding a `Reader` field in the heading. Move your cursor in between **Author:** and **Translators:**, like so:

{% include figure.html filename="about-to-insert.png" caption="About to Insert a Field" %}

If you just start typing, you'll get an error message or the cursor will begin jumping around. This is because you have to specify that you want to do an edit. Press the letter

`a`

At the bottom of the screen, you will see

`-- INSERT --`

This means you are in insert mode. You can now type and edit text as if you are in a standard text editor. Press `enter` twice, then `arrow up`, and type

`Reader: A Programming Historian`

When you are done, press `ESC` to return to reading mode.

To leave vim or to make saves, you have to enter a series of commands. Press `:` and you'll move to the command input line of Vim. you can enter a variety of commands here. If you want to save the file, type `w` to 'write' the file. If you execute that command, you will see

>> "tolstoy.txt" [dos] 65009L, 3291681C written

{% include figure.html filename="after-writing.png" caption="After Writing the File, with Our Minor Change" %}

If you want to quit, type `:` again and then `q`. It will return you to the command line. As with the rest of bash, you could have also combined the two commands. Pressing `:` and then typing `wq` would have written the file and then quit. Or, if you wanted to exit **without** saving, `q!` would have quit vim and overriden the default preference to save your changes.

Vim is different than you are likely used to and will require more work and practice to become fluent with it. But if you are tweaking minor things in files, it is a good way to get started. As you become more comfortable, you might even find yourself writing term papers with it, by harnessing the [footnoting and formatting power of Pandoc and Markdown](/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown).

## Moving, Copying, and Deleting Files

Let's say you are done with this directory, and you would like to move `tolstoy.txt` somewhere else. First, you should create a backup copy. The shell is quite unforgiving with mistakes, and backing up is even more important than with GUIs. If you delete something here, there's no recycling bin to fish it out of. To create a backup, you can type

`cp tolstoy.txt tolstoy-backup.txt`

Now when you run a `ls` command you will see five files, two of which are the same: `tolstoy.txt` and `tolstoy-backup.txt`. 

Let's move the first of these somewhere else. By way of example, let's create a second directory on your desktop. Move up to your desktop (`cd ..`) and `mkdir` another directory. Let's call it `proghist-dest`. 

To copy `tolstoy.txt` you have a few different options. you could run these commands from anywhere in the shell, or you could visit either the origin or destination directories. For this example, let's just run it from here. The basic format of the copy command is `cp [source] [destination]`. That is, you type `cp` first, and then enter the file or files that you want to copy followed by where they should go.

In this case, the command

`cp /users/ianmilligan1/desktop/proghist-text/tolstoy.txt /users/ianmilligan1/desktop/proghist-dest/`

will copy Tolstoy from the first directory to the second directory. You will have to insert your own username in place of 'ianmilligan1'. This means you now have three copies of the novel on our computer. The original, the backup and the new copy in the second directly. If you wanted to **move** the file, that is, not leave a copy behind, you could run the command again, swapping `cp` for `mv`; let's not do this yet.

You can also copy multiple files with a single command. If you wanted to copy **both** the original and the backup file, you could use the wildcard command. 

`cp /users/ianmilligan1/desktop/proghist-text/*.txt /users/ianmilligan1/desktop/proghist-dest/`

This command copies **all** the text files from the origin directory into the destination directory.

Note: If you are in the directory that you either want to move things to or from, you do not have to type out the whole directory structure. Let's do two quick examples. Change your directory to the `proghist-text` directory. From this location, if you wanted to copy these two files to `proghist-dest`, this command would work:

`cp *.txt /users/ianmilligan1/desktop/proghist-dest/` (on OS X, substitute the directory on Windows)

Alternatively, if you were in the `proghist-dest` directory, this command would work:

`cp /users/ianmilligan1/desktop/proghist-text/*.txt ./`

The `./` command refers to the **current** directory you're in. **This is a really valuable command.**

Finally, if you want to delete a file, for whatever reason, the command is `rm`, or remove. **Be careful with the `rm` command**, as you don't want to delete files that you do not mean to. Unlike deleting from within your GUI, there is **no** recycling bin or undo options. For that reason, if you are in doubt, you may want to exercise caution or maintain a regular backup of your data.

Move to `proghist-text` and delete the original file by typing

`rm tolstoy.txt`

Check that the file is gone using the `ls` command.

If you wanted to delete an entire directory, you have two options. you can use `rmdir`, the opposite of `mkdir`, to delete an **empty** directory. To delete a directory with files, you could use from the desktop:

`rm -r proghist-text`

## Conclusions

You may want to take a break from the terminal at this point. To do so, enter `exit` and you'll close your session. 

There are more commands to try as you get more comfortable with the command line. Some of our other favourites are `du`, which is a way to find out how much memory is being used (`du -h` makes it human readable — as with other commands). For those of you on OS X, `top` provides an overview of what processes are running (`mem` on Windows) and `touch FILENAME` can create a basic text file on both systems

By this point, we hope you have a good, basic understanding of how to move around using the command line, move basic files, and make minor edits here and there. This beginner-level lesson is designed to give you some basic fluency and confidence. In the future, you may want to get involved with scripting.

Have fun! Before you know it, you may find yourself liking the convenience and precision of the command line - for certain applications, at least - far more than the bulkier GUI that your system came with. Your toolkit just got bigger.

## Reference Guide

For your convenience, here are the commands that you have learned in this lesson:

| Command | What It Does |
|---------|--------------|
| `pwd` | Prints the 'present working directory,' letting you know where you are. |
| `ls` | Lists the files in the current directory
| `man *` | Lists the manual for the command, substituted for the `*`
| `cd *` | Changes the current directory to `*`
| `mkdir *` | Makes a directory named `*`
| `open` or `explorer` | On OS X, `open` followed by a file opens it; in Windows, the command `explorer` followed by a file name does the same thing.
| `cat *` | `cat` is a versatile command. It will read a file to you if you substitute a file for `*`, but can also be used to combine files.
| `head *` | Displays the first ten lines of `*`
| `tail *` | Displays the last ten lines of `*`
| `mv` | Moves a file
| `cp` | Copies a file
| `rm` | Deletes a file
| `vim` | Opens up the `vim` document editor.
