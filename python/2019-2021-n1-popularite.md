---
URL:     https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1
Title:   Python 2019/2021 — partie 1 — Popularité
Authors: Oliver, M5oul, theojouedubanjo, Benoît Sibaud, Davy Defaud, Nÿco, Ysabeau et palm123
Date:    2019-09-01T16:16:30+02:00
License: CC0
Tags:    python, 2019, python3, mongodb et objective-c
Score:   43
---

Python 2019/2021 — partie 1 — Popularité
========================================

Pour cette rentrée 2019, faisons le point sur Python : actualité, bonnes pratiques Python, astuces, projets intéressants, témoignages…

Cette première partie présente la popularité de Python, chiffres à l’appui. Mais qu’est ce qui explique qu’un vieux langage de vingt‐cinq ans, lent et dont l’indentation influence la compilation, puisse être aussi populaire ?

[![Un barbu présente le logo de Python](2019-2021-n1.webp)](https://www.newgenapps.com/blog/python-in-2019)

----

[Appel à conférence pour la PyConFR, du 31 octobre au 3 novembre 2019 à Bordeaux](https://linuxfr.org/news/pyconfr-2019-du-31-octobre-au-3-novembre-a-bordeaux-appel-a-conferences)

----

Licence
=======

Cette dépêche est publiée sous [licence CC0](https://fr.wikipedia.org/wiki/Licence_CC0) (sous domaine public dans les pays où cela est possible) pour te permettre de recopier, modifier, réutiliser et republier ce contenu sans t’obliger à citer ses auteurs (sauf que la loi de certains pays comme la France t’oblige quand même à citer les auteurs).

Actualité
=========

Bientôt la PyConFR, du 31 octobre au 3 novembre à Bordeaux, lire la [dépêche](https://linuxfr.org/news/pyconfr-2019-du-31-octobre-au-3-novembre-a-bordeaux-appel-a-conferences).

Popularité du langage Python
============================

StackOverflow
-------------

En 2017, David Robinson, un _data scientist_ travaillant pour StackOverflow, a publié un article intitulé *The Incredible Growth of Python* dans lequel, en se basant sur le trafic Web de StackOverflow, il réalise une projection du trafic dans les prochaines années. Pour sa projection, David prend en compte les pays à forts revenus, car ce sont souvent les premiers à adopter les nouvelles technologies.

[![Projection du trafic sur StackOverflow concernant les principaux langages de programmation](https://1015711.v1.pressablecdn.com/wp-content/uploads/2017/09/projections-1-1024x878.png)](https://stackoverflow.blog/2017/09/06/incredible-growth-python/ "Le trafic Web concernant Python devraient représenter plus de 13 % en 2020, devant JavaScript et Java qui devraient être dans les 10 %.")

L’année suivante (2018), le trafic Web relatif aux questions Python représente une part de plus en plus importante.

![Trafic StackOverflow concernant les principaux langages de programmation entre 2012 et 2018](http://olibre.github.io/GreatTips/python/news/traffic-web-stack-overflow-2018.png)

Chaque année, StackOverflow réalise un sondage publié sous le nom *Developer Survey Results*.

Je n’ai pas pris en compte HTML et CSS car ils ne figurent pas dans les anciens sondages.

### Le langage le plus utilisé ?

&emsp; &emsp;   2013       | 2014       | [2015][5]  | [2016][6]  | [2017][7]  | [2018][8]  | [2019][9]
---------------------------|------------|------------|------------|------------|------------|------------
&nbsp;1. &emsp; SQL        | JavaScript | JavaScript | JavaScript | JavaScript | JavaScript | JavaScript
&nbsp;2. &emsp; JavaScript | SQL        | SQL        | SQL        | SQL        | SQL        | SQL
&nbsp;3. &emsp; C#         | Java       | Java       | Java       | Java       | Java       | **Python**
&nbsp;4. &emsp; Java       | C#         | C#         | C#         | C#         | Shell      | Java
&nbsp;5. &emsp; PHP        | PHP        | PHP        | PHP        | **Python** | **Python** | Shell
&nbsp;6. &emsp; C++        | **Python** | **Python** | **Python** | PHP        | C#         | C#
&nbsp;7. &emsp; C          | C++        | C++        | C++        | C++        | PHP        | PHP
&nbsp;8. &emsp; **Python** | C          | C          | AngularJS  | C          | C++        | C++
&nbsp;9. &emsp; ObjectiveC | ObjectiveC | Node.js    | Node.js    | TypeScript | C          | TypeScript
10.      &emsp; Ruby       | Ruby       | AngularJS  | C          | Ruby       | TypeScript | C
11.      &emsp; Node.js    | Node.js    | Ruby       | Ruby       | Swift      | Ruby       | Ruby
    
[5]: https://insights.stackoverflow.com/survey/2015#tech-lang
[6]: https://insights.stackoverflow.com/survey/2016#technology-most-popular-technologies
[7]: https://insights.stackoverflow.com/survey/2017#technology-_-programming-languages
[8]: https://insights.stackoverflow.com/survey/2018#technology-_-programming-scripting-and-markup-languages
[9]: https://insights.stackoverflow.com/survey/2019#technology-_-programming-scripting-and-markup-languages

Et la question, certainement la plus intéressante pour sentir le désir des développeurs, concerne les langages (au sens large) les plus aimés, les plus redoutés et les plus désirés.

### Le plus aimé ?

&emsp; &emsp;   2015       | 2016       |  2017      |  2018      | 2019
---------------------------|------------|------------|------------|-----------
&nbsp;1. &emsp; Swift      | Rust       | Rust       | Rust       | Rust
&nbsp;2. &emsp; C++11      | Swift      | Smalltalk  | Kotlin     | **Python**
&nbsp;3. &emsp; Rust       | F#         | TypeScript | **Python** | TypeScript
&nbsp;4. &emsp; Go         | Scala      | Swift      | TypeScript | Kotlin
&nbsp;5. &emsp; Clojure    | Go         | Go         | Go         | WebAsembly
&nbsp;6. &emsp; Scala      | Clojure    | **Python** | Swift      | Swift
&nbsp;7. &emsp; F#         | React      | Elixir     | JavaScript | Clojure
&nbsp;8. &emsp; Haskell    | Haskell    | C#         | C#         | Elixir
&nbsp;9. &emsp; C#         | **Python** | Scala      | F#         | Go
10. &emsp;      **Python** | C#         | Clojure    | Clojure    | C#

D’après les résultats de l’étude StackOverflow, Python est le premier langage de programmation qui est à la fois très utilisé et très aimé. C’est aussi le langage le plus désiré.

### Le plus désiré ?

&emsp; &emsp;  2015         | 2016       |  2017      |  2018      | 2019
----------------------------|------------|------------|------------|-----------
&nbsp; 1. &emsp; Android    | Android    | **Python** | **Python** | **Python**
&nbsp; 2. &emsp; JavaScript | Node.js    | JavaScript | JavaScript | JavaScript
&nbsp; 3. &emsp; **Python** | AngularJS  | Go         | Go         | Go
&nbsp; 4. &emsp; Node.js    | **Python** | C++        | Kotlin     | TypeScript
&nbsp; 5. &emsp; AngularJS  | JavaScript | Java       | TypeScript | Kotlin
&nbsp; 6. &emsp; Java       | React      | TypeScript | Java       | Rust
&nbsp; 7. &emsp; iOS        | Swift      | C#         | C++        | C++
&nbsp; 8. &emsp; Arduino/R.Pi| MongoDB    | Swift      | Swift      | WebAssembly
&nbsp; 9. &emsp; Swift      |Arduino/R.Pi| Ruby       | HTML       | Java
10. &emsp;       C#         | C++        | Rust       | CSS        | SQL

GitHub
------

Chaque année, l’[Octoverse de GitHub](https://octoverse.github.com/projects) comptabilise, à partir des dépôts privés et publics, le nombre de contributeurs uniques par langage de programmation, dont voici la liste des dix premiers langages :

&emsp; &emsp;   2014       | 2015       | 2016       | 2017       | 2018
---------------------------|------------|------------|------------|-------
&nbsp;1. &emsp; JavaScript | JavaScript | JavaScript | JavaScript | JavaScript
&nbsp;2. &emsp; Java       | Java       | Java       | Java       | Java
&nbsp;3. &emsp; PHP        | **Python** | **Python** | **Python** | **Python**
&nbsp;4. &emsp; **Python** | PHP        | PHP        | PHP        | PHP
&nbsp;5. &emsp; Ruby       | Ruby       | C#         | C++        | C++
&nbsp;6. &emsp; C++        | C++        | C++        | C#         | C#
&nbsp;7. &emsp; C          | C#         | Ruby       | C          | TypeScript
&nbsp;8. &emsp; C#         | C          | C          | Shell      | Shell
&nbsp;9. &emsp; Shell      | Shell      | Shell      | Ruby       | C
10.      &emsp; ObjectiveC | ObjectiveC | ObjectiveC | TypeScript | Ruby

Un autre résultat intéressant pour faire des prévisions est l’augmentation du nombre de contributeurs par langage informatique :

Augmentation | Langage
------------:|---------
+ 160 %      | [Kotlin](https://fr.wikipedia.org/wiki/Kotlin_(langage))
+ 120 %      | [HCL](https://github.com/hashicorp/hcl "HashiCorp Configuration Language")
+ 90 %      | [TypeScript](https://fr.wikipedia.org/wiki/TypeScript)
+ 70 %      | [PowerShell](https://fr.wikipedia.org/wiki/Windows_PowerShell)
+ 70 %      | [Rust](https://fr.wikipedia.org/wiki/Rust_(langage))
+ 60 %      | [CMake](https://fr.wikipedia.org/wiki/CMake)
+ 50 %      | [Go](https://fr.wikipedia.org/wiki/Go_(langage))
+ 50 %      | [**Python**](https://fr.wikipedia.org/wiki/Python_(langage))
+ 40 %      | [Groovy](https://fr.wikipedia.org/wiki/Groovy_(langage))

D’après les résultats de l’étude GitHub, Python est à la fois le langage ayant une des communautés d’utilisateurs la plus importante (en troisième position), mais aussi ayant une des plus fortes progressions du nombre de ses contributeurs sur la période 2017-2018 (+ 50 %).

Tiobe
-----

Tiobe a une approche indépendante des données des entreprises, pas besoin d’avoir accès aux métriques réseaux du site StackOverflow ou d’analyser les codes source publics et privés de GitHub. Tout simplement, Tiobe utilise une vingtaine de moteurs de recherche avec `+"Python programming"`, et prend le maximum du nombre de résultats (pour éviter de compter plusieurs fois les mêmes résultats). Les langages pouvant avoir des appellations différentes sont regroupés comme `JavaScript`, `JS` et `SSJS`. Les termes `"Python3 programming"`, `"Python-3 programming"` et `"Python 3 programming"` ne sont pas pris en compte.

![Indice Tiobe entre 2002 et 2019](http://olibre.github.io/GreatTips/python/news/tiobe-aout-2019.png)

Avant 2002, l’[indice Tiobe](https://www.tiobe.com/tiobe-index/) utilisait d’autres méthodes pour comptabiliser la popularité des langages de programmation. Son historique remonte à 1989, il y a trente ans !

Tiobe, décerne aussi le prix de la célébrité au langage ayant la plus forte hausse chaque année. Python est le langage ayant été le plus souvent lauréat du prix de la célébrité : en 2007, 2010 et 2018. Nous pouvons aussi supposer de même dans les années 1990 quand on voit que Python obtient des scores de plus de 20 % pour les années 1999 et 1994.

Pourquoi Python a autant de succès ?
====================================

* car vieux de 25 ans ?
* car interprété et lent ?
* car pas conçu pour la performance (ne minimise pas la [cache cohérence](https://fr.wikipedia.org/wiki/Protocole_de_cohérence_de_cache) entre processeurs) ?
* car l’indentation a une influence directe sur l’exécution ?
* car pas de typage statique à l’exécution ?
* car dépourvu de `switch`/`case` ?
* car les appels à des fonctions inexistantes se fait à l’exécution (et en prod) ?
* car `sudo pip install --upgrade pip` répare tout ? [N. D. M. : c’est ironique…]
* car on a le choix entre espaces et tabulations ?
* car on a toujours Python 2 ?
* car l’exécution parallélisée (_multi‐threading_) est super top gérée ?
* car on a les meilleurs outils de débogage et de profilage ?
* car c’est juste pour du prototypage, pas pour la prod ?

Allez, à ton clavier, nous avons hâte de connaître ton avis dans les commentaires. ✍🤔
