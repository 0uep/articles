---
URL:     https://linuxfr.org/news/python-pour-la-rentree-2019-partie-2
Title:   Python 2019/2021 — partie 2 — Python 2
Authors: Oliver, Davy Defaud, Benoît Sibaud et palm123
Date:    2019-09-06T09:39:49+02:00
License: CC0
Tags:    python, python2 et opensuse
Score:   22
---

Python 2019/2021 — partie 2 — Python 2
======================================

Pour cette rentrée 2019, faisons le point sur Python : actualité, bonnes pratiques, astuces, projets intéressants, témoignages…

Cette partie **2** traite de Python **2**. 🐍 🐍 Oui, c’est la [fin](https://www.python.org/dev/peps/pep-0373/#maintenance-releases) de la maintenance de Python 2. Joie pour certain, désolation pour d’autres…

Allez, on se raconte toutes nos anecdotes dans les commentaires.

[![Un barbu présente le logo de Python](2.webp)](https://github.com/linuxfr.org/articles/tree/main/python/2019-2021)

----

* [La 1ʳᵉ partie de cette série de dépêches Python](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1)

----

Licence
=======

Cette dépêche est publiée sous [licence CC0](https://fr.wikipedia.org/wiki/Licence_CC0) (sous domaine publique dans les pays où cela est possible) pour te permettre de recopier, modifier, réutiliser et republier ce contenu sans t’obliger à citer ses auteurs (sauf que la loi de certains pays comme la France t’oblige quand même à citer les auteurs).

Rendre un script exécutable
===========================

Pour lancer un script Python, de nombreuses personnes font :

```
python3 script.py
```

Avec deux petits changements, il est possible de le lancer juste comme ça :

```
./mon-script.py
```

Premier changement, dire que le script est un fichier e**X**écutable :

```
chmod +x mon-script.py
```

Second changement, on rajoute un _[[shebang]]_ sur la **première** ligne du fichier `mon-script.py` :

* pas bien 😯 :
    
    ```sh
    #!/usr/bin/python
    ```
* pas bien 🤔 :
    
    ```sh
    #!/usr/bin/python3
    ```
* très bien 😛 :
    
    ```sh
    #!/usr/bin/env python3
    ```

Les deux premiers caractères du fichier « `#!` » sont appelés le _[[shebang]]_, et même des langages dont le [croisillon](https://fr.wikipedia.org/wiki/Croisillon_(signe)) « `#` » n’est pas utilisé pour les commentaires le prennent en charge, comme [PHP](https://www.php.net/manual/fr/features.commandline.usage.php#example-422).

Le `/usr/bin/env`.

j − 100 avant la fin de Python 2
================================

La durée de maintenance d’une version Python est [généralement de cinq ans](https://devguide.python.org/devcycle/#end-of-life-branches).
Mais Python 2.7 (2010) bénéficie d’une durée de maintenance étendue, jusqu’au [1^(er) janvier 2020](https://pythonclock.org/). C’est la version de Python ayant la plus grande durée de maintenance, ce qui explique aussi le fait que de nombreuses organisations se soient concentrées sur d’autres problématiques plus urgentes, et par [procrastination](https://fr.wikipedia.org/wiki/Procrastination), Python 2 est encore utilisé en 2019 !

Si tu dois maintenir du code compatible Python 2.6 (2008) ou 2.7 (2010), ce chapitre est fait pour toi. Si tu dois maintenir une compatibilité avec Python 2.4 (2004), tu peux regarder comment le projet Ansible s’y ~~prend~~ [prenait](https://www.ansible.com/blog/using-ansible-to-manage-rhel-5-yesterday-today-and-tomorrow). Le code source d’Ansible 2.3, la dernière version compatible Python 2.4, est disponible dans la branche [stable-2.3](https://github.com/ansible/ansible/tree/stable-2.3) (GitHub).

Mort du projet utilisant Python 2
---------------------------------

Si le code compatible Python 2 est prévu pour être remplacé par autre chose dans un avenir proche, le conseil : sois fainéant, fais le strict minimum, et aide plutôt à faire avancer le projet qui doit remplacer le vieux code Python 2.

Tu peux quand même remplacer `python` par `python2` pour explicitement indiquer que c’est seulement compatible Python 2. Par exemple, en haut de tes scripts `*.py` remplace le _[shebang](https://fr.wikipedia.org/wiki/Shebang)_ :

* pas bien 😯 :
    
    ```sh
    #!/usr/bin/python
    ```
* pas bien 🤔 :
    
    ```sh
    #!/usr/bin/env python
    ```
* très bien 😛
    
    ```sh
    #!/usr/bin/env python2
    ```

Les versions des grandes distributions GNU/Linux qui sortent pour cette fin d’année, devraient avoir la commande `python` qui correspond à Python 3. Que ce soit Debian, Arch Linux, Ubuntu, Fedora, openSUSE, etc., toutes auront (enfin) migré leurs scripts vers Python 3. Les rares scripts qui nécessitent encore Python 2 appelleront explicitement `python2` et non pas `python`.

Nouveau code compatible Python 2 et 3
-------------------------------------

Si tu écris du **nouveau** code qui doit être compatible à la fois Python 2 et 3, alors ajoute en haut de ton **nouveau** fichier `*.py` les lignes suivantes :

```python
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function
from __future__ import unicode_literals

from builtins import *

from future import standard_library
standard_library.install_aliases()
```

**⚠ Attention, ne pas le faire sur ta base de vieux code Python 2 ⚠**

Le top est d’avoir ces lignes dans tous tes fichiers `*.py`. En plus de devoir adapter le code source, de nouveaux bogues peuvent apparaître. Par exemple, la ligne `from __future__ import division` change le résultat de `x = 1 / 2` :

```python
$ python2
Python 2.7.16
>>> 1 / 2
0
>>> from __future__ import division
>>> 1 / 2
0.5
```

`Ctrl` + `D`

```python
$ python3
Python 3.7.3
>>> 1 / 2
0.5
```

Si tu testes du code en mode interactif, comme dans l’exemple `python2` ci‐dessus ou avec `ipython`, pense à taper tous ces `import` avant de tester ton code pour être sûr d’avoir le même comportement. Pour ne pas avoir à taper ces lignes à chaque fois, tu peux les mettre dans le script d’initialisation, comme sur cet exemple :

```
$ cat ~/.ipython/profile_default/startup/ipython_config.py

from __future__ import absolute_import
from __future__ import division
from __future__ import print_function
from __future__ import unicode_literals

from builtins import *

from future import standard_library
standard_library.install_aliases()
```

Attention à ne pas s’emmêler les pinceaux en voulant tester du code *Python 2 only* et du code compatible avec les deux versions !

Autre détail : le _[shebang](https://fr.wikipedia.org/wiki/Shebang)_. Comme dit plus haut, la commande `python` devrait correspondre à Python 3 avec la sortie des nouvelles versions Debian, Arch Linux (publication continue), Ubuntu, Fedora, openSUSE.

Si ton script pourrait être exécuté sur une machine ayant seulement Python 2 :

```sh
#!/usr/bin/env python
# Ce script est compatible Python 2 et 3
# Ce script doit pouvoir être exécuté sur une machine ayant seulement Python 2
```

Sinon :

```sh
#!/usr/bin/env python3
# Ce script est compatible Python 2 et 3
# Ce script est toujours exécuté sur une machine ayant Python 3
```

Migration vers Python 3
-----------------------

Il existe déjà beaucoup d’articles sur le sujet, voici quelques liens :

* [article de janvier 2019](https://blog.invivoo.com/la-migration-de-python-2-x-a-python-3-x/) (en français) ;
* migration assistée avec [`2to3`](https://docs.python.org/fr/3.9/library/2to3.html) (en français) ;
* [documentation officielle](https://docs.python.org/3.9/howto/pyporting.html) (en anglais).

Migration vers Go
-----------------

Google utilisait pas mal d’applications Python 2.7 pour gérer la partie serveur de certains de ses sites Web (comme YouTube). Sa décision a été de migrer vers [Go](https://fr.wikipedia.org/wiki/Go_(langage)). Google a publié en 2017, son script de ~~migration~~ [transpilation](https://fr.wiktionary.org/wiki/transpilation) :
<https://github.com/google/grumpy>

Et toi, comment vis tu cette fin de Python 2 ?
==============================================

1. enfin, on aura plus à gérer la rétrocompatibilité ? 🤩
2. sniff, on avait enfin une version stable de Python ? 💚 💚

Tes conseils pour gérer la transition ?

Et n’oublie pas de nous donner un coup de main pour la troisième partie de cette série de dépêches : 
→ <https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3>
