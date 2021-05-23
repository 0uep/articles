---
URL:     https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets
Title:   Python 2019/2021 — partie 3 — Installation de Python et de paquets
Authors: Oliver, lolop, ZeroHeure, Ysabeau, Étienne BERSAC, Davy Defaud, eggman, Adrien Dorsaz, palm123, Benoît Sibaud, M5oul, Cetera, Dimitri Merejkowsky, barmic, tisaac, Florent Zara et Bruno Michel
Date:    2019-09-03T05:30:20+02:00
License: CC0
Tags:    python, python3, 2019, pip, pipenv et python2
Score:   23
---

Python 2019/2021 — partie 3 — Installation de Python et de paquets
==================================================================

Pour cette rentrée 2019, faisons le point sur Python : actualité, bonnes pratiques, astuces, projets intéressants, témoignages…

Cette troisième dépêche présente différentes façons d’installer Python, ainsi que l’installation de paquets supplémentaires : applications et bibliothèques Python.  🖥 💻 🐍

[![Python installation](03.webp)](https://github.com/linuxfrorg/articles/tree/main/python/2019-2021)

----

* [Sam&Max : Lancer correctement Python et ses commandes cousines](http://sametmax.com/lancer-correctement-python-et-ses-commandes-cousines/)
* [Partie 1 : Popularité de Python](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1)
* [Partie 2 : Python 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2)

----

Licence
=======

Cette dépêche est publiée sous [licence CC0](https://fr.m.wikipedia.org/wiki/Licence_CC0) (sous domaine publique dans les pays où cela est possible) pour te permettre de recopier, modifier, réutiliser et republier ce contenu sans t’obliger à citer ses auteurs (sauf que la loi de certains pays comme la France t’oblige quand même à citer les auteurs).

Remerciements
=============

Un immense merci à _[lolop](https://linuxfr.org/users/lolop)_ et [Étienne Bersac](https://linuxfr.org/users/bersace) pour leurs nombreuses contributions aux dépêches Python. 👏 👏 👏 Merci aussi à toutes les autres personnes qui ont participé à leur rédaction. 😉 Continuons à améliorer les prochaines dépêches. ✍😎

Les interpréteurs Python
========================

L’interpréteur Python de référence, [**CPython**](https://fr.wikipedia.org/wiki/CPython), est distribué par la [Python Software Foundation](https://www.python.org/psf-landing/). Il met en œuvre les évolutions du langage pilotées par la communauté.

D’autres interpréteurs Python existent toutefois :

* [MicroPython](https://fr.wikipedia.org/wiki/MicroPython) et [CircuitPython](https://github.com/adafruit/circuitpython), pour l’embarqué ;
* [Jython](https://fr.wikipedia.org/wiki/Jython) et [IronPython](https://fr.wikipedia.org/wiki/IronPython), pour la compilation vers le _bytecode_ des plates‑formes, respectivement Java et CLR.NET de Microsoft (tous deux limités en Python 2) ;
* [Brython](http://brython.info/), pour l’utilisation côté butineur Web ;
* le projet de recherche [PyPy](https://fr.wikipedia.org/wiki/PyPy), qui compile à la volée (_just‑in‑time_) le code Python pour l’exécuter plus rapidement ;
* [Anaconda](https://fr.wikipedia.org/wiki/Anaconda_(Python_distribution)) et [Miniconda](https://stackoverflow.com/a/45421204/938111), très utilisés par les scientifiques [des données](https://fr.wikipedia.org/wiki/Science_des_données) (_data scientists_) et de [l’apprentissage automatique](https://fr.wikipedia.org/wiki/Apprentissage_automatique) (_machine learning_) ;
* [ActivePython](https://wiki.python.org/moin/ActivePython) ;
* [Pyston](https://github.com/dropbox/pyston) ;
* [Stackless](https://fr.wikipedia.org/wiki/Stackless_Python) ;
* [etc.](https://wiki.python.org/moin/CategoryImplementations)

Les distributions Python
========================

L’interpréteur Python et tout son écosystème de paquets qui gravite autour représente un ensemble de logiciels : une distribution.

La distribution de référence est disponible sur _[www.python.org](http://www.python.org)_. Elle fournit un ensemble déjà conséquent de bibliothèques standards (« piles inclues »), et permet d’installer beaucoup d’autres paquets Python fournis par la communauté, le plus souvent sous licence libre. Les autres distributions se basent généralement sur l’interpréteur de référence CPython, en y ajoutant leurs propres touches.

Une autre distribution très utilisée est [Anaconda](https://fr.wikipedia.org/wiki/Anaconda_(Python_distribution)), surtout par les [scientifiques des données](https://fr.wikipedia.org/wiki/Science_des_données) (_data scientist_) et de [l’apprentissage automatique](https://fr.wikipedia.org/wiki/Apprentissage_automatique) (_machine learning_). La distribution Anaconda fournit les paquets standards de Python ainsi que d’autres paquets déjà compilés qui peuvent être difficiles à installer sous Windows ou macOS (besoin de compilation de code C ou Fortran).

Cette distribution est toutefois très volumineuse, car elle installe de très nombreux outils et applications. L’alternative [Miniconda](https://docs.conda.io/en/latest/miniconda.html), est une distribution plus légère et basée sur le même outil de gestion de paquets [`conda`](https://docs.conda.io/en/latest/). Miniconda permet de sélectionner plus finement les paquets à installer.

D’autres distributions Python existent comme [ActivePython](https://wiki.python.org/moin/ActivePython), [WinPython](https://winpython.github.io/) ou encore [Python(x,y)](http://python-xy.github.io/). N’hésitez pas à partager dans les commentaires vos retours d’expériences et vos recommandations.

**Note** : Il est possible de faire cohabiter sur la même machine différentes distributions de Python. Il est aussi possible d’installer différent versions de Python. Le problème ensuite est de lancer le bon exécutable lorsqu’on tape `python3`. Sans précision, ça sera le premier exécutable `python3` trouvé dans les répertoires du `PATH`. On doit spécifier `/chemin/vers/python` pour y choisir un exécutable particulier. Et si l’on utilise un « environnement virtuel », l’exécutable `python` est celui lié à cet environnement.

Installation de Python
======================

De nombreux lectrices et lecteurs de _LinuxFr.org_ utilisent Windows, et sont bien souvent forcés (boulot, enseignement). Nous avons donc décidé d’expliquer également l’installation de Python pour Windows. Les lectrices et lecteurs sous macOS ne sont pas non plus oubliés. Nos excuses pour celles et ceux sous *BSD, Haiku, Illumos, OpenIndiana, GNU Hurd, ReactOS, AROS, Android, iOS…

GNU/Linux
---------

Les deux distributions les plus utilisées sont la distribution de référence, **CPython**, et **Miniconda**. Voici quelques méthodes d’installation.

### Installation de CPython via les paquets fournis par sa distribution

Attention le paquet `pip` est fourni à part. Ci‑dessous un exemple pour Ubuntu. Je recommande l’installation des paquets `python3‑dev` et `build‑essential` qui pourraient être nécessaires quand `pip` (ou `pipenv`) installent certains paquets nécessitant une compilation de dépendances basées sur d’autres langages de programmation comme C et Fortran.

    sudo apt update
    sudo apt install python3 python3-pip
    sudo apt install python3-dev build-essential

### Installation du [snap](https://doc.ubuntu-fr.org/snap) `conda`

Avec, par exemple, la logithèque Ubuntu (GNOME Software), ou la ligne de commande ci‑dessous :

```sh
sudo apt install snapd
sudo snap install --beta conda  # version stable pas dispo
```

Exemple pour chercher et installer le paquet Python [`black`](https://github.com/psf/black) :

    $ conda search black
    Loading channels: done
    # Name Version Build Channel
    black 19.3b0 py_0 pkgs/main
    $ conda install black
    […]

Notons que le [snap `conda`](https://snapcraft.io/conda) n’est pas indiqué comme libre.
Attention à l’espace de stockage disponible, Miniconda et Anaconda ont tendance à **être très gourmands**, on arrive assez rapidement à des gigaoctets occupés.

### Utilisation d’environnements virtuels avec des versions de Python spécifiques

C’est l’objet de la dépêche suivante (et est aussi permis avec `conda`).

Il est également possible de télécharger des exécutables et de les installer à la main. Miniconda et Anaconda sont disponibles sous cette forme. Attention à vérifier que les logiciels proviennent bien d’une source de confiance et à les exécuter, si possible, dans un bac à sable (_sandbox_). Voir le projet [Firejail](https://github.com/netblue30/firejail).

macOS
-----

macOS fournit de base Python 2.7 :

    $ python --version
    Python 2.7.15

Voici quatre possibilités pour installer Python 3 sur macOS :

1. le site _python.org_ fournit [CPython pour macOS](https://www.python.org/downloads/mac-osx/), qui nécessite une petite centaine de mégaoctets ;
2. si [HomeBrew](https://brew.sh/index_fr) est installé, celui‑ci permet d’installer CPython empaqueté par la communauté :

        $ brew install python3
        $ python3 --version
        Python 3.7.0

3. la distribution [Miniconda](https://docs.conda.io/en/latest/miniconda.html) ;
4. la distribution [Anaconda](https://www.anaconda.com/distribution/#download-section).

Windows
-------

Toutes les versions de CPython sont sur le [site officiel](https://www.python.org/downloads/windows/). Les installateurs *executable installer* et *web‑based installer* simplifient l’installation.

Comme expliqué par Sam dans son article « [Lancer correctement Python et ses commandes cousines](http://sametmax.com/lancer-correctement-python-et-ses-commandes-cousines/) », ne pas oublier de mettre le répertoire des exécutables Python dans la variable d’environnement `%PATH%`. L’installateur propose de le faire en cochant la case « **[✓] Add Python 3.7 to PATH** » :
![Fenêtre de l’installateur de Python 3.7 avec la case à cocher pour rajouter l’exécutable Python dans la variable d’environnement PATH](http://sametmax.com/wp-content/uploads/2019/06/python37_win_installer.png "Fenêtre de l’installateur de Python 3.7 avec la case à cocher pour rajouter l’exécutable Python dans la variable d’environnement PATH")

Citons une manière familière pour les _[Ubunteros](https://en.wiktionary.org/wiki/Ubunteros)_ d’installer CPython : avec le [Windows Subsystem for Linux](https://fr.wikipedia.org/wiki/Windows_Subsystem_for_Linux) (WSL). Pour cela, choisir une image GNU/Linux, par exemple l’image Ubuntu, et ouvrir un terminal avec un interpréteur de commandes de type Bash. Avec la nouvelle version WSL2, les applications graphiques GNU/Linux devraient aussi pouvoir s’exécuter sur Windows et avec des performances acceptables.

Téléchargez les alternatives [Miniconda](https://docs.conda.io/en/latest/miniconda.html) et [Anaconda](https://www.anaconda.com/distribution/#download-section) pour les installer.

Lire aussi la description, étape par étape, de l’[installation d’Anaconda sous Windows](https://perso.limsi.fr/pointal/python: installation: accueil#windows).

![Quel python adopter ?](http://olibre.github.io/GreatTips/python/news/quel-python-adopter.png)

Installer des paquets Python
============================

Sous GNU/Linux, avec le gestionnaire de paquets
-----------------------------------------------

Les gestionnaires de paquets des distributions GNU/Linux fournissent un certain nombre de bibliothèques Python. Leur installation via ces outils permet de s’assurer qu’elles seront compatibles avec la version de Python installée en standard par le système, et mises à jour lorsque nécessaire. En revanche, elles ne seront peut‐être pas dans la version la plus récente disponible. L’installation de cette façon rend ces bibliothèques disponibles pour tous les utilisateurs de l’ordinateur.

**Attention lors de l’installation**, ces bibliothèques sont souvent empaquetées séparément pour Python 2 et pour Python 3 ; en général la version de Python est spécifiée dans le nom du paquet.

Exemple sous Debian/Ubuntu : `sudo apt install python3-exif`.

Sous n’importe quel système d’exploitation, avec `pip`
------------------------------------------------------

L’outil `pip` permet d’installer et de gérer des paquets Python directement en liaison avec le [Python Package Index](https://pypi.org/) ; dépôt qui rend ceux‑ci accessibles à tout le monde via l’Internet.

**Attention**, pour les personnes qui disposent d’outils de gestion de paquets pour le système de leur ordinateur (typiquement tous les UNIX), `pip` vient en concurrence. Comme Python est très souvent utilisé par des outils de maintenance ou d’administration des machines, cela peut causer des problèmes : installation de versions de certains paquets directement à la place de ceux du système, ou encore installation de certains paquets pour l’utilisateur qui ont la priorité par rapport aux versions installées par le système. Il est très fortement conseillé d’utiliser des environnements virtuels, comme cela est présenté dans la dépêche suivante. Il est **prohibé** d’installer un paquet via `pip` dans le cadre d’une commande `sudo` (cela risque de casser votre système).

Normalement `pip` est installé directement (ou disponible dans les paquets de votre distribution GNU/Linux). Si ce n’est pas le cas, un script [`get-pip.py`](https://pip.pypa.io/en/stable/installing/) permet de le mettre en place sur n’importe quelle plate‑forme.

La **bonne façon** d’utiliser `pip` est de demander à l’exécutable Python pour lequel on veut installer un paquet de charger `pip` afin de réaliser cette installation :
`/chemin/vers/python -m pip install nom_du_paquet --user --upgrade`.
Les autres façons de faire que l’on peut trouver sur l’Internet (typiquement `pip install nom_du_paquet`) sont à éviter. Mais dans le cas d’un « environnement virtuel », on peut saisir `python` sans spécifier le chemin d’accès et utiliser la commande `pip` — tous deux sont issus de l’environnement virtuel.

Les options courantes :

* `--user` indique d’installer le paquet dans un répertoire personnel de l’utilisateur, lié au Python concerné (cela évite d’aller écraser les paquets fournis par d’autres moyens) ; il n’est pas nécessaire de l’utiliser avec un _environnement virtuel_ ;
* `--upgrade` (ou `-U`) indique en plus de mettre à jour un paquet déjà installé vers la version la plus récente disponible.

Mais, même en utilisant l’option `--user`, si l’on installe un paquet pour une utilisation avec le Python 3 standard de la machine, ceci peut casser le fonctionnement de certains programmes (le paquet ainsi installé étant prioritaire par rapport à celui du système, s’il y a des incompatibilités… boum). La bonne façon de faire est d’**utiliser des environnements virtuels** (où l’on peut [utiliser directement `pip`](https://pip.pypa.io/en/stable/quickstart/) sans risque). C’est une bonne pratique à adopter dès le début afin de s’éviter des problèmes ultérieurs.

## Sous Anaconda ou Miniconda avec `conda`

Le [gestionnaire de paquets](https://fr.wikipedia.org/wiki/Gestionnaire_de_paquets) [`conda`](https://en.wikipedia.org/wiki/Conda_(package_manager)) est développé pour [Anaconda](https://fr.wikipedia.org/wiki/Anaconda_(Python_distribution)), disponible sur Windows, GNU/Linux et macOS.

La société qui le produit (ex‑Continuum Analytics, maintenant Anaconda) fournit des paquets déjà compilés pour de nombreuses bibliothèques Python (et autres langages), principalement dans le domaine des sciences et du calcul, mais pas uniquement. Certaines de ces bibliothèques ne sont pas toujours triviales à reconstruire, particulièrement sous Windows. L’adoption d’Anaconda peut être une solution si l’installation de certains paquets échoue avec d’autres distributions ; entre autres, par exemple, pour travailler localement sur des calepins (_notebooks_) [Jupyter](https://fr.wikipedia.org/wiki/Jupyter).

**Notes** :

* les paquets absents de cette distribution peuvent être installés normalement avec `pip` ;
* sous Windows, un menu d’application _Anaconda Prompt_ est ajouté dans le groupe de programmes _Anaconda_, il permet d’accéder à `conda` même si celui‑ci n’est pas accessible dans les répertoires du `PATH`.

Conda gère un environnement _base_, celui par défaut correspondant à son installation de Python, mais peut aussi gérer des environnements supplémentaires avec leurs propres installations de Python et des paquets (avec les versions au choix).

```bash
~$ conda activate base
(base) ~$ which python
/home/login/.miniconda3/bin/python
(base) ~$ conda install numpy

… (liste de paquets à installer ou mettre à jour)…

Proceed ([y]/n) ? y

… (téléchargement, puis installation)…
```

Lorsqu’un paquet n’est pas disponible dans les dépôts de `conda`, on peut l’installer simplement à partir de [PyPI](https://pypi.org/) avec `pip` :

```
(base)~$ conda install osc4py3
…
PackagesNotFoundError: The following packages are not available from current channels:

- osc4py3
…
(base)~$ python -m pip install osc4py3
(base)~$ python
Python 3.6.9 |Anaconda, Inc.| (default, Jul 30 2019, 19:07:31)
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import osc4py3
>>>
```

**À noter** : certains IDE comme [Pyzo](https://pyzo.org/) donnent directement accès aux commandes `conda` et `pip` dans leur fenêtre d’interpréteur de commandes Python.

Mettre à jour les paquets Python
================================

Avec le gestionnaire de paquets
-------------------------------

Les paquets installés avec les gestionnaires habituels sous GNU/Linux (`apt`, `yum`, `dnf`, `urpmi`…) peuvent être mis à jour simplement avec ces mêmes gestionnaires. Ceux‐ci assurent la cohérence des versions installées (et il vaut mieux ne pas interférer avec ce qu’ils installent).

Avec `pip`
----------

La commande `python3 -m pip` permet de mettre à jour un paquet particulier avec l’option `--upgrade` :

    /chemin/vers/python3 -m pip install nom_du_paquet --user --upgrade

Mais il n’y a pas pour le moment de mise à jour automatique simple de l’ensemble des paquets installés avec `pip`. Celui-ci propose seulement un argument `--outdated` pour lister les paquets obsolètes. Avec un shell, en l’intégrant dans une expression en ligne de commande, il est toutefois possible de réaliser cette tâche :

```sh
/chemin/vers/python -m pip list --user --outdated --format freeze |
    cut -d= -f1 |
    xargs --no-run-if-empty /chemin/vers/python -m pip install --user --upgrade --progress-bar emoji
```

Sous macOS, retirer l’argument `--no-run-if-empty` de l’exemple ci‑dessus.

En cas de mise à jour des modules avec `pip`, il est possible d’enregistrer préalablement les versions des modules avant ou après la mise à jour :

```
python3 -m pip list --user --format freeze > ~/requirements_avant_pip_upgrade.txt

python3 -m pip list --user --outdated --format freeze |
    cut -d= -f1 |
    xargs --no-run-if-empty python3 -m pip install --user --upgrade --progress-bar emoji

python3 -m pip list --user --format freeze > ~/requirements_apres_pip_upgrade.txt
```

On peut ensuite visualiser les changements en affichant les différences entre les deux fichiers générés, par exemple avec l’outil `meld` :

```
meld ~/requirements_avant_pip_upgrade.txt ~/requirements_apres_pip_upgrade.txt
```

Et si besoin, en cas de problème, revenir aux versions précédentes :

```
python3 -m pip install --user -r ~/requirements_avant_pip_upgrade.txt
```

## Avec `conda`

Pour les paquets fournis via _Anaconda_ ou _Miniconda_, une simple commande exécutée dans l’environnement `conda` activé permet d’effectuer les mises à jour _dans cet environnement_ :

```bash
~$ conda activate base

(base) ~$ conda update --all
```

Comment bien faire
==================

Alors, utiliser `pip` est‑il dangereux ? Oui, sauf dans un **environnement Python virtualisé**. \o/ C’est l’objet du prochain article de cette série.

Tes astuces ?
=============

N’hésite pas à partager tes expériences, tes astuces et tes interrogations. Quel est le meilleur interpréteur Python ? Pour quel usage ? Le plus performant ? Des différences de fonctionnement ? Avec quel système d’exploitation ?