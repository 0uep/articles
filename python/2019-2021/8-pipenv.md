---
URL:     https://linuxfr.org/news/python-partie-8-pipenv
Title:   Python 2019/2021 — partie 8 — Pipenv
Authors: Philippe F, Oliver, Ysabeau, Benoît Sibaud, tisaac et gusterhack
Date:    2019-09-27T16:16:15+02:00
License: CC0
Tags:    python et pipenv
Score:   18
---

Python 2019/2021 — partie 8 — Pipenv
====================================

Cette dépêche est la suite d’une série sur Python initiée en septembre 2019. Après un sommeil cryogénique de un an et demi, on repart en forme avec d’autre contenu Python à vous proposer: actualité, bonnes pratiques, astuces, témoignages…

Cette huitième partie présente `pipenv`, un outil pour s’abstraire de `pip` et `virtualenv` qui est mis en valeur par la PyPA *(Python Packaging Autority)*. Puis nous finirons la dépêche par un cas pratique avec conteneurisation via Docker, le tout avec plein d’astuces et de conseils pour bien s’en sortir. 🚀 🐍

Pour rappel, les dépêches précédentes :

* [Python - partie 1](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1) parlait de la popularité explosive du langage Python ;
* [Python - partie 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2) évoquait la fin du support de Python 2 ;
* [Python - partie 3](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets) parlait des différentes façons d’installer Python et des gestionnaires de paquets Python ;
* [Python - partie 4](https://linuxfr.org/news/python-pour-noel-2019-partie-4-py-pyenv) vous présentaient `py` et `pyenv` pour faciliter la gestion de plusieurs versions de Python en parallèle sur un poste ;
* [Python — partie 5](https://linuxfr.org/news/python-partie-5-nix-et-guix) qui dissertait de Nix (et Guix) ;
* [Python — partie 7](https://linuxfr.org/news/python-pour-noel-202x-partie-7-environnements-virtuels) évoquait les environnements virtuels Python et ses alternatives comme la conteneurisation, le tout avec plein d’astuces et de conseils pour bien s’en sortir.

[![Le logo de Python est entouré de petites icônes symbolisant la variété des domaines où s’applique Python, et, à droite, un joyeux barbu se tient derrière un écran d’ordinateur qui affiche « partie = 8, "Pipenv" \n print (partie) »](8.webp)](https://github.com/linuxfr.org/articles/tree/main/python/2019-2021)

----

* [Python — partie 1 ― Popularité](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1)
* [Python — partie 2 ― Python 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2)
* [Python — partie 3 — Installation de Python et de paquets](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets)
* [Python — partie 4 — Py Pyenv – LinuxFr.org](https://linuxfr.org/news/python-pour-noel-2019-partie-4-py-pyenv)
* [Python — partie 7 — Environnements virtuels](https://linuxfr.org/news/python-pour-noel-202x-partie-7-environnements-virtuels)

----

`pipenv` encapsule `pip` et  `virtualenv`
==================

L’outil `pipenv` est présenté par l’équipe PyPA (Python Packaging Authority) dans son tutoriel en anglais :
https://packaging.python.org/tutorials/managing-dependencies/

À l’origine, il y a un constat simple : l’ensemble des paquets Python installés sur votre système par votre distribution a bien été testé par cette dernière. Il est délicat d’en rajouter des nouveaux avec `pip` au niveau système ou même utilisateur car vous risquez de casser cet écosystème bien testé. Si vous avez besoin d’ajouter des paquets, c’est sûrement pour un projet particulier. Donc cela a plus de sens de ne les ajouter que dans ce projet, via un environnement virtuel. Surtout que si vous avez plusieurs projets, ceux-ci n’ont peut-être pas exactement les mêmes besoins.

La conclusion immédiate, c’est que `pip` et `venv` s’utilisent conjointement. Cela a un sens de les rassembler. Une autre motivation de Kenneth Reitz pour se lancer dans l’aventure `pipenv` était son souhait de capturer les dépendances générales d’un projet dans un fichier, et de capturer toutes les dépendances précises en parallèle. Il explique cela mieux dans [une présentation sur `pipenv`](https://speakerdeck.com/kennethreitz/the-future-of-python-dependency-management?slide=24) que je vous recommande .

Historique
----------

* 2014, la communauté discute sur le futur format [`requirements.txt` 2.0](https://github.com/pypa/pip/issues/1795) ;
* 2015, nouvelle fonctionnalité demandée pour `pip` : [gérer les environnements virtuels](https://github.com/pypa/pip/issues/2488) ;
* 2016, ébauche de `pip2` basé sur le format `Pipfile`, la **v&nbsp; 2.0** du format `requirements.txt` ;
* 2017, le projet `pip2` est renommé `pipenv` et le [dépôt de code source](https://github.com/pypa/pipenv) est créé ;
* 2019, Goldy nous [recommande `pipenv`](https://linuxfr.org/users/oliver_h/journaux/quelques-bonnes-pratiques-python-pour-2019#comment-1766395).

Installation
------------

L’installation de `pipenv` peut se faire avec le gestionnaire de paquets de la distribution :

```cpp
$ sudo apt search pipenv
Sorting... Done
Full Text Search... Done
pipenv/disco,disco 11.9.0-1 all
  Python's officially recommended packaging tool

$ sudo apt install pipenv
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  python3-virtualenv python3-virtualenv-clone
The following NEW packages will be installed:
  pipenv python3-virtualenv python3-virtualenv-clone
[...]
```

L’installation peut aussi se faire avec `pip` ce qui permet d’avoir une version plus à jour :

```cpp
$ python3 -m pip install pipenv --user --upgrade --progress-bar emoji
[...]
Successfully installed pipenv-2018.11.26
```

Dans, mon cas, j’ai installé `pipenv` avec les deux possibilités, j’ai donc deux exécutables `pipenv`. Vérifions les versions installées :

```cpp
$ type -a pipenv
pipenv is /home/oliver/.local/bin/pipenv
pipenv is /usr/bin/pipenv

$ /home/oliver/.local/bin/pipenv --version
pipenv, version 2018.11.26

$ /usr/bin/pipenv --version
pipenv, version 11.9.0

```

En fait, la version [`11.9.0`](https://github.com/pypa/pipenv/releases/tag/v11.9.0) date du 21 mars 2018, puis, [deux mois après](https://github.com/pypa/pipenv/releases/tag/v2018.05.18), la numérotation des versions est modifiée. La version la plus récente est bien celle installée avec `pip`.

Rappels :

1. Installer `pipenv` avec `pip` pourrait casser le fonctionnement d’une autre application. Par exemple, la mise à jour de la dépendance `virtualenv` peut rentrer en conflit avec la version nécessaire à cette autre application. L’installation recommandée est celle avec le gestionnaire de la distribution. Utiliser `pip` si cela est vraiment nécessaire et que les risques sont maîtrisés.
2. Ou alors, vous avez lu la dépêche qui parle de `pip` et `pipx` et vous installez `pipenv` avec `pipx`. Là, vous êtes sûr d’éviter plein de problèmes.

Exemple d’utilisation
---------------------

Se positionner à la base de son projet et installer les dépendances `flask` et `autopep8` avec `pipenv` :

```cpp
cd /chemin/vers/mon/projet/chouette
```

```python
$ pipenv install flask
Creating a virtualenv for this project…
Pipfile: /chemin/vers/mon/projet/chouette/Pipfile
Using /usr/bin/python3 (3.7.3) to create virtualenv…
⠸ Creating virtual environment...Already using interpreter /usr/bin/python3
Using base prefix '/usr'
New python executable in /home/tux/.local/share/virtualenvs/chouette-4m-Hw0ap/bin/python3
Also creating executable in /home/tux/.local/share/virtualenvs/chouette-4m-Hw0ap/bin/python
Installing setuptools, pip, wheel...
done.

✔ Successfully created virtual environment! 
Virtualenv location: /home/tux/.local/share/virtualenvs/chouette-4m-Hw0ap
Creating a Pipfile for this project…
Installing flask…
Adding flask to Pipfile's [packages]…
✔ Installation Succeeded 
Pipfile.lock not found, creating…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
✔ Success! 
Updated Pipfile.lock (662286)!
Installing dependencies from Pipfile.lock (662286)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 6/6 — 00:00:01
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

```rust
$ pipenv install --dev autopep8
Installing autopep8…
Adding autopep8 to Pipfile's [dev-packages]…
✔ Installation Succeeded 
Pipfile.lock (b0a650) out of date, updating to (662286)…
Locking [dev-packages] dependencies…
✔ Success! 
Locking [packages] dependencies…
✔ Success! 
Updated Pipfile.lock (b0a650)!
Installing dependencies from Pipfile.lock (b0a650)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 8/8 — 00:00:01
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

Nous avons deux nouveaux fichiers :

* `Pipfile`, au format [TOML](https://fr.wikipedia.org/wiki/TOML), spécifie les règles générales ;
* `Pipfile.lock`, au format [JSON](https://fr.wikipedia.org/wiki/JavaScript_Object_Notation), verrouille *(lock)* les versions de chacune des dépendances.

```ada
$ ls -gG
total 12K
-rw-r--r-- 1 4,5K août  31 15:42 Pipfile.lock
-rw-r--r-- 1  150 août  31 15:42 Pipfile
```

Le fichier `Pipfile` sépare les dépendances en deux sections et peut remplacer les fichiers `requirements.txt` et `requirements-dev.txt` que nous rencontrons souvent à la base des projets Python. C'est aussi une alternative aux sections `install_requires` et `extras_require` du fichier `setup.py`.

```yaml
$ head -n 33 Pipfile*
==> Pipfile <==
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]
autopep8 = "*"

[packages]
flask = "*"

[requires]
python_version = "3.7"

==> Pipfile.lock <==
{
    "_meta": {
        "hash": {
            "sha256": "be66bf67d2a9a5d1606be53501e0b029c8c465fc0660151ea0b5c780f7b0a650"
        },
        "pipfile-spec": 6,
        "requires": {
            "python_version": "3.7"
        },
        "sources": [
            {
                "name": "pypi",
                "url": "https://pypi.org/simple",
                "verify_ssl": true
            }
        ]
    },
    "default": {
        "click": {
            "hashes": [
                "sha256:2335065e6395b9e67ca716de5f7526736bfa6ceead690adf616d925bdc622b13",
                "sha256:5b94b49521f6456670fdb30cd82a4eca9412788a93fa6dd6df72c94d5a8ff2d7"
            ],
            "version": "==7.0"
        },
        "flask": {
            "hashes": [
                "sha256:13f9f196f330c7c2c5d7a5cf91af894110ca0215ac051b5844701f2bfd934d52",
                "sha256:45eb5a6fd193d6cf7e0cf5d8a5b31f83d5faae0293695626f539a823e93b13f6"
            ],
            "index": "pypi",
            "version": "==1.1.1"
        },
```

Le fichier `Pipfile.lock` n’a pas besoin d’être versionné, car `pipenv` le génère automatiquement à partir du fichier `Pipfile`. Néanmoins, je recommande de le versionner afin de suivre l’évolution des versions des dépendances et de pouvoir reproduire un même fonctionnement tout au long du cycle : développement, intégration, production…

La commande 'pipenv lock' est l’équivalent de 'pip freeze'. Voir aussi le projet [lock-requirements](https://pypi.org/project/lock-requirements/). 

Visitons notre environnement virtualisé avec la commande `pipenv shell` :

```c
$ pipenv shell
Launching subshell in virtual environment…
 . /home/tux/.local/share/virtualenvs/chouette-4m-Hw0ap/bin/activate
```

```cpp
$ pip list
Package      Version
------------ -------
autopep8     1.4.4  
Click        7.0    
Flask        1.1.1  
itsdangerous 1.1.0  
Jinja2       2.10.1 
MarkupSafe   1.1.1  
pip          19.2.3 
pycodestyle  2.5.0  
setuptools   41.2.0 
Werkzeug     0.15.5 
wheel        0.33.6 
```

Utiliser <kbd>`[Ctrl]`</kbd> + <kbd>`[D]`</kbd> ou `exit` pour sortir du `pipenv shell`.

La commande `pipenv run` est aussi bien pratique :

```c
$ pipenv run pip list
Package      Version
------------ -------
autopep8     1.4.4  
Click        7.0    
Flask        1.1.1  
itsdangerous 1.1.0  
Jinja2       2.10.1 
MarkupSafe   1.1.1  
pip          19.2.3 
pycodestyle  2.5.0  
setuptools   41.2.0 
Werkzeug     0.15.5 
wheel        0.33.6 
```

Mais pour visualiser ses dépendances, `pipenv graph` est mieux que `pip list` :

```c
$ pipenv graph
autopep8==1.4.4
  - pycodestyle [required: >=2.4.0, installed: 2.5.0]
Flask==1.1.1
  - click [required: >=5.1, installed: 7.0]
  - itsdangerous [required: >=0.24, installed: 1.1.0]
  - Jinja2 [required: >=2.10.1, installed: 2.10.1]
    - MarkupSafe [required: >=0.23, installed: 1.1.1]
  - Werkzeug [required: >=0.15, installed: 0.15.5]
```

Supprimer son environnement virtualisé avec `pipenv --rm` :

```c
$ pipenv --rm
Removing virtualenv (/home/tux/.local/share/virtualenvs/chouette-4m-Hw0ap)…
```

Vérifions notre environnement virtualisé :

```c
$ pipenv run pip list
Creating a virtualenv for this project…
Pipfile: /home/tux/chouette/Pipfile
Using /usr/bin/python3.7m (3.7.3) to create virtualenv…
⠼ Creating virtual environment...Already using interpreter /usr/bin/python3.7m
Using base prefix '/usr'
New python executable in /home/tux/.local/share/virtualenvs/chouette-4m-Hw0ap/bin/python3.7m
Also creating executable in /home/tux/.local/share/virtualenvs/chouette-4m-Hw0ap/bin/python
Installing setuptools, pip, wheel...
done.
Running virtualenv with interpreter /usr/bin/python3.7m

✔ Successfully created virtual environment! 
Virtualenv location: /home/tux/.local/share/virtualenvs/chouette-4m-Hw0ap
Package    Version
---------- -------
pip        19.2.3 
setuptools 41.2.0 
wheel      0.33.6 
```

Installons les modules nécessaires en prod avec `pipenv install` ou `pipenv sync` :

```c
$ pipenv install
Installing dependencies from Pipfile.lock (b0a650)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 6/6 — 00:00:01
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

```c
$ pipenv run pip list
Package      Version
------------ -------
Click        7.0    
Flask        1.1.1  
itsdangerous 1.1.0  
Jinja2       2.10.1 
MarkupSafe   1.1.1  
pip          19.2.3 
setuptools   41.2.0 
Werkzeug     0.15.5 
wheel        0.33.6 
```

Enfin, installons les modules nécessaires au développement avec l’option `--dev` :

```c
$ pipenv install --dev
Installing dependencies from Pipfile.lock (b0a650)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 8/8 — 00:00:02
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

```c
$ pipenv run pip list
Package      Version
------------ -------
autopep8     1.4.4  
Click        7.0    
Flask        1.1.1  
itsdangerous 1.1.0  
Jinja2       2.10.1 
MarkupSafe   1.1.1  
pip          19.2.3 
pycodestyle  2.5.0  
setuptools   41.2.0 
Werkzeug     0.15.5 
wheel        0.33.6 
```

L’installation de [`black`](https://github.com/psf/black) (formateur de code Python) nécessite d’autoriser les versions bêta car celui-ci n’est livré que en _prerelease_ (cf [sa page sur pypi.org](https://pypi.org/project/black/#history)):

```
$ pipenv install --dev --pre black
Installing black…
Adding black to Pipfile's [dev-packages]…
✔ Installation Succeeded 
Pipfile.lock (d00da7) out of date, updating to (b0a650)…
Locking [dev-packages] dependencies…
✔ Success! 
Locking [packages] dependencies…
✔ Success! 
Updated Pipfile.lock (d00da7)!
Installing dependencies from Pipfile.lock (d00da7)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 12/12 — 00:00:02
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

Sans l’option `--dev` nous obtenons l’erreur peu explicite `"ERROR : Could not find a version that matches black"` au milieu d’un tas de logs peu intuitifs. Maintenenant, notre fichier `Pipfile` contient une section `allow_prereleases = true` :

```ini
$ cat Pipfile
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]
autopep8 = "*"
black = "*"

[packages]
flask = "*"

[requires]
python_version = "3.7"

[pipenv]
allow_prereleases = true
```

C’est une mauvaise idée d’installer `black` avec `pipenv` car cela nous force à activer `allow_prereleases = true` qui s’applique aussi aux versions utilisées pour l’exécution de l’application. Je recommande plutôt d’installer `black` avec `pip install --user`.

Nous avons `black`, alors désinstallons `autopep8` :

```
$ pipenv uninstall autopep8
Uninstalling autopep8…
Uninstalling autopep8-1.4.4:
  Successfully uninstalled autopep8-1.4.4

Removing autopep8 from Pipfile…
Locking [dev-packages] dependencies…
✔ Success! 
Locking [packages] dependencies…
✔ Success! 
Updated Pipfile.lock (a5c3f0)!
```

Faisons le ménage, désinstallons les dépendances qui ne sont plus nécessaires :

```c
$ pipenv clean
Uninstalling pycodestyle…
```

Pipenv est vraiment un outil facile à utiliser et très pratique. Personnellement, j’édite directement le fichier `Pipfile` qui reste simple, et du coup, je n’utilise plus les commandes `pipenv install` et `pipenv uninstall`. En fait, la commande `pipenv install` est pratique pour ajouter d’une dépendance avec des paramètres compliqués. Dans ce cas, j’applique la ligne de commande de `pip install` à `pipenv install`.

Exemple, la documentation dit :

```lisp
pip install git+ssh://git@gitlab.monserveur/chemin/cool.git#egg=cool
```

Donc nous remplaçons `pip` par `pipenv` :

```lisp
python3 -m pipenv install git+ssh://git@gitlab.monserveur/chemin/cool.git#egg=cool
```

Et nous obtenons une nouvelle ligne dans notre fichier `Pipfile` :

```ini
[packages]
cool = {git = "ssh://git@gitlab.monserveur/chemin/cool.git"}
```

Un autre exemple, avec la documentation qui dit :

```css
pip install prospector[with_everything]
```

Nous remplaçons `pip` par `pipenv` et n’oublions pas l’option `--dev` :

```css
python3 -m pipenv install --dev prospector[with_everything]
```

Cela rajoute dans notre fichier `Pipfile` :

```ini
[dev-packages]
prospector = {extras = ["with_everything"],version = "*"}
```

Index PyPi privé
----------------

Souvent, les entreprises ont un index PyPi privé pour permettre de livrer ses propres packages Python en interne. Pour gérer proprement ce cas de figure, voici mes recommandations. Dans le fichier `Pipfile`, déclarer les deux sources :   

```ini
[[source]]
source = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[[source]]
source = "private"
url = "https://pypi.monserveur.com/simple"
verify_ssl = true
```

Si l’index PyPi privé est protégé par un {nom}/{mdp}, chaque utilisateur crée un fichier `~/.netrc` avec le minimum de permissions `chmod 0600 ~/.netrc` et contenant :

```ini
machine pypi.monserveur.com
    login    {nom}
    password {mdp}
```

Pipenv va chercher automatiquement les paquets dans les deux index PyPi. Pour éviter tout conflit, il est possible d’indiquer l’index PyPi concerné :

```css
pipenv install cool --index https://pypi.monserveur.com/simple
```

Ce qui rajoute dans le fichier `Pipfile` :

```ini
[packages]
cool = {index = "https://pypi.monserveur.com/simple",version = "*"}
```

😘✨ Merci aux contributrices et contributeurs de `pipenv` (dont environ [300 personnes listées sur GitHub](https://github.com/pypa/pipenv/graphs/contributors)).

Dockeriser Python
=================

Docker avec `pip`
-----------------

Prenons un projet Python très simple ayant `dateutil` comme seule dépendance pour l’exécution *(runtime)* :

```
├── mon_app/
│   ├── mon_script.py
│   └── ...
│
├── Dockerfile
│   ║
│   ╚═╡ FROM python:3.7-slim
│     │ COPY requirements.txt /tmp
│     │ RUN pip3 install -r /tmp/requirements.txt
│     │ COPY mon_app /
│     │ CMD ["python3", "/mon_app/mon_script.py"]
│
├── requirements.txt
│   ║
│   ╚═╡ dateutil
│
└── requirements-dev.txt
    ║
    ╚═╡ black
```

La première ligne de notre `Dockerfile` est `FROM python:3.7-slim` ce qui est un raccourci vers `FROM python:3.7.4-slim-buster` qui référence un [autre Dockerfile sur GitHub](https://github.com/docker-library/python/blob/master/3.7/buster/slim/Dockerfile). L'image `python:3.7-slim` correspond à la plus petite image nécessaire pour faire tourner la dernière version Python 3.7 fournie par [Debian stable](https://wiki.debian.org/fr/DebianStable) (Buster).

L’ordre des commandes du Dockerfile est important. On commence par ce qui a le moins de probabilité de changer afin de permettre à `docker` d’utiliser son cache et éviter de perdre du temps à exécuter à nouveau toutes les commandes. Ici, dans notre exemple, changer le contenu de `mon_script.py` va permettre à `docker` de réutiliser son cache pour les trois premières lignes du fichier `Dockerfile`. Si la ligne `COPY mon_app /mon_app` avait été la toute première, `docker` aurait alors du ré-exécuter toutes les commandes du `Dockerfile` pour chaque changement du fichier `mon_script.py`. Ceci est la raison pour laquelle gérer ses dépendances Python dans le fichier `setup.py` (`install_requires`) n’est pas une bonne idée comme [expliqué](https://pythonspeed.com/articles/pipenv-docker/) par Itamar Turner-Trauring (en anglais).

Séparer les dépendances pour la production (`requirements.txt`) est pour le développement (`requirements-dev.txt`) est une bonne pratique afin d’augmenter la sécurité de notre script (moins de surface d’attaque) et de réduire la taille de notre image Docker.

Le souci de notre fichier `requirements.txt` est l’absence des versions des dépendances. Nous risquons d’avoir une régression due à une nouvelle version d’une dépendance sans s’en apercevoir. Une solution avec `pip` est d’utiliser `pip-compile` pour générer un fichier `requirements-lock.txt` et de versionner celui-ci avec le code source:

```sh
pip-compile requirements.txt > requirements-lock.txt
```

Docker avec `pipenv`
--------------------

Migrons notre projet simpliste vers `pipenv` :

```
├── mon_app/
│   ├── mon_script.py
│   └── ...
│
├── Dockerfile
│   ║
│   ╚═╡ FROM python:3.7-slim
│     │ RUN pip3 install pipenv
│     │ COPY Pipfile* /tmp
│     │ RUN cd /tmp && pipenv lock --requirements > requirements.txt
│     │ RUN pip3 install -r /tmp/requirements.txt
│     │ RUN pip3 uninstall pipenv
│     │ COPY mon_app /
│     │ CMD ["python3", "/mon_app/mon_script.py"]
│
├── Pipfile
│   ║
│   ╚═╡ [[source]]
│     │ url = "https://pypi.python.org/simple"
│     │ verify_ssl = true
│     │ 
│     │ [packages]
│     │ dateutil = "*"
│     │
│     │ [dev-packages]
│     │ black = "*"
│     │ 
│     │ [requires]
│     │ python_version = "3.7"
│
└── Pipfile.lock
```

La commande `pip` ne sait pas installer des modules Python à partir d’un fichier `Pipfile`, et nous devons installer `pipenv`. Une demande pour avoir `pip install --pipfile Pipfile` est en cours de [discussion sur GitHub](https://github.com/pypa/pip/issues/6925).

Une alternative est de lancer l’application conteneurisée dans l’environnement virtualisé avec ce Dockerfile :

```dockerfile
FROM python:3.7-slim
RUN pip3 install pipenv
MKDIR         /mon_projet
COPY Pipfile* /mon_projet
WORKDIR       /mon_projet
RUN pipenv sync
COPY mon_app /mon_projet
CMD ["pipenv", "run", "./mon_app/mon_script.py"]
```

Remerciements
=============

Merci à tous les contributeurs de cette dépêche, et notamment à [Sam & Max](http://sametmax.com), [lolop](https://linuxfr.org/users/lolop) et [Ysabeau](https://linuxfr.org/users/ysabeau). Sam m’autorise à copier les articles du site http://sametmax.com 🤩 📄📝 lolop s’est beaucoup investit dans l’organisation de la dépêche précédente et cette dépêche 🤩 🎛🎚 et Ysabeau a initié les illustrations de cette série de dépêches 🤩 🎨🖌.  

Extrait du courrier de Sam :

> Bonjour Oliver,
>
> Je te donne explicitement l’autorisation de copier, modifier et publier les articles, partiellement, ou en totalité, et de mettre le résultat sous licence CC0. Cette autorisation s’étend à l’écriture de posts inspirés d’articles du blog par Sam ou Max, avec ou sans reprise de contenu, et te laisse libre de piocher dans le texte, les codes et contenus graphiques que nous avons produit, mais ne peut concerner les articles invités ou les images piochées sur le net sur lesquels nous n’avons pas les droits. Les articles invités peuvent néanmoins être repris sous CC-BY, bien entendu.
>
> [...]

Licence
=======

Cette dépêche est publiée sous [licence CC0](https://fr.m.wikipedia.org/wiki/Licence_CC0) (sous domaine publique dans les pays où cela est possible) pour permettre de la recopier, modifier, réutiliser et republier sans obligation de citer ses auteurs. Sauf la loi de certains pays, comme la France, qui oblige quand même à citer les auteurs. Au moins, cela montre l’intention des auteurs à autoriser le plagiat.

Tes astuces ?
=============

N’hésite pas à partager tes expériences, tes astuces et tes interrogations.
