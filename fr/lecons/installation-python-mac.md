---
title: Installer un environnement de développement Python (Mac)
layout: lesson
date: 2012-07-17
authors:
- William J. Turkel
- Adam Crymble
reviewers:
- Jim Clifford
- Amanda Morton
editors:
- Miriam Posner
translator:
- Sylvain Machefert
translation-editor:
- X
translation-reviewer:
- X
translation_date: 2018-01-26
difficulty: 1
activity: transforming
topics: [get-ready, python]
abstract: "Cette leçon détaille les étapes nécessaires à l'installation d'un environnement de développement intégré sur Mac pour Python."
redirect_from: /fr/lessons/mac-installation
---

{% include toc.html %}


### Effectuer une sauvegarde de votre système

Les utilisateurs de Mac peuvent utiliser le système [Time Machine][] pour mener à bien cette opération.

### Installation de Python v.2

Depuis au moins mai 2012, Mac OS X est livré avec Python 2 préinstallé. 
Vous pouvez vérifier qu'il est bien installé sur votre machine en lançant
le terminal disponible sous `‘Applications/Utilities’` puis en tapant :
`which python` suivi de la toucher entrée. La touche entrée a pour effet 
de demander au terminal d'exécuter la commande saisie. Si vous voyez alors 
`‘/usr/bin/python’` ou quelque chose d'approchant contenant le mot "python"
et plusieurs signes slash, l'installation devrait être ok. Sinon, fermez le 
terminal, téléchargez la dernière version du langage (2.7.14 en janvier 2018)
et installez la en suivante les instructions disponibles sur le [site officiel Python][].

### Créer un répertoire

Pour ne pas s'égarer, le mieux est d'avoir un répertoire (ou dossier) sur
votre ordinateur dans lequel vous conserverez vos programmes Python (par exemple 
`programming-historian`). Vous pouvez le créer où vous le souhaitez sur votre disque dur.

### Installer Komodo Edit

Komodo Edit is est éditeur de code libre et gratuit. Si vous préférez utiliser
un autre éditeur, il existe de multiples [autres solutions][]. Certains de
nos testeurs préfèrent par exemple le logiciel [TextWrangler][]. À vous de 
choisir la solution qui vous convient le mieux, mais afin de garder une cohérence
dans l'ensemble de nos leçons, celles-ci utiliseront Komodo Edit. Vous pouvez en
télécharger une version depuis le [site officiel de Komodo Edit]. Installez ensuite 
le logiciel à partir du fichier `.DMG`.

##### Démarrer Komodo Edit

Cela devrait ressembler à quelque chose de ce type :

![capture d'écran de Komodo Ecit sur OS X](https://raw.githubusercontent.com/programminghistorian/jekyll/bc4c0f1398f54adb1add6bb156756212c28e8f78/images/komodo-edit-mac.png)

Komodo Edit sur un Mac

Si vous ne voyez pas la "Toolbox" sur la droite, vous pouvez l'afficher
via le menu `View->Tabs & Sidebars ->Toolbox`. La zone "projet" qui apparaît
peut-être n'est pas primordiale pour le moment. N'hésitez pas à prendre un peu
de temps pour vous familiariser avec l'éditeur, le fichier d'aide est plutôt
bien fait.

##### Configurer Komodo Edit

Vous devez maintenant configurer l'éditeur pour pouvoir exécuter des 
programmes en Python. Dans la zone Toolbox, cliquer sur l'icône en
forme d'engrenange et sélectionnez “`New Command…`“. Dans la fenêtre 
qui apparaît, renommez votre commande en “`Run Python`” et n'hésitez pas
à modifier l'icône si vous le souhaitez. 

Dans la zone “`Command`”, type

``` python
%(python) %f
```

and under "Start in," enter

``` python
%D
```

Click OK. Your new Run Python command should appear in the Toolbox
pane.

Step 2 – “Hello World” in Python
--------------------------------

It is traditional to begin programming in a new language by trying to
create a program that says ‘hello world’ and terminates. We will show
you how to do this in Python and HTML.

Python is a good programming language for beginners because it is very
high-level. It is possible, in other words, to write short programs that
accomplish a lot. The shorter the program, the more likely it is for the
whole thing to fit on one screen, and the easier it is to keep track of
all of it in your mind.

Python is an 'interpreted' programming language. This means that
there is a special computer program (known as an interpreter) that knows
how to follow instructions written in that language. One way to use the
interpreter is to store all of your instructions in a file, and then run
the interpreter on the file. A file that contains programming language
instructions is known as a program. The interpreter will execute each of
the instructions that you gave it in your program and then stop. Let’s
try this.

In your text editor, create a new file, enter the following two-line
program and save it to your `programming-historian` directory as
`hello-world.py`

``` python
# hello-world.py
print('hello world')
```

Your chosen text editor should have a “`Run`” button that will allow you
to execute your program. If you are using TextWrangler, click on the
“\#!” button and Run. If all went well, it should look something like
this:

![TextWrangler-hello-world](https://raw.githubusercontent.com/programminghistorian/jekyll/bc4c0f1398f54adb1add6bb156756212c28e8f78/images/TextWrangler-hello-world.png)
“Hello World” in Python on a Mac

### Interacting with a Python shell

Another way to interact with an interpreter is to use what is known as a
shell. You can type in a statement and press the Enter key, and the
shell will respond to your command. Using a shell is a great way to test
statements to make sure that they do what you think they should. This is
done slightly differently on Mac, Linux and Windows.

You can run a Python shell by launching the 'terminal'. On the Mac, open
the Finder and double-click on `Applications -> Utilities -> Terminal`
then typing “`python`” into the window that opens on your screen. At the
Python shell prompt, type

``` python
print('hello world')
```

and press Enter. The computer will respond with

``` python
hello world
```

When we want to represent an interaction with the shell, we will use
`->` to indicate the shell’s response to your command, as shown below:

``` python
print('hello world')
-> hello world
```

On your screen, it will look more like this:

![hello world terminal on a Mac](https://raw.githubusercontent.com/programminghistorian/jekyll/bc4c0f1398f54adb1add6bb156756212c28e8f78/images/hello-world-terminal.png)
Python Shell in Mac Terminal

Now that you and your computer are up and running, we can move onto some
more interesting tasks. If you are working through the Python lessons in
order, we suggest you next try '[Understanding Web Pages and HTML][].'

  [Time Machine]: http://support.apple.com/kb/ht1427
  [site officiel Python]: http://www.python.org/
  [Beautiful Soup]: http://www.crummy.com/software/BeautifulSoup/
  [autres solutions]: http://wiki.python.org/moin/PythonEditors/
  [TextWrangler]: http://www.barebones.com/products/textwrangler/
  [Komodo Edit website]: http://www.activestate.com/komodo-edit
  [Understanding Web Pages and HTML]: /lessons/viewing-html-files
