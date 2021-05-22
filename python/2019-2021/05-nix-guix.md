---
URL:     https://linuxfr.org/news/python-partie-5-nix-et-guix
Title:   Python 2019/2021 — partie 5 — Nix (et Guix)
Authors: nokomprendo
         Oliver, Ysabeau, palm123, tisaac et gusterhack
Date:    2019-10-21T13:16:25+02:00
License: CC By-SA
Tags:    python, nix, guix, python3, anaconda, docker et podman
Score:   16
---

Python 2019/2021 — partie 5 — Nix (et Guix)
===========================================

Dans les précédentes dépêches, nous avons discuté de la [popularité de Python](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1), la [fin de la maintenance de Python 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2), les [différentes variantes](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets) de Python, comment les faire [cohabiter avec Py et Pipenv](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-4-py-pyenv)…

Dans la continuité de la précédente dépêche, cette dépêche présente une autre approche pour faire cohabiter différentes versions de Python sur un même ordinateur : [Nix](https://fr.wikipedia.org/wiki/Nix). 🚀 🐍 💫 [![Le logo de Python entouré de petites icônes symbolisant la variété des domaines où s’applique Python, et à droite, un joyeux barbu se tient derrière un écran d’ordinateur qui affiche « partie = 5, "Conda Docker" \n print(partie) »](05.webp)](https://github.com/linuxfr.org/articles/tree/main/python/2019-2021)

----

* [Python ― partie 1 ― Popularité](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1)
* [Python ― partie 2 ― Python 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2)
* [Python ― partie 3 ― Installation de Python et de paquets](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets)
* [Python ― partie 4 ― Py Pyenv](https://linuxfr.org/news/python-pour-noel-2019-partie-4-py-pyenv)
* [Python — partie 7 — Environnements virtuels](https://linuxfr.org/news/python-pour-noel-202x-partie-7-environnements-virtuels)

----

Gestionnaires de paquets évolués (Nix, Guix)
============================================

[Nix](https://fr.wikipedia.org/wiki/Nix) et [Guix](https://fr.wikipedia.org/wiki/GNU_Guix) sont des gestionnaires de paquets généralistes mais très pratiques pour développer en Python. L’idée de base est d’appliquer les principes de la programmation fonctionnelle à la gestion de paquets. Ainsi, un paquet est vu comme une fonction qui prend l’environnement courant et le code source d’un logiciel, et retourne un nouvel environnement où le nouveau logiciel est disponible. Cette approche simpifie la reproduction, la réutilisation et l’isolation des environnements logiciels créés. 

Avec Nix
--------

### Créer un environnement Python simple

Nix permet de créer des environnements temporaires. Par exemple, la commande suivante lance l’interpréteur Python en incluant les modules Numpy et Pandas :

```
$ nix-shell -p 'python3.withPackages(ps: with ps; [ numpy pandas ])' --run python
Python 3.7.5 (default, Oct 14 2019, 23:08:55) 
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

Ici, Python et les modules Numpy et Pandas sont fournis par le dépôt de paquets associé à Nix. Le dépôt standard `nixpkgs` propose une version de Python 3 et une version de Python 2, avec les modules correspondants. Il est également possible d’utiliser son propre dépôt personnalisé ou de personnaliser spécifiquement quelques paquets du dépôt standard (comme expliqué dans la suite de cette dépêche).

Lorsqu’on travaille sur un projet particulier, on préfère généralement ajouter un fichier `shell.nix`, qui décrit l’environnement à créer pour le projet :

```nix
with import <nixpkgs> {};
(python3.withPackages (ps: with ps; [
  numpy
  pandas
])).env
```

Une fois ce fichier créé, il suffit de lancer la commande `nix-shell` pour créer l’environnement correspondant.

```
$ nix-shell --run python
Python 3.7.5 (default, Oct 14 2019, 23:08:55) 
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

Ce simple fichier `shell.nix` est déjà très pratique car il permet de définir de façon précise et homogène l’environnement logiciel d’un projet Python. De plus, les dépendances sont mutualisées : si un autre projet nécessite Numpy, ce sont exactement les mêmes fichiers Numpy qui seront utilisés. Enfin, Nix permet de gérer d’autres types de paquets que Python et de personnaliser finement l’environnement, si besoin.

### Empaqueter un projet Python, avec toutes ses dépendances

Pour construire un projet Python, on écrit généralement un fichier `setup.py`. Nix possède une fonction `buildPythonPackage` pour créer un paquet Nix à partir d’un fichier `setup.py`. L’intérêt d’utiliser Nix en plus du fichier Python est que l’on peut définir précisément toutes les dépendances (Python ou non) et intégrer notre projet au système Nix (et donc de pouvoir le réutiliser directement dans un autre projet).

Par exemple, imaginons que nous avons un projet Python "myapp" qui utilise le paquet Python Numpy, le paquet système zlib et une bibliothèque interne C++ "mylibcpp" (elle-même empaquetée via Nix). Alors, on peut empaqueter notre projet avec le fichier `default.nix` suivant :

```nix
{ pkgs ? import <nixpkgs> {} }:

let
  mylibcpp = pkgs.callPackage ./mylibcpp/default.nix {};
in
pkgs.python3Packages.buildPythonPackage {
  name = "myapp";
  src = ./.;
  propagatedBuildInputs = [
    pkgs.python3Packages.numpy  # paquet python
    pkgs.zlib                   # paquet non python
    mylibcpp                    # paquet perso
  ];
}
```

Ce fichier `default.nix` nous permet de :

- lancer un `nix-shell` et avoir toutes les dépendances nécessaires pour travailler sur notre projet Python;
- lancer un `nix-build` pour construire et exécuter une version finale de notre projet;
- lancer un `nix-env -i -f .` pour installer notre projet sur le système, comme n’importe quel autre paquet de la logithèque de Nix;
- réutiliser notre projet dans un autre projet utilisant Nix;
- et même, de soumettre notre projet pour une intégration dans la logithèque de Nix.

### Modifier l’environnement Python standard

Nix permet de configurer complètement l’environnement logiciel, notamment d’ajouter des paquets Python supplémentaires. Par exemple, si on veut récupérer le paquet Cma sur Pypi et l’intégrer à l’environnement, on peut écrire le fichier `shell.nix` suivant :

```nix
with import <nixpkgs> {};

( let
  cma = python3Packages.buildPythonPackage rec {
    pname = "cma";
    version = "2.7.0";
    src = python3Packages.fetchPypi {
      inherit pname version;
      sha256 = "0nfdq7qznfqcnqwbk04812xiddq8azzbvdj2pa2lvgzxbr00sqzl";
    };
    propagatedBuildInputs = [
      python3Packages.numpy
    ];
    doCheck = false;
  };
  in python3.withPackages (ps: [ cma ])
).env
```

Il est également possible de redéfinir l’environnement courant. Par exemple, le fichier `shell.nix` suivant fixe Numpy à la version 1.16.4 et utilise cette version dans le nouvel environnement, notamment pour le paquet Cma, également ajouté.

```nix
with import <nixpkgs> {};

(let
  python = let
    packageOverrides = self: super: {

      numpy = self.buildPythonPackage rec {
        pname = "numpy";
        version = "1.16.4";
        src = fetchTarball {
          url = "https://github.com/numpy/numpy/releases/download/v${version}/numpy-${version}.tar.gz";
          sha256 = "1wparj9r5cnh9290s2ikp28yvhx95mainnnlxjgw5p6mppk5zkix";
        };
        doCheck = false;
      };

      cma = self.buildPythonPackage rec {
        pname = "cma";
        version = "2.7.0";
        src = self.fetchPypi {
          inherit pname version;
          sha256 = "0nfdq7qznfqcnqwbk04812xiddq8azzbvdj2pa2lvgzxbr00sqzl";
        };
        propagatedBuildInputs = [
          self.numpy
        ];
        doCheck = false;
      };

    };
  in pkgs.python3.override {
        inherit packageOverrides;
        self = python;
      };

in python.withPackages(ps: [ ps.cma ])).env
```

Avec Guix
---------

Le gestionnaire de paquets [GNU Guix](https://fr.wikipedia.org/wiki/GNU_Guix), inspiré de Nix, offre une solution similaire avec la commande [`guix environment`](https://guix.gnu.org/manual/en/html_node/Invoking-guix-environment.html).

Remerciements
=============

Merci à tou⋅te⋅s les contribut⋅rices⋅eurs de cette dépêche, et notamment à [Oliver](https://linuxfr.org/users/oliver) pour l’avoir initiée. 👏 Continuons à participer aux prochaines dépêches. 👍

Licence
=======

Cette dépêche est publiée sous [licence CC0](https://fr.m.wikipedia.org/wiki/Licence_CC0) (dans le domaine public dans les pays où c’est possible) pour permettre de la recopier, modifier, réutiliser et republier sans obligation de citer ses auteurs quelle que soit la loi de certains pays comme la France, qui oblige quand même à citer les auteurs. Au moins, cela montre l’intention des auteurs à autoriser le plagiat.

Tes astuces ?
=============

N’hésite pas à partager tes expériences, tes astuces et tes interrogations.

Donne-nous un coup de main pour la rédaction des dépêches à venir.
