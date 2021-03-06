---
URL:     https://linuxfr.org/news/python-pour-noel-2019-partie-4-py-pyenv
Title:   Python 2019/2021 — partie 4 — Py Pyenv
Authors: Oliver, Ysabeau, Philippe F, ZeroHeure, Davy Defaud, Yves Bourguignon, Gounou, patrick_g et Benoît Sibaud
Date:    2019-09-28T11:19:34+02:00
License: CC0
Tags:    python
Score:   34
---

Python 2019/2021 — partie 4 — Py Pyenv
======================================

Dans les précédentes dépêches, nous avons discuté de la [popularité de Python](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1), de la [fin de la maintenance de Python 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2), de l’[installation de différentes variantes](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets) de Python…

Ce quatrième volet de la série donne des conseils pour faire cohabiter différentes versions de Python sur sa machine et pouvoir basculer simplement d’une version à l’autre. On commence avec [Py](https://docs.python.org/3/using/windows.html#getting-started) et [Pyenv](https://github.com/pyenv/pyenv). La dépêche suivante montrera comment obtenir des résultats similaires avec [Conda](https://en.wikipedia.org/wiki/Conda_(package_manager)) et [Docker](https://fr.wikipedia.org/wiki/Docker_(logiciel)).

La dépêche est au format *tutoriel* afin d’être rapidement opérationnelle. Enfin, les versions de CPython, d’ActivePython, d’Anaconda, de Miniconda, d’IronPython, de Jython, de MicroPython, de PyPy, de Pyston et de Stackless sont à portée de ~~main~~ clavier. 🚀 🐍 [![Le logo de Python est entouré de petites icônes symbolisant la variété des domaines où s’applique Python, et, à droite, un joyeux barbu se tient derrière un écran d’ordinateur qui affiche « partie = 4, "Py Pyenv" \n print(partie) »](04.webp)](https://github.com/linuxfrorg/articles/tree/main/python/2019-2021)

----

* [Dépôt du code source de Pyenv](https://github.com/pyenv/pyenv)
* [Python pour la rentrée 2019 — partie 1 — Popularité de Python](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1)
* [Python pour la rentrée 2019 — partie 2 — Fin de Python 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2)
* [Python pour la rentrée 2019 — partie 3 — Installation de Python et de paquets](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets)
* [Dépôt du code source de Pyenv-Win, le portage pour Windows](https://github.com/pyenv-win/pyenv-win)
* [Article Wikipédia sur Conda, le gestionnaire de paquets Python de Miniconda/Anaconda ](https://en.wikipedia.org/wiki/Conda_(package_manager))
* [Article Wikipédia sur Docker](https://fr.m.wikipedia.org/wiki/Docker_%28logiciel%29)

----

Plusieurs Pythons sur sa machine
================================

Parfois, nous avons besoin d’avoir plusieurs versions de Python installées sur sa machine. Citons quelques cas pratiques :

* une équipe est en cours de migration d’une version Python à une autre, cela peut être de Python 2 vers Python 3, mais aussi de Python 3.4 à Python 3.6 ; et pendant la phase de transition, le logiciel doit fonctionner avec les deux versions ;
* les utilisateurs sont hétérogènes en termes de version de Python, cas typique du logiciel libre : Python 2.6, Python 2.7, Python 3.4, Python 3.5, Python 3.6, Python 3.7, PyPy, Anaconda, Miniconda, MicroPython, etc. ;
* une équipe livre des applications pour plusieurs systèmes d’exploitation différents, lesquels utilisent des versions de Python différentes ; l’équipe a besoin de passer facilement d’une version à une autre ;
* chaque membre d’une équipe (dev, test, …) a le choix d’installer le système d’exploitation de son choix sur sa machine, mais tous les membres doivent pouvoir tester l’application avec la version cible utilisée en production ;
* on développe une application Python et on souhaite vérifier si elle est bien fonctionnelle avec la future Python 3.8 (en plus de la version Python actuellement utilisée pour le développement).

Dans tous ces cas, c’est plus simple si plusieurs versions de Python sont installées sur une même machine, et si un outil nous permet de facilement passer d’une version de Python à une autre. C’est ce que nous allons voir dans la suite de la dépêche.

Sous Windows, gérer plusieurs versions de Python avec le lanceur Py
===================================================================

Introduction
------------

Toutes les versions de Python sous Windows installent le lanceur Py (cela concerne Python 2.7 et toute la série des Python 3). Il permet de sélectionner la bonne version de Python à lancer parmi les installations disponibles.

Historiquement, lancer un programme Python depuis Windows pouvait s’avérer fastidieux. En effet, si l’on avait omis de cocher la case « ajouter Python au chemin d’exécution lors de l’installation », Python n’était pas accessible depuis la ligne de commande. Et lorsqu’il y a plusieurs versions de Python installées, notamment Python 2 et Python 3, cocher cette case systématiquement fait que l’un des interpréteurs prend le pas sur l’autre et c’est vite le bazar. Autre facteur aggravant, les versions récentes de Python s’installent selon la recommandation de Microsoft dans le répertoire `%USERDATA%\Local\Programs\Python`, ce qui fait qu’elles peuvent être pénibles à retrouver ou à taper en ligne de commande (fini le `C:\Python33\python.exe`).

Py apporte une solution sympathique à ces problèmes. Il inspecte les informations du système pour détecter toutes les versions de Python installées et propose un moyen simple de les lancer.

**⚠ Attention** de ne pas confondre [Py](https://docs.python.org/3/using/windows.html#getting-started) avec [Py.io](https://pypi.org/project/py/).

En pratique
-----------

Py s’utilise en ligne de commande. Le premier argument passé désigne le choix (optionnel) de l’interpréteur, et le reste est passé à la commande `python.exe` tel quel :

    >py
    Python 3.7.0 (v3.7.0:1bf9cc5093, Jun 27 2018, 04:59:51) [MSC v.1914 64 bit (AMD64)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

Si je veux lancer du Python 2 :

    >py -2
    Python 2.7.14 (v2.7.14:84471935ed, Sep 16 2017, 20:25:58) [MSC v.1500 64 bit (AMD64)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

Du Python 3 :

    >py -3
    Python 3.7.0 (v3.7.0:1bf9cc5093, Jun 27 2018, 04:59:51) [MSC v.1914 64 bit (AMD64)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

On note qu’il a choisi la version 3.7 par défaut pour Python 3.

Pour avoir Python 3.5 plus spécifiquement :

    >py -3.5
    Python 3.5.3 (v3.5.3:1880cb95a742, Jan 16 2017, 16:02:32) [MSC v.1900 64 bit (AMD64)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

Il choisit la version 64 bits par défaut. Pour avoir du Python 3.5 32 bits :

    >py -3.5-32
    Python 3.5.1 (v3.5.1:37a07cee5969, Dec  6 2015, 01:38:48) [MSC v.1900 32 bit (Intel)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

Je liste les versions de Python installées avec `py -0` :

    >py -0
    Installed Pythons found by py Launcher for Windows
     -3.7-64 *
     -3.5-64
     -3.5-32
     -2.7-64

Le symbole `*` indique la version utilisée par défaut.

J’utilise régulièrement la commande `-0p` qui permet de voir où sont installés les interpréteurs, car je ne m’en rappelle jamais bien. Sur mon système, ça donne (c’est un peu le bazar) :

    >py -0p
    Installed Pythons found by py Launcher for Windows
     -3.7-64        C:\Users\g582619\AppData\Local\Programs\Python\Python37\python.exe *
     -3.5-64        C:\Users\g582619\AppData\Local\Programs\Python\Python35\python.exe
     -3.5-32        "C:\Program Files (x86)\Python35-32\python.exe"
     -2.7-64        C:\Python27\python.exe

Cette petite démo couvre l’ensemble des commandes disponibles, qu’on peut bien sûr retrouver avec `--help` . À noter que cela va afficher l’aide de Py suivie de l’aide de Python.

    >py --help
    Python Launcher for Windows Version 3.7.150.1013

usage:
    py [launcher-args] [python-args] script [script-args]

Launcher arguments :

    -2     : Launch the latest Python 2.x version
    -3     : Launch the latest Python 3.x version
    -X.Y   : Launch the specified Python version
         The above all default to 64 bit if a matching 64 bit python is present.
    -X.Y-32: Launch the specified 32bit Python version
    -X-32  : Launch the latest 32bit Python X version
    -X.Y-64: Launch the specified 64bit Python version
    -X-64  : Launch the latest 64bit Python X version
    -0  --list       : List the available pythons
    -0p --list-paths : List with paths

    The following help text is from Python:

    usage: C:\Users\g582619\AppData\Local\Programs\Python\Python37\python.exe [option] ... [-c cmd | -m
    mod | file | -] [arg] ...
    Options and arguments (and corresponding environment variables):
    -b     : issue warnings about str(bytes_instance), str(bytearray_instance)
    -B     : don't write .pyc files on import; also PYTHONDONTWRITEBYTECODE=x
    -c cmd : program passed in as string (terminates option list)
    …

Un autre atout de Py est qu’il comprend la fameuse *shebang line*. Ainsi, des scripts écrits pour UNIX, prévus pour être exécutables grâce à la ligne magique vont fonctionner sous Windows :

    #!/usr/bin/env python

Les différentes variations de _shebang line_ sont gérées. Et on peut combiner ça astucieusement avec la sélection automatique de l’interpréteur. Voici un exemple concret (pour rappel, sous DOS, la commande `type` est l’équivalent pauvre de `cat`) :

    >type toto2.py
    #! /usr/bin/env python2
    # lancez moi avec Python 2!
    import sys
    print sys.version

    >type toto3.py
    #! /usr/bin/env python3.5.0
    # lancez moi avec Python 3!
    async def hello(): pass # pas de async en python 2
    import sys
    print(sys.version)

On a deux programmes qui vont tous les deux refuser de fonctionner si on les lance avec la mauvaise version de Python 2 vs Python 3. Mais Py s’en sort très bien. Et comme c’est lui qui est déclaré comme *ouvreur* de fichiers avec l’extension `.py` , on peut exécuter ces scripts directement :

    >toto2.py
    2.7.14 (v2.7.14:84471935ed, Sep 16 2017, 20:25:58) [MSC v.1500 64 bit (AMD64)]

    >toto3.py
    3.5.3 (v3.5.3:1880cb95a742, Jan 16 2017, 16:02:32) [MSC v.1900 64 bit (AMD64)]

Quelques limitations
--------------------

Py résout pas mal de problèmes, mais il conserve un gros inconvénient : il ne gère pas le répertoire `Python/Scripts` qui contient tous les scripts ou les applications installées via `pip`.

Par exemple, pour utiliser PyQt, on a besoin d’exécuter `designer.exe` et `pyuic5.exe`, qui sont installés dans `Python/Scripts`. Si vous lancez Py avec une version donnée, le `PATH` n’est pas modifié et vous n’avez pas accès directement aux exécutables dont vous avez besoin. Dans ce cas, retour à la case départ, avec bidouillage du `PATH` en fonction de la version Python lancée.

Un cas où il faut être particulièrement attentif à ce détail, est celui de l’utilisation de `pip` : `pip install toto` va installer le paquet `toto` dans la version par défaut de Python, qui n’est pas forcément celle que vous aviez en tête.

La solution avec `pip` est plutôt simple. Il faut penser à taper :

    py -3.5 -m pip install toto

Conclusion sur Py
-----------------

Son arrivée a vraiment amélioré le quotidien de la ligne de commande Python sous Windows. Ça marche tellement bien qu’une réflexion est en cours pour l’adapter sous UNIX.

Pour plus de détails sur Py, allez voir la [documentation](https://docs.python.org/3.7/using/windows.html?highlight=launcher#python-launcher-for-windows).

Py référence les versions majeures de Python que vous avez installées sur votre système, mais il ne va pas vous aider à les installer. En particulier, si vous voulez tester des versions de Python en développement (dev, alpha ou rc), elles ne sont pas empaquetées sous forme d’installateur Windows. Il faut les compiler et les installer à la main. Sauf si vous utilisez Pyenv… qu’on décrit justement dans la suite de la dépêche.

Pyenv
=====

Introduction
------------

L’outil `pyenv` n’a aucune dépendance vis‐à‐vis de Python, et peut donc être installé sur une machine dépourvue de Python. Son secret ? `pyenv` est un ensemble de scripts shell (`bash`) à base de [poudre verte](http://poudreverte.org/).

C’est le cousin des outils [`rbenv`](https://github.com/rbenv/rbenv) et [`phpenv`](https://github.com/phpenv/phpenv). Sa documentation le décrit comme le gestionnaire simple des versions Python _(Simple Python Version Management)_.

Ses fonctionnalités :

* sélection parmi des centaines de versions et interpréteurs Python ([CPython](https://fr.wikipedia.org/wiki/CPython), [ActivePython](https://wiki.python.org/moin/ActivePython), [Anaconda](https://fr.wikipedia.org/wiki/Anaconda_(Python_distribution)), [Miniconda](https://stackoverflow.com/a/45421204/938111), [IronPython](https://fr.wikipedia.org/wiki/IronPython), [Jython](https://fr.wikipedia.org/wiki/Jython), [MicroPython](https://fr.wikipedia.org/wiki/MicroPython), [PyPy](https://fr.wikipedia.org/wiki/PyPy), [Pyston](https://github.com/dropbox/pyston) et [Stackless](https://fr.wikipedia.org/wiki/Stackless_Python)) ;
* téléchargement automatique des sources et des éventuels correctifs ;
* compilation et installation automatique ;
* passage facile d’une version Python à une autre.

Avantage
--------

Son avantage principal est de permettre de tester un développement en cours avec différentes variations Python avec lesquelles le projet cherche à être compatible. Prenons deux cas :

* une équipe souhaite tester son logiciel avec les versions de Python utilisées par les utilisateurs finaux comme, par exemple, Python 2.7, Python 3.4, Python 3.5, Python 3.6, Python 3.7, PyPy, Anaconda, Miniconda, etc. ;
* les membres d’une équipe (dev, test…) peuvent utiliser le système d’exploitation de leur choix sur leur machine mais chaque membre doit pouvoir tester l’application avec la (ou les) version(s) cible(s) utilisée(s) en prod (ou par les clients).

Dans ces deux cas, les membres de l’équipe peuvent avoir, avec `pyenv` sur leur ordinateur, les mêmes variations/versions de Python et peuvent obtenir des exécutions similaires.

En plus, `pyenv` peut s’interfacer avec `virtualenv`, `pipenv` et bien d’autres outils bien pratiques. Et comme [Ryzz nous le signale](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets#comment-1784295), on peut utiliser `pip` sans l’option `--user` car `pyenv` installe Python dans l’espace utilisateur.

Inconvénients
-------------

Attention, [_jihele_ nous explique](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets#comment-1784390) que cela n’avait pas été possible d’installer Python 3.7 sur Debian _Stretch_ car cette distribution n’avait pas les bibliothèques en version compatible.

En effet, `pyenv` télécharge le code source de l’interpréteur Python, mais pas celui de ses dépendances qu’il faut installer préalablement. Les anciennes versions des distributions GNU/Linux ont des vieilles versions des bibliothèques qui peuvent être trop anciennes par rapport aux besoins des dernières versions des interpréteurs Python !

Notons que la version installée avec `pyenv` n’a pas reçu la même attention que la version fournie (compilée) par la distribution GNU/Linux. Bien souvent, l’équipe d’intégration (de la distribution) va empaqueter (compiler) une version en activant différentes optimisations comme la [LTO](https://wiki.debian.org/LTO "Link Time Optimization") et l’équipe assurance qualité va vérifier que le paquet Python passe correctement les tests.

Par conséquent, `pyenv` c’est bien pour tester la conformité avec les versions des interpréteurs, mais on risque d’avoir des comportements différents entre la version compilée par `pyenv` et la version *officielle* de chaque distribution GNU/Linux, comme, par exemple, sur la vitesse d’exécution ou la commutation de contexte des fils d’exécution (_thread context switching_)…

Un dernier point à noter dans les inconvénients : la difficulté pour trouver la bibliothèque nécessaire à la compilation, car le message d’erreur n’a vraiment pas été conçu pour indiquer le nom du paquet à installer. De plus, les distributions nomment rarement un paquet avec le même nom.

Donc, c’est bien pour les postes de l’équipe projet, mais à éviter en production.

Installer pyenv
---------------

* sous macOS, `pyenv` est disponible via [homebrew](https://github.com/pyenv/pyenv#homebrew-on-macos) ;
* sous Windows, voir le portage [pyenv-win](https://github.com/pyenv-win/pyenv-win) ;
* les distributions GNU/Linux n’empaquettent pas (encore ?) `pyenv`, un installateur est disponible, [pyenv-installer](https://github.com/pyenv/pyenv-installer), mais je préfère vous indiquer aussi une méthode plus manuelle, nous allons donc voir deux façons d’installer `pyenv` — avant d’exécuter les scripts ci‐dessous, les responsables sécurité recommandent de vérifier leur contenu car ces scripts pourraient aussi installer un logiciel malveillant (_malware_).

### Avec l’installateur

    git clone https://github.com/pyenv/pyenv-installer
    chmod +x pyenv-installer/bin/pyenv-installer
    pyenv-installer/bin/pyenv-installer

### À la main

    mkdir -p ~/.local/git
    cd       ~/.local/git
    git clone https://github.com/pyenv/pyenv
    cd pyenv
    cd plugins/python-build

Pour partager le cache avec les autres utilisateurs avec `sudo` :

    PREFIX=/usr/local/share/python-build sudo ./install.sh

Sans utiliser `sudo` (ma recommandation, surtout si une seule personne utilise l’ordinateur) :

    PREFIX=~/.local/share/python-build ./install.sh

Configurer son shell
--------------------

Si on aime avoir un `$PATH` minimaliste, alors je recommande d’ajouter plutôt un lien symbolique :

    cd ~/.local/bin
    ln -s ~/.local/git/pyenv/bin/* .

Sinon, ajouter `export PATH="~/.local/git/pyenv/bin:$PATH"` dans le `~/.bashrc` (ou `~/.zshrc` ou autres).

Ensuite, ajouter un `eval "$(pyenv init -)"` dans le `~/.bashrc` ou `~/.zshrc` ou [~/.config/fish/config.fish](http://fishshell.com/docs/current/tutorial.html#tut_startup).

Au final, le `~/.bashrc` (ou `~/.zshrc` ou autres) va donc ressembler à :

```sh
# ------ pyenv ------
# activer la ligne suivante si pas de lien symbolique ~/.local/bin 
# export PATH="~/.local/git/pyenv/bin:$PATH" 
eval "$(pyenv init -)"
```

Tester l’installation
---------------------

    $ source ~/.bashrc

    $ pyenv --version
    pyenv 1.2.12-5-g10bf9d22

    $ pyenv versions
    * system (set by /home/<user>/.local/git/pyenv/version)

    $ pyenv install --list | wc -l

    $ pyenv install --list
    [...]

Incroyable, `pyenv` propose 374 variantes d’interpréteurs Python, avec les versions de [CPython](https://fr.wikipedia.org/wiki/CPython), [ActivePython](https://wiki.python.org/moin/ActivePython), [Anaconda](https://fr.wikipedia.org/wiki/Anaconda_(Python_distribution))/[Miniconda](https://stackoverflow.com/a/45421204/938111), [IronPython](https://fr.wikipedia.org/wiki/IronPython), [Jython](https://fr.wikipedia.org/wiki/Jython), [MicroPython](https://fr.wikipedia.org/wiki/MicroPython), [PyPy](https://fr.wikipedia.org/wiki/PyPy), [Pyston](https://github.com/dropbox/pyston) et [Stackless](https://fr.wikipedia.org/wiki/Stackless_Python) !

Prérequis à la compilation
--------------------------

Pour installer une version de Python open source, la commande `pyenv` va télécharger le code source et le compiler. Il est donc nécessaire d’installer les dépendances pour que la compilation se passe bien. Les dépendances nécessaires pour la compilation sont celles avec un suffixe `-dev` ou `-devel` selon la distribution GNU/Linux :

* avec Ubuntu 19.04 _Disco Dingo_ :

        sudo apt install build-essentials
        sudo apt install libbz2-dev
        sudo apt install tk-dev
        sudo apt install libreadline-dev
        sudo apt install libsqlite3-dev

* avec Fedora 29 :

        sudo dnf install gcc make
        sudo dnf install openssl-devel
        sudo dnf install tk-devel
        sudo dnf install readline-devel
        sudo dnf install libsqlite3x-devel

J’ai pu oublier d’autres dépendances. Merci de fournir vos conseils dans les commentaires. Par exemple, comment cela se passe avec d’autres systèmes d’exploitation ?

Fichier `.python-version`
-------------------------

C’est un fichier magique !

```c
$ cd /chemin/projet/python

$ python --version
Python 2.7.16

$ python3 --version
Python 3.7.3

$ echo '3.5.3' > .python-version

$ pyenv install
[...] pyenv détecte ce fichier,
      et comme CPython 3.5.3
      n'est pas encore installé,
      pyenv télécharge le code source
      et le compile...

$ python --version
Python 3.5.3

$ python3 --version
Python 3.5.3
```

Installons plusieurs versions de CPython
----------------------------------------

C’est parti :

```c
$ pyenv install 3.4.3
(compilation...)

$ pyenv install 3.5.3
(compilation...)

$ pyenv install 3.6.8
(compilation...)

$ pyenv install 3.7.3
(compilation...)

$ pyenv install versions
* system (set by /home/oliver/.local/git/pyenv/version)
  3.4.3
  3.5.3
  3.6.8
  3.7.3
```

Maintenant, demandons à `pyenv` de gérer le fichier `.python-version` :

```c
$ cd /un/autre/projet/python

$ ls .python-version
ls: cannot access '.python-version': No such file or directory

$ pyenv local 3.5.3

$ python --version
Python 3.5.3

$ cat .python-version
3.5.3

$ pyenv local 3.6.8

$ python --version
Python 3.6.8

$ python3 --version
Python 3.6.8

$ pyenv install versions
  3.4.3
  3.5.3
* 3.6.8 (set by /un/autre/projet/python/.python-version)
  3.7.3

$ cat .python-version
3.6.8
```

La commande `pyenv` peut aussi changer la version de Python au niveau global, mais je ne le recommande pas. Attention à bien rétablir la situation normale avec `pyenv global system`. Sinon, certaines commandes utilisant Python (par exemple, les applications installées par le gestionnaire de paquets de votre distribution GNU/Linux) pourraient avoir des conflits de versions et ne plus fonctionner !

```c
$ cd /un/chemin/sans/fichier-python-version

$ python --version
Python 2.7.16

$ python3 --version
Python 3.7.3

$ pyenv global 3.5.3

$ python --version
Python 3.5.3

$ pyenv global 3.6.8

$ python --version
Python 3.6.8

$ python3 --version
Python 3.6.8

$ pyenv global system
```

Alternatives
============

* certains gestionnaires de paquets Python comme `conda` ;
* la conteneurisation, comme avec Docker ;
* les gestionnaires modernes de paquets comme `nix` et `guix`.

La prochaine dépêche (partie 5) abordera ces sujets. 🤓

[![La mascotte de Linux, Tux, en train de voler avec le logo Python sur sa cape et sur sa tenue. Attention, cette image peut ne pas s’afficher car elle est au format WebP et ce format n’est pas toujours pris en charge. Si tel est le cas, merci de nous le signaler dans les commentaires et nous rectifierons le tir pour les prochaines dépêches.](http://olibre.github.io/GreatTips/python/news/tux-python.png)](https://github.com/olibre/GreatTips/tree/master/python)

Remerciements
=============

Merci à tous les contributeurs (et les contributrices) de cette dépêche, et notamment à [Philippe F.](https://linuxfr.org/users/bluebird) pour avoir rédigé la moitié de cette dépêche et à [Ysabeau](https://linuxfr.org/users/ysabeau) pour avoir initié les illustrations de cette série de dépêches. 🤩 🎨 🖌 Continuons à participer aux prochaines dépêches. 👍 👏 👏 👏

Licence
=======

Cette dépêche est publiée sous [licence CC0](https://fr.m.wikipedia.org/wiki/Licence_CC0) (dans le domaine public dans les pays où c’est possible) pour permettre de la recopier, modifier, réutiliser et republier sans obligation de citer ses auteurs quelle que soit la loi de certains pays comme la France, qui oblige quand même à citer les auteurs. Au moins, cela montre l’intention des auteurs à autoriser le plagiat.

Tes astuces ?
=============

N’hésite pas à partager tes expériences, tes astuces et tes interrogations.

Appel à contribution
--------------------

Donne‐nous un coup de main pour la rédaction des dépêches à venir : [Conda et Docker](https://linuxfr.org/redaction/news/python-pour-noel-2019-partie-5-conda-docker), [Pip et Pipx](https://linuxfr.org/news/python-pour-noel-2019-partie-6-pip-et-pipx), [environnements virtuels](https://linuxfr.org/news/python-pour-noel-2019-partie-7-environnements-virtuels), [Pipenv](https://linuxfr.org/news/python-pour-noel-2019-partie-8-pipenv), [empaquetage](https://linuxfr.org/news/python-pour-noel-2019-partie-9-empaquetage), formateur de code, analyse statique, les apports des dernières versions Python ([`asyncio`](https://docs.python.org/fr/3/library/asyncio.html), [type hints](https://docs.python.org/fr/3/library/typing.html)…), entretiens avec des utilisateurs Python pas comme les autres… Par manque de contributions, la série initialement nommée « pour la rentrée 2019 » a été renommée en « pour Noël 2019 » ! Ton aide sera la bienvenue. 💚
