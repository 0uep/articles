---
URL:     https://linuxfr.org/news/python-partie-7-environnements-virtuels
Title:   Python 2019/2021 — partie 7 — Environnements virtuels
Authors: Oliver
         lolop, Ysabeau, Axone, bobble bubble, tisaac, Di3s3L, gusterhack et ted
Date:    2019-09-16T05:22:02+02:00
License: CC0
Tags:    python
Score:   33
---

Python 2019/2021 — partie 7 — Environnements virtuels
=====================================================

Cette septième dépêche présente les environnements virtuels Python et ses alternatives comme la conteneurisation, le tout avec plein d’astuces et de conseils pour bien s’en sortir. 🚀 🐍

[![Le logo de Python est entouré de petites icônes symbolisant la variété des domaines où s’applique Python, et, à droite, un joyeux barbu se tient derrière un écran d’ordinateur qui affiche « partie = 7, "Env. Virtuels" \n print(partie) »](07.webp)](https://github.com/linuxfrorg/articles/tree/main/python/2019-2021)

----

* [Python — partie 1 ― Popularité de Python](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1)
* [Python — partie 2 ― Python 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2)
* [Python ―Partie 3  ― Installation](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets)
* [Hors série : Python revient dans la course face à JS & TS](https://linuxfr.org/users/oliver_h/journaux/python-pour-la-rentree-2019-hors-serie-python-revient-dans-la-course-face-a-node-js-8fa9db9e-c045-4136-8618-9044e69f56e0)
* [Python — partie 4 ― Py Pyenv](https://linuxfr.org/news/python-pour-noel-2019-partie-4-py-pyenv)
* [Python — partie 5 ― Nix (et Guix)](https://linuxfr.org/news/python-pour-noel-202x-partie-5-nix-et-guix)
* [Critique des environments virtuels](https://lwn.net/Articles/757354/)
* [Sam&Max - Les environnements virtuels Python : venv, virtualenv et virtualenvwrapper](http://sametmax.com/les-environnement-virtuels-python-virtualenv-et-virtualenvwrapper/)
* [Sam&Max - pipenv, solution moderne pour remplacer pip et virtualenv](http://sametmax.com/pipenv-solution-moderne-pour-remplacer-pip-et-virtualenv/)
* [Sam&Max - Mieux que Python virtualenvwrapper : pew](http://sametmax.com/pipenv-solution-moderne-pour-remplacer-pip-et-virtualenv/)

----

Environnement Python virtualisé, quésaco
========================================

L’idée est d’avoir une installation d'une version de Python et de paquets spécifiques pour chacun de ses projets, avec une maîtrise des versions et des dépendances, et qui n'interfère pas avec l'installation standard des paquets par le système. Et le tout versionné avec le code source de son projet. Ainsi nous avons une installation équivalente pour les différents développeurs et la production.

Quelques outils pour créer des environnements virtuels :

* [**`virtualenv`**](https://github.com/pypa/virtualenv), pour Linux / macOS / Windows, est l’ancêtre, continue d’évoluer et toujours très utilisé ([article en français](https://python-guide-pt-br.readthedocs.io/fr/latest/dev/virtualenvs.html)) ;
* [**`venv`**](https://docs.python.org/fr/3.9/library/venv.html) est l'intégration de *`virtualenv`* dans le cœur de Python, mais il est paradoxalement moins utilisé que son ancêtre *`virtualenv`* car *`venv`* est plus basique ;
* [**`virtualenvwrapper`**](https://virtualenvwrapper.readthedocs.io/en/latest/) est un ensemble de commandes bien pratiques pour étendre les possibilités de `virtualenv` tout en le gardant simple d'usage, avec des portages pour Windows ([shell cmd](https://pypi.org/project/virtualenvwrapper-win/) et [PowerShell](https://pypi.org/project/virtualenvwrapper-powershell/2.7.1/)) ;
* [**`pew`**](https://github.com/berdario/pew) est aussi complet et plus simple que `virtualenvwrapper` ;
* [**`pipenv`**](https://github.com/pypa/pipenv) (Linux / macOS / Windows) unifie `pip` et `virtualenv` afin de simplifier d'avantage la gestion des environnements virtuels et la gestion des dépendances (versions) et sera abordé dans la prochaine dépêche ;
* [**`conda`**](https://en.wikipedia.org/wiki/Conda_(package_manager)), pour Linux / macOS / Windows,  gère aussi des environnements virtuels, et propose un certain nombre de bibliothèques pré-paquagées en supplément à `pip`.

Nous allons également présenter [**`pyenv`**](https://github.com/pyenv/pyenv) pour l'installation de différentes versions de Python et l'activation rapide d'une des différentes installations de Python pour un même projet.

L'ancêtre `virtualenv`
======================

L'outil historique donc, encore très utilisé et qui sert de base pour certaines surcouches. Il est généralement déjà paquagé dans les distributions Linux, et est donc installable par votre gestionnaire de paquets. Sinon, à installer avec `pip` :

```sh
/usr/bin/python3 -m pip install --user --upgrade virtualenv
```

L'environnement virtuel se crée dans un sous-répertoire, nommé `.env-truc` dans l'exemple ci-dessous :

```c
$ cd /chemin/vers/le/projet
$ /usr/bin/python3 -m virtualenv .env-truc
  No LICENSE.txt / LICENSE found in source
New python executable in /tmp/truc/.env-truc/bin/python3
Also creating executable in /tmp/truc/.env-truc/bin/python
Installing setuptools, pip, wheel...
done.
```

ou directement :

```sh
/usr/bin/python3 -m virtualenv /chemin/vers/le/projet/.env-truc
```

Le répertoire `.env-truc` contient tout ce qui est nécessaire à l’interpréteur Python avec ses commandes et ses bibliothèques. Cet environnement de travail est indépendant des paquets déjà installés sur la machine :

```c
$ $ tree -d -L 4 .env-truc/
.env-truc/
├── bin
├── include
│   └── python3.7m -> /usr/include/python3.7m
├── lib
│   └── python3.7
│       ├── collections -> /usr/lib64/python3.7/collections
│       ├── config-3.7m-x86_64-linux-gnu -> /usr/lib64/python3.7/config-3.7m-x86_64-linux-gnu
│       ├── distutils
│       │   └── __pycache__
│       ├── encodings -> /usr/lib64/python3.7/encodings
│       ├── importlib -> /usr/lib64/python3.7/importlib
│       ├── lib-dynload -> /usr/lib64/python3.7/lib-dynload
│       ├── __pycache__
│       └── site-packages
│           ├── pip
│           ├── pip-19.2.3.dist-info
│           ├── pkg_resources
│           ├── __pycache__
│           ├── setuptools
│           ├── setuptools-41.2.0.dist-info
│           ├── wheel
│           └── wheel-0.33.6.dist-info
└── lib64 -> lib
```

Pour entrer dans le shell de cet environnement isolé :

* Sous GNU/Linux et macOS : `source /chemin/vers/le/projet/.env-truc/bin/activate`
* Sous Windows : `C:\\chemin\vers\le\projet\.env\bin-truc\activate\Scripts\activate.bat`

Le prompt indique le nom de l'environnement virtuel:

```c
<mon-prompt> $ cd /chemin/vers/le/projet
<mon-prompt> $ source .env-truc/bin/activate
(.env-truc) <mon-prompt> $ type -a python3
python3 is /chemin/vers/le/projet/.env-truc/bin/python3
python3 is /usr/bin/python3
```

Installer les dépendances avec `pip` sans affecter les autres installations Python de la machine. Attention à bien utiliser `python3` et non pas `/bin/usr/python3` :

```c
(.env-truc) <mon-prompt> $ python3 -m pip install requests
Collecting requests
  Downloading https://files.pythonhosted.org/packages/51/bd/23c926cd341ea6b7dd0b2a00aba99ae0f828be89d72b2190f27c11d4b7fb/requests-2.22.0-py2.py3-none-any.whl (57kB)
     |████████████████████████████████| 61kB 5.4MB/s
Collecting urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 (from requests)
  Downloading https://files.pythonhosted.org/packages/e0/da/55f51ea951e1b7c63a579c09dd7db825bb730ec1fe9c0180fc77bfb31448/urllib3-1.25.6-py2.py3-none-any.whl (125kB)
     |████████████████████████████████| 133kB 10.0MB/s
Collecting chardet<3.1.0,>=3.0.2 (from requests)
  Downloading https://files.pythonhosted.org/packages/bc/a9/01ffebfb562e4274b6487b4bb1ddec7ca55ec7510b22e4c51f14098443b8/chardet-3.0.4-py2.py3-none-any.whl (133kB)
     |████████████████████████████████| 143kB 10.5MB/s
Collecting idna<2.9,>=2.5 (from requests)
  Downloading https://files.pythonhosted.org/packages/14/2c/cd551d81dbe15200be1cf41cd03869a46fe7226e7450af7a6545bfc474c9/idna-2.8-py2.py3-none-any.whl (58kB)
     |████████████████████████████████| 61kB 9.4MB/s
Collecting certifi>=2017.4.17 (from requests)
  Using cached https://files.pythonhosted.org/packages/18/b0/8146a4f8dd402f60744fa380bc73ca47303cccf8b9190fd16a827281eac2/certifi-2019.9.11-py2.py3-none-any.whl
Installing collected packages: urllib3, chardet, idna, certifi, requests
Successfully installed certifi-2019.9.11 chardet-3.0.4 idna-2.8 requests-2.22.0 urllib3-1.25.6
```

Sortir de l’environnement virtuel :

```c
(.env-truc) <mon-prompt> $ deactivate
<mon-prompt> $
```

On peut donc créer un environnement virtuel pour chacun des projets, ou même plusieurs environnements virtuels pour un projet : un pour être iso prod, un pour les tests de nouvelles libs…

Cela prend un peu de place, surtout dans `.env-truc/lib64/python3.7/site-packages` (les dépendances) car pour le reste ce sont des liens symboliques.

```
$ du -hsc .env-truc/* | sort -h
0       .env-truc/include
0       .env-truc/lib64
76K     .env-truc/bin
16M     .env-truc/lib
16M     total
```

`venv` est fourni de base avec Python
=====================================

L'outil `venv` est similaire à son ancêtre et s'utilise avec la même approche. Création :

```c
<mon-prompt>$ cd /chemin/mon/projet
<mon-prompt>$ /usr/bin/python3 -m venv .env-truc
```

Activation :

```c
<mon-prompt>$ . .env-truc/bin/activate
(.env-truc) <mon-prompt>$ type -a python3
python3 is /tmp/truc/.env-truc/bin/python3
python3 is /usr/bin/python3
```

Installation des dépendances :

```c
(.env-truc) <mon-prompt>$ python3 -m pip install requests
Collecting requests
  Using cached https://files.pythonhosted.org/packages/51/bd/23c926cd341ea6b7dd0b2a00aba99ae0f828be89d72b2190f27c11d4b7fb/requests-2.22.0-py2.py3-none-any.whl
Collecting chardet<3.1.0,>=3.0.2 (from requests)
  Using cached https://files.pythonhosted.org/packages/bc/a9/01ffebfb562e4274b6487b4bb1ddec7ca55ec7510b22e4c51f14098443b8/chardet-3.0.4-py2.py3-none-any.whl
Collecting certifi>=2017.4.17 (from requests)
  Using cached https://files.pythonhosted.org/packages/18/b0/8146a4f8dd402f60744fa380bc73ca47303cccf8b9190fd16a827281eac2/certifi-2019.9.11-py2.py3-none-any.whl
Collecting idna<2.9,>=2.5 (from requests)
  Using cached https://files.pythonhosted.org/packages/14/2c/cd551d81dbe15200be1cf41cd03869a46fe7226e7450af7a6545bfc474c9/idna-2.8-py2.py3-none-any.whl
Collecting urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 (from requests)
  Using cached https://files.pythonhosted.org/packages/e0/da/55f51ea951e1b7c63a579c09dd7db825bb730ec1fe9c0180fc77bfb31448/urllib3-1.25.6-py2.py3-none-any.whl
Installing collected packages: chardet, certifi, idna, urllib3, requests
Successfully installed certifi-2019.9.11 chardet-3.0.4 idna-2.8 requests-2.22.0 urllib3-1.25.6
You are using pip version 19.0.3, however version 19.2.3 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
```

Désactivation :

```c
(.env-truc) <mon-prompt>$ deactivate
```

Espace occupé :

```c
<mon-prompt>$ du -hsc .env-truc/* | sort -h
0       .env-truc/include
0       .env-truc/lib64
4.0K    .env-truc/pyvenv.cfg
36K     .env-truc/bin
14M     .env-truc/lib
14M     total
```

La documentation officielle de la *Python Software Foundation* est en français : https://docs.python.org/fr/dev/library/venv.html

`virtualenvwrapper` pour étendre `virtualenv`
=============================================

Le projet [`virtualenvwrapper`](https://virtualenvwrapper.readthedocs.io/en/latest/) permet de ne plus se soucier du répertoire où se trouvent les environnements virtuels. Ce projet fonctionne et ajoutant des commandes au dessus de la commande `virtualenv` pour :

* organiser les environnements virtuels où que l’on se trouve dans l’arborescence des répertoires ;
* simplifier la création/copie/suppression des environnements virtuels ;
* passer d’un environnement virtuel à un autre (super utile) ;
* compléter la ligne de commande, avec touche `[Tab]`, selon les environnements virtuels disponibles ;
* étendre davantage ces commandes avec un système d’extensions *(plugins)* ;
* fournir des crochets *(hook)* personnalisables.

Installation:

```c
/usr/bin/python3 -m pip install --user --upgrade virtualenvwrapper
```

Ajouter dans le `~/.bashrc` (ou autre fichier de configuration équivalent) :

```sh
export WORKON_HOME=~/.virtualenvs
mkdir -p $WORKON_HOME
source ~/.local/bin/virtualenvwrapper.sh
```

Les commandes suivantes ont le même effet quel que soit le répertoire où l’on se trouve :

* `mkvirtualenv {nom_env}` pour créer un environnement virtuel (avec `virtualenv`) dans le dossier `$WORKON_HOME` (`~/.virtualenvs`) ;
* `workon {nom_env}` pour activer un environnement virtuel ;
* `rmvirtualenv {nom_env}` pour supprimer l’environnement virtuel.

Les options de `mkvirtualenv` sont les mêmes que pour la commande `virtualenv`.

`pew` dépasse `virtualenvwrapper`
================================

Installation :

```c
/bin/usr/python -m pip install --user --upgrade pew
```

Par rapport au projet `virtualenvwrapper`, le nom des commandes `pew` (tout comme le nom du projet) sont plus courtes et élégantes. Les commandes `pew` sont aussi plus nombreuses :

| Équivalence             | `virtualenvwrapper`   | `pew`
|-------------------------|-----------------------|--------------
| `$WORKON_HOME` <br> par défaut | `~/.virtualenvs` | `~/local/share/virtualenvs`
| Lister les env          | `workon`              | `pew ls`
| Créer un env 	          | `mkvirtualenv <nom>`  | `pew new <nom>`
| Supprimer un env 	  | `rmvirtualenv <nom>`  | `pew rm <nom>`
| Activer un env 	  | `workon <nom>`        | `pew workon <nom>`
| Aller dans le `site-packages` | `cdsitepackages` | `cd $(pew sitepackages_dir)`
| Exécuter sans activer l'env | (aucune) | `pew in <nom> <commande>`
| Exécuter dans tous les env | (aucune) | `pew inall <commande>`
| Dupliquer un env  | (aucune) | `pew cp <nom> <destination>`
| Modifier `PYTHONPATH` | (aucune) | `pew add path`
| Créer un env temporaire  | (aucune) | `pew mktmpenv`
| Choisir le dossier <br> par défaut | (aucune) | `pew setproject path`

&nbsp;
De plus, `pew` ne nécessite pas de modifier le `.bashrc` car `pew` ouvre un nouveau shell. Donc, la sortie de l'environnement virtuel se fait avec `exit` ou la combinaison des touches `[Ctrl]`+`[D]`.

L'inconvénient de `pew` est de nécessiter l'exécution de l'interpréteur Python pour chaque commande lancée, ce qui alourdit son utilisation et peut rajouter une latence par rapport à `virtualenvwrapper`, mais cela reste négligeable pour la plupart des machines modernes. 

`conda` les gère les aussi
==========================

La commande [`conda`](https://en.wikipedia.org/wiki/Conda_(package_manager)) d'_Anaconda_ et de _Miniconda_ permet, en plus de la gestion des paquets, de gérer des environnements virtuels Python. On dispose de trois sous-commandes de base :

* `conda create` pour créer un environnement virtuel,
* `conda activate` pour l'utiliser,
* `conda deactivate` pour cesser de l'utiliser

Exemple :

```
~$ conda create -n testenv1
Collecting package metadata (current_repodata.json): done
Solving environment: done
    
## Package Plan ##
    
  environment location: /home/login/.miniconda3/envs/testenv1
    
Proceed ([y]/n)? y
…
~$ conda activate testenv1
(testenv1) ~$ 
```

Par défaut l'environnement virtuel reprend la version de Python standard du système. Mais il est possible de spécifier une version de Python à utiliser :

```
~$ conda create -n testenv2 python=3.7
Collecting package metadata (current_repodata.json): done
Solving environment: done
    
## Package Plan ##
    
  environment location: /home/login/.miniconda3/envs/testenv2
    
  added / updated specs:
    - python=3.7
    
…(plus de choses à installer)…
    
Proceed ([y]/n)? 
    
…(téléchargement et installation)…
~$ conda activate testenv2
(testenv2) ~$ which python
/home/login/.miniconda3/envs/testenv2/bin/python
(testenv2) ~$ which pip
/home/login/.miniconda3/envs/testenv2/bin/pip
```

On remarque qu'une fois l'environnement virtuel activé, la commande `pip` peut être utilisée directement, de façon saine sans risque de dommages pour votre système.

C'est nul les environnements virtuels !
=======================================

Des [experts Pythons](https://lwn.net/Articles/757354/) trouvent que les environnements virtuels complexifient inutilement l'utilisation de Python et qu'ils dénaturent la philosophie de simplicité. Ces experts réfléchissent avec la PSF pour trouver une solution plus simple en s'inspirant des écosystèmes [Ruby](https://fr.wikipedia.org/wiki/Ruby), ~~Node.js~~ [Deno](https://en.wikipedia.org/wiki/Deno_(software)), [Rust](https://fr.wikipedia.org/wiki/Rust_(langage)) ([`cargo`](https://fr.wikipedia.org/wiki/Cargo_(informatique))), [Go](https://fr.wikipedia.org/wiki/Go_(langage))...

En attendant, pour avoir des espaces de développement indépendants entre ses projets, nous avons des alternatives.

`PYTHONUSERBASE`
----------------

La façon la plus basique est d'invoquer `pip` avec la variable d'environnement `PYTHONUSERBASE`.

Installer les dépendances :

```c
cd /chemin/mon/projet
PYTHONUSERBASE=$PWD/.pip-env
/usr/bin/python3 -m pip install --user --upgrade requests
```

Tester son application :

```c
cd /chemin/mon/projet
PYTHONUSERBASE=$PWD/.pip-env 
PYTHONPATH=$PWD 
/usr/bin/python3 -m mon-projet
```

ou juste un script :

```c
PYTHONUSERBASE=$PWD/.pip-env 
/usr/bin/python3 mon-script.py
```

Les variables d'environnement peuvent aussi être mises dans un fichier shell et activées avec `source /chemin/mon/projet/activate.sh`. Mais bon... on réinvente un peu la roue `venv` !

```c
export PYTHONUSERBASE=/chemin/mon/projet/.pip-env
export PYTHONPATH=/chemin/mon/projet
```

Conteneur
---------

Les habitué·e·s des conteneurs, comme Docker, ont tendance à se créer une image avec uniquement la version Python de leur choix, puis de travailler dans un shell de ce conteneur pour y installer les dépendances nécessaires.

De toutes façons, dans ces organisations, les applications sont livrées dans des conteneurs. Pourquoi ne pas utiliser le même environnement qu'en production ?

Attention quand même à bien configurer son image pour conserver ses changements. 😁

Machine Virtuelle
-----------------

On peut aussi carrément utiliser une machine virtuelle pour isoler un environnement Python. C'est plus lourd qu'un conteneur, mais bon, on faisait comme ça il n'y a pas si longtemps. Sans oublier, que de nombreuses organisations déploient encore leurs applications avec une installation classique. Alors, pourquoi pas utiliser un environnement similaire à celui de la production ?

L'outil [`vagrant`](https://fr.wikipedia.org/wiki/Vagrant) peut aider a *scripter* la création de sa VM. On peut créer plusieurs VMs sur sa machine (en local) et/ou dans les nuages *(cloud)*...

AppVM
-----

L'[Application Machine Virtuelle](https://fr.wikipedia.org/wiki/Qubes_OS#Application_Machines_virtuelles_(AppVM)) (AppVM), concept du système d'exploitation Qubes OS, permet d'isoler chaque application.

Gestionnaire de paquet de nouvelle génération
---------------------------------------------

Le gestionnaire de paquets [Nix](https://fr.wikipedia.org/wiki/Nix) est fourni avec la commande [`nix-shell`](https://nixos.org/nix/manual/#sec-nix-shell) pour activer un shell en spécifiant les dépendances souhaitées.

Le gestionnaire de paquets [GNU Guix](https://fr.wikipedia.org/wiki/GNU_Guix), inspiré de Nix, offre une solution similaire avec la commande [`guix environment`](https://guix.gnu.org/manual/en/html_node/Invoking-guix-environment.html).

Remerciements
=============

Merci à tous les contributeurs de cette dépêche, et notamment à [lolop](https://linuxfr.org/users/lolop), [Ysabeau](https://linuxfr.org/users/ysabeau) et [Sam & Max](http://sametmax.com). lolop sʼest beaucoup investi dans la rédaction et lʼorganisation des dépêches 🤩, Ysabeau a initié les illustrations de cette série de dépêches 🤩 🎨 🖌 et Sam m'autorise à copier les articles du site http://sametmax.com 🤩 📄 📝.

Extrait du courrier de Sam :

> Bonjour Oliver,
>
> Je te donne explicitement lʼautorisation de copier, modifier et publier les articles, partiellement, ou en totalité, et de mettre le résultat sous licence CC0. Cette autorisation sʼétend à l'écriture de posts inspirés d'articles du blog par Sam ou Max, avec ou sans reprise de contenu, et te laisse libre de piocher dans le texte, les codes et contenus graphiques que nous avons produit, mais ne peut concerner les articles invités ou les images piochées sur le net sur lesquels nous n'avons pas les droits. Les articles invités peuvent néanmoins être repris sous CC-BY, bien entendu.
>
> [...]

Licence
=======

Cette dépêche est publiée sous [licence CC0](https://fr.m.wikipedia.org/wiki/Licence_CC0) (sous domaine publique dans les pays où cela est possible) pour permettre de la recopier, modifier, réutiliser et republier sans obligation de citer ses auteurs. Sauf la loi de certains pays, comme la France, qui oblige quand même à citer les auteurs. Au moins, cela montre l'intention des auteurs à autoriser le plagiat.

Tes astuces ?
=============

N'hésite pas à partager tes expériences, tes astuces et tes interrogations.
