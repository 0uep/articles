---
URL:     https://linuxfr.org/news/python-partie-6-pip-et-pipx
Title:   Python 2019/2021 — partie  6 — Pip et Pipx
Authors: Philippe F, Oliver, Ysabeau, tisaac, yPhil, Yves Bourguignon, palm123, ted, yal et gusterhack
Date:    2019-09-28T11:15:54+02:00
License: CC0
Tags:    python, pip et pipx
Score:   5
---

Python 2019/2021 — partie  6 — Pip et Pipx
==========================================

Cette dépêche est la suite d’une série sur Python initiée en septembre 2019. Après un sommeil cryogénique de un an et demi, on repart en forme avec d’autres contenus Python à vous proposer: actualité, bonnes pratiques, astuces, témoignages…

Cette sixième partie explique les inconvénients de `pip` et présente l’alternative `pipx`, le tout avec plein d’astuces et de conseils pour bien s’en sortir. 🚀 🐍

Pour rappel, les dépêches précédentes :

* [Python — partie 1](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1) parlait de la popularité explosive du langage Python
* [Python — partie 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2) évoquait la fin du support de Python 2
* [Python — partie 3](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets) parlait des différentes façons d’installer Python et des gestionnaires de paquets Python
* [Python — partie 4](https://linuxfr.org/news/python-pour-noel-2019-partie-4-py-pyenv) vous présentait `py` et `pyenv` pour faciliter la gestion de plusieurs versions de Python en parallèle sur un poste
* [Python — partie 5](https://linuxfr.org/news/python-partie-5-nix-et-guix) vous faisait découvrir un autre moyen de gérer l’installation en parallèle de différentes versions de Python

[![Le logo de Python est entouré de petites icônes symbolisant la variété des domaines où s’applique Python, et, à droite, un joyeux barbu se tient derrière un écran d’ordinateur qui affiche « partie = 6, "Pip Pipx" \n print(partie) »](6.webp)](https://github.com/linuxfr.org/articles/tree/main/python/2019-2021-n6.webp)

----

* [Python — partie 1 ― Popularité](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1)
* [Python — partie 2 ― Python 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2)
* [Python — partie 3 — Installation de Python et de paquets](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets)
* [Python — partie 4 — Py Pyenv](https://linuxfr.org/news/python-pour-noel-2019-partie-4-py-pyenv)
* [Python — partie 5 — Nix (et Guix) ](https://linuxfr.org/news/python-partie-5-nix-et-guix)
* [Python — partie 7 — Environnements virtuels](https://linuxfr.org/news/python-pour-noel-202x-partie-7-environnements-virtuels)
* [Python— partie 8 — Pipenv](https://linuxfr.org/news/python-partie-8-pipenv)
* [Python — partie 11 — Entretiens](https://linuxfr.org/news/python-partie-11-entretiens)

----

La problématique de l’installation des paquets Python
=====================================================

Le gestionnaire de paquets des distributions GNU/Linux
------------------------------------------------------

Les distributions GNU/Linux fournissent des applications et bibliothèques Python. Les intégrateurs de ces paquets font très attention à la cohérence et la compatibilité entre les dépendances communes à toutes ces applications. Les dépendances et applications sont fournies, le plus souvent, dans des paquets séparés. De plus, les intégrateurs prennent en compte certains correctifs, notamment celles concernant les failles de sécurité. Nous avons donc des paquets Python compatibles entre eux, sans faille de sécurité, et dont la mise à jour est gérée automatiquement par le système.

Par contre, ces paquets sont bien souvent dans une seule version, et pas forcément dans la version la plus récente. Un autre inconvénient est le nombre limité de paquets Python disponibles via la distribution GNU/Linux.

C’est pour cela, que nous utilisons `pip` : pouvoir choisir la version exacte d’un paquet Python, et bien souvent la toute dernière version (voire une pré-version *(pre-release)*) ou pour installer des paquets Python qui ne sont pas fournis par votre distribution.

Le gestionnaire de paquets `pip`
--------------------------------

L’outil `pip` permet d’installer et de gérer des paquets Python directement en liaison avec le [Python Package Index](https://pypi.org/), dépôt qui rend ceux-ci accessibles à tout le monde via l’Internet.

Mais `pip` n’empêche pas d’installer des dépendances dans des versions incompatibles avec d’autres applications. Et cela nous arrive de temps en temps de *casser* une application :-( ! 

La bonne façon d’utiliser `pip`
===============================

Généralement, la documentation dit d’installer avec :

```
pip install nom_paquet
```

Comme on rencontre un problème de permission, on commence à vouloir bien faire avec :

```
sudo pip install "nom-du-module-python"    # en root
```

Ce qui rentre en conflit avec :

```
sudo apt install "autre-nom-du-meme-module-python"
sudo dnf install "autre-nom-du-meme-module-python"
sudo yum install "autre-nom-du-meme-module-python"
```

Pour éviter que `pip` (et `pip3`) écrase les fichiers installés par `apt`, sur Debian les deux installations sont séparées :

* `/usr/lib/python2.7/dist-packages` avec `apt`
* `/usr/local/lib/python2.7/dist-packages` avec `pip` 

Comme Python est très souvent utilisé par des outils de maintenance ou d’administration des machines, cela peut créer des problèmes : installation de versions de certains paquets directement à la place de ceux du système, ou encore installation de certains paquets pour l’utilisateur qui ont la priorité par rapport aux versions installées par le système. Il est très fortement conseillé d’utiliser des _environnements virtuels_ . Il est fortement déconseillé d’installer un paquet via `pip` dans le cadre d’une commande `sudo` (le meilleur moyen de casser votre système).

Le pire, c’est de mettre à jour `pip` avec lui-même, car `pip` nous le réclame : `pip install --upgrade pip` et cela a quelquefois comme conséquence de casser `pip` ! Installer des modules Python devient un bazar si on ne prend pas les bonnes pratiques dès le début.

[![Image Xkcd décrivant la complexité de l’installation des modules Python](https://imgs.xkcd.com/comics/python_environment_2x.png)](https://xkcd.com/1987/)

Cette problématique est très fréquente comme nous pouvons le constater sur le [ticket #5599 du projet `pip`](https://github.com/pypa/pip/issues/5599).

Bonnes pratiques :

1. Ne jamais utiliser `sudo pip` car la gestion des paquets (et des modules Python) du système est gérée par `apt`, `yum`, `dnf`…
2. Utiliser `pip install --user` pour installer des modules pour son besoin personnel sans écraser les modules Python du système ;
3. Ne pas utiliser `pip install` (même avec `--user`)

Les pratiques n°2 et n°3 rentrant en conflit, bien réfléchir avant d’installer un module Python avec `pip`. Est-ce que le module peut être installé avec `apt`, `yum`, `dnf` ? De quelle version avons-nous besoin ? Et pourquoi pas un environnement Python virtualisé ? Et un conteneur ?…

Bon, revenons à `pip`, supposons que nous décidions d’appliquer la pratique n°2 et de ne pas écouter la pratique n°3. Nous allons donc installer notre module en précisant **toujours** l’argument `--user` :

```sh
pip install "nom-du-module-python" --user
```

Attention, notre `pip` utilise peut-être Python 2, voici une meilleure ligne de commande :

```sh
pip3 install "nom-du-module-python" --user
```

Attention, nous pourrions avoir plusieurs versions Python 3 installées sur notre machine.
Voici une encore meilleure ligne de commande :

```sh
python3 -m pip install "nom-du-module-python" --user
```

Pour la différence entre `pip3` et `python3 -m pip` lire [les détails sur stackoverflow](https://stackoverflow.com/q/25749621/938111) (en anglais). En bref, on est sûr que `python3 -m pip` utilise la même arborescence d’installation que le script qui est exécuté avec `python3 « nom-du-script.py"` (ou `#!/usr/bin/env python3`). C’est d’autant plus recommandé si le `$PATH` de la machine est tarabiscoté, s’il y a plusieurs installations de Python sur l’ordinateur ou encore que la machine soit sous Windows.

Et si nous voulions préciser l’installation Python avec laquelle nous souhaitons travailler :

```sh
/chemin/vers/bin/python3 -m pip install "nom-du-module-python" --user
```

Attention, si nous avions une ancienne version du module python déjà installée sur notre machine, les commandes `pip` ci-dessus ne nous permettent pas d’installer la dernière version du module Python :-/

Ajoutons l’argument `--upgrade` :

```
python3 -m pip install "nom-du-module-python" --user --upgrade
```

Nous pouvons aussi changer la barre de progression :

```
python3 -m pip install "nom-du-module-python" --user --upgrade --progress-bar emoji
```

Et pour utiliser le module Python fraichement installé :

```sh
python3 -m "nom-du-module-python" [options du module]
```

Oui, cela devient compliqué ! Mais cette façon de faire, avec malheureusement de longues lignes de commande, va nous éviter bien des problèmes.

De plus, même en appliquant les recommandations 2 ou 3, si on installe un paquet pour utilisation avec le Python 3 standard de la machine, ceci peut casser le fonctionnement de certains programmes (le paquet ainsi installé étant prioritaire par rapport à celui du système, s’il y a des incompatibilités… boum). La bonne façon de faire est d'**utiliser des environnements virtuels** (où l’on peut [utiliser directement `pip`](https://pip.pypa.io/en/stable/quickstart/) sans risque). C’est une bonne pratique à adopter dès le début afin de s’éviter des problèmes ultérieurs. Cf la suite de la dépêche et la dépêche suivante sur Python où nous vous parlerons plus en détails des environnements virtuels.

## Sous Anaconda ou Miniconda avec conda

La société Continuum Analytics qui réalise ces distributions Python fournit des paquets déjà compilés pour de nombreuses bibliothèques Python (et autres langages), principalement dans le domaine des sciences et du calcul mais pas uniquement. Certaines de ces bibliothèques ne sont pas toujours triviales à reconstruire, particulièrement sous Windows. L’adoption d’Anaconda peut être une solution si l’installation de certains paquets échoue avec d'autres distributions.

Attention toutefois avec Anaconda ou Miniconda : ils ont tendance à être très gourmands en espace disque (on arrive assez rapidement à des Gio occupés).

Note : Sous Windows un menu d’application _Anaconda Prompt_ est ajouté dans le groupe de programmes _Anaconda_. Il permet d’accéder à `conda` même si celui-ci n’est pas accessible dans les répertoires du `PATH`.

Conda gère un environnement _base_, celui par défaut correspondant à son installation de Python, mais peut aussi gérer des environnements supplémentaires avec leurs propres installations de Python et des paquets (avec les versions au choix).

```bash
~$ conda activate base
(base) ~$ which python
/home/login/.miniconda3/bin/python
(base) ~$ conda install numpy

…(liste de paquets à installer/mettre à jour)…

Proceed ([y]/n)? y

…(téléchargement puis installation)…
```

Lorsqu’un paquet n’est pas disponible dans les dépôts de conda, on peut l’installer simplement à partir de [PyPI](https://pypi.org/) avec `pip`. Il faut juste prendre soin de lancer pip pour le Python fourni par conda :

```
(base)~$ conda install osc4py3
…
PackagesNotFoundError: The following packages are not available from current channels:

  - osc4py3
…
(base)~$ python -m pip install osc4py3
(base)~$ python
Python 3.6.9 |Anaconda, Inc.| (default, Jul 30 2019, 19:07:31) 
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import osc4py3
>>>
```

À noter : certains IDE comme [Pyzo](https://pyzo.org/) donnent directement accès aux commandes `conda` et `pip` dans leur fenêtre de shell Python.

Mettre à jour les paquets Python
================================

Avec le gestionnaire de paquets
--------------------------------

Les paquets installés avec les gestionnaires habituels sous Linux (`apt`, `yum`, `dnf`…) peuvent être mis à jours simplement avec ces mêmes gestionnaires. Ceux-ci assurent la cohérence des versions installées (et il vaut mieux ne pas interférer avec ce qu’ils installent). 

Voir pour chaque gestionnaire de paquets sa documentation pour faire des mises à jour système.

Avec pip
--------

On a vu qu’il était possible avec `pip` de mettre à jour un paquet particulier avec l'option `--upgrade`:

```
/chemin/vers/python -m pip install nom_du_paquet --user --upgrade
```

Mais il n’y a pas pour le moment de mise à jour automatique simple de l’ensemble des paquets installés avec pip. Celui-ci propose seulement un argument `--outdated` pour lister les paquets obsolètes. Avec un shell, en l’intégrant dans une expression en ligne de commande, il est toutefois possible de réaliser cette tâche :

```sh
/chemin/vers/python -m pip list --user --outdated --format freeze |
  cut -d= -f1 |
  xargs --no-run-if-empty /chemin/vers/python -m pip install --user --upgrade --progress-bar emoji
```

Sous macOS, il faut retirer l’argument `--no-run-if-empty` de l’exemple ci-dessus.

Notons que de nombreuses applications système sont codées en Python. Mettre à jour les modules et leurs dépendances même avec l’argument `--user` peut changer le comportement des applications exécutées par l’utilisateur. Par exemple, si nous utilisons [`meld`](https://doc.ubuntu-fr.org/meld) en ligne de commande pour comparer deux fichiers, `meld` pourrait ne plus fonctionner correctement. C’est qu’il fallait respecter la bonne pratique n°3 ! (lire aussi le [commentaire de lolop](https://linuxfr.org/users/oliver_h/journaux/quelques-bonnes-pratiques-python-pour-2019#comment-1766432))

Pour l’anecdote, un jour, Oliver décide de mettre à jour ses modules Python dont un module `redis` qui avait été installé à partir d’un fichier `requirements.txt` avec une version précise. Sans s’en rendre compte ce module passait de la version 2 à la version 3 avec une [incompatibilité dans l’appel des fonctions](https://pypi.org/project/redis/#upgrading-from-redis-py-2-x-to-3-0). Benoît Sibaud a eu un souci similaire avec [pyOpenssl en conflit avec la version fournie par le gestionnaire de paquets de la distrib](https://linuxfr.org/users/oliver_h/journaux/quelques-bonnes-pratiques-python-pour-2019#comment-1766396). C’est à ce moment-là que l’on comprend pourquoi `pip` ne permet pas de mettre à jour tous les modules d’un coup !

Si quelqu’un s’amuse à mettre à jour tous tes modules avec `pip`, il serait prudent de prendre quand même des précautions comme enregistrer préalablement les versions des modules avant la mise à jour :

```
python3 -m pip list --user --format freeze > ~/requirements_avant_pip_upgrade.txt

python3 -m pip list --user --outdated --format freeze |
  cut -d= -f1 |
  xargs --no-run-if-empty python3 -m pip install --user --upgrade --progress-bar emoji

python3 -m pip list --user --format freeze > ~/requirements_apres_pip_upgrade.txt
```

Pour visualiser les changements :

```
sudo apt install meld

meld ~/requirements_avant_pip_upgrade.txt ~/requirements_apres_pip_upgrade.txt
```

En cas de problème, revenir aux versions précédentes :

```
python3 -m pip install --user -r ~/requirements_avant_pip_upgrade.txt
```

## Avec Conda

Pour les paquets fournis via _Anaconda_ ou _Miniconda_, une simple commande exécutée dans l’environnement conda activé permet d’effectuer les mises à jour _dans cet environnement_ :

```bash
(base) ~$ conda update --all
…
```

Environnement Python virtualisé
==============================

Alors, utiliser `pip` est dangereux ? Oui, sauf dans un **environnement Python virtualisé**. \o/

L’idée est d’avoir une installation des paquets Python spécifique pour chacun de ses projets, avec une maîtrise des versions et des dépendances, et qui n’interfère pas avec l’installation standard des paquets par le système. Et le tout versionné avec le code source de son projet. Ainsi nous avons une installation équivalente pour les différents développeurs et la production.

Quelques outils pour créer des environnements virtualisés :

* [*`python -m venv`*](https://docs.python.org/fr/3.9/library/venv.html) fait partie des piles fournies avec Python ;
* [*`virtualenv`*](https://github.com/pypa/virtualenv) est l’ancêtre de `venv` mais il continue d’évoluer et il est bien plus utilisé que `venv` ([article en français](https://python-guide-pt-br.readthedocs.io/fr/latest/dev/virtualenvs.html)) ;
* [*`virtualenvwrapper`*](https://virtualenvwrapper.readthedocs.io/en/latest/) est une série d’extensions pour `virtualenv` ;
* [*`pipenv`*](https://github.com/pypa/pipenv) est une surcouche agréable au-dessus de `virtualenv` et de `pip` ;
* [*`conda`*](https://en.wikipedia.org/wiki/Conda_(package_manager)) gère aussi des environnements virtuels, et propose un certain nombre de bibliothèques pré-packagées en supplément à `pip` ;
* [*`pipx`*](https://pipxproject.github.io/pipx/) crée un environnement virtuel pour chaque programme Python du système, que l’on souhaite protéger d’un cassage accidentel par mise à jour des dépendances.

`pipx` pour ne plus utiliser `pip`
=================================

Comme nous le disions, malgré tout le soin apporté à la préparation d’un paquet Python par un développeur et au contrôle soigné de ses dépendances, il arrive que nous cassions de façon incontrôlée des dépendances de paquets Python.

Le cas typique est par exemple un paquet fournissant un utilisateur en ligne de commande, disons `supertoto`, qui dépend du paquet `super` en version 1. Par la suite, vous installez un autre utilitaire, `supertiti`, qui dépend aussi du paquet `super` mais en version 3. Lors de l’installation de `supertiti`, le paquet `super` va être mis à jour vers la version 3, qui malheureusement n’est pas rétro-compatible avec la version 1. Vous venez de casser `supertoto`.

Pour éviter ce type de problème d’interférence entre les différentes dépendances installées avec `pip`, l’astuce est d’installer chaque application et ses dépendances dans un environnement isolé.

Et voilà, [**`pipx`**](https://pipxproject.github.io/pipx/), une alternative à `pip`, mais uniquement pour l’installation d’applications Python. Le gestionnaire de paquets `pipx` n’a pas été conçu pour l’installation de bibliothèques Python (les dépendances).

L’outil `pipx` installe chaque application dans un environnement virtuel avec `venv`. Ainsi, plus de conflit entre les différents paquets applicatifs et leurs dépendances respectives, et donc plus besoin de s’embêter avec les environnements virtuels.

Quant à l’outil `pip`, il peut être relégué à une seule utilisation : installer `pipx` (un peu comme, sous Windows, le navigateur Explorer/Edge ayant pour seule utilité de télécharger Firefox). On peut aussi installer `pipx` avec `apt`/`dnf`/`nix-env`/… Les puristes considèrent même que `pip` est volontairement dissocié de l’installation de Python pour permettre d’utiliser `pipx` sans jamais devoir passer par `pip` !

En fait, d’autres outils se basent sur `pip` comme `pipenv`, il vaut donc mieux garder un `pip` fonctionnel sur son ordi. 😁 Les deux outils `pip` et `pipx` cohabitent très bien, chacun avec ses avantages. 👍

Installation avec `pip` :

```
/usr/bin/python3 -m pip install --user --upgrade pipx
```

Le plus dur est de prendre l’habitude d’utiliser `pipx` à la place de `pip`. Allez, on commence par désinstaller les applications préalablement installées avec `pip` :

```bash
/usr/bin/python3 -m pip uninstall black flake8 pipenv poetry meld
```

On résinstalle avec `pipx` :

```bash
$ /usr/bin/python3 -m pipx install black
  installed package black 19.3b0, Python 3.7.4
  These apps are now globally available
    - black
    - blackd
done! ✨ 🌟 ✨
```

Il se souvient bien sûr que l’installation a déjà été faite :

```bash
$ /usr/bin/python3 -m pipx install black
'black' already seems to be installed. Not modifying existing installation in '/home/o/.local/pipx/venvs/black'. Pass '--force' to force installation.
```

D’autres utilitaires sympathiques en ligne de commande, à installer avec pipx :

```bash
$ /usr/bin/python3 -m pipx install pipenv
  installed package pipenv 2018.11.26, Python 3.7.4
  These apps are now globally available
    - pipenv
    - pipenv-resolver
done! ✨ 🌟 ✨
```

```bash
$ /usr/bin/python3 -m pipx install poetry
  installed package poetry 0.12.17, Python 3.7.4
  These apps are now globally available
    - poetry
done! ✨ 🌟 ✨
```

```bash
$ /usr/bin/python3 -m pipx install flake8
  installed package flake8 3.7.8, Python 3.7.4
  These apps are now globally available
    - flake8
done! ✨ 🌟 ✨
```

```bash
$ /usr/bin/python3 -m pipx install meld --include-deps
⚠️  File exists at /home/o/.local/bin/futurize and points to /home/o/.local/bin/futurize, not /home/o/.local/pipx/venvs/meld/bin/futurize. Not modifying.
⚠️  File exists at /home/o/.local/bin/pasteurize and points to /home/o/.local/bin/pasteurize, not /home/o/.local/pipx/venvs/meld/bin/pasteurize. Not modifying.
  installed package meld 0.2.3, Python 3.7.4
  These apps are now globally available
    - f2py
    - f2py3
    - f2py3.7
done! ✨ 🌟 ✨
```

Notons l'option `--include-deps` nécessaire pour installer `meld`.

Tes astuces ?
=============

N’hésite pas à partager tes expériences, tes astuces et tes interrogations.

Licence
=======

Cette dépêche est publiée sous [licence CC0](https://fr.m.wikipedia.org/wiki/Licence_CC0) (en domaine public dans les pays où cela est possible) pour permettre de la recopier, modifier, réutiliser et republier sans obligation de citer ses auteurs. Sauf dans certains pays, comme la France, dont la loi oblige quand même à citer les auteurs. Au moins, cela montre l’intention des auteurs à autoriser le plagiat.
