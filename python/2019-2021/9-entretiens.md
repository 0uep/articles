---
URL:     https://linuxfr.org/news/python-partie-11-entretiens
Title:   Python 2019/2021 — partie 9 — Entretiens
Authors: Collectif
         tisaac, Oliver, liberforce, Ysabeau, François GUÉRIN, Philippe F, serge_sans_paille, Jehan, Benoît Sibaud, Maderios, dovik, E3Ms6vyX et gusterhack
Date:    2019-09-23T00:58:59+02:00
License: CC By-SA
Tags:    python et entretien
Score:   23
---

Python 2019/2021 — partie 9 — Entretiens
=========================================

Pour cette dépêche, nous donnons la parole à celles et ceux qui pratiquent le langage de programmation Python : des développeuses et développeurs de différents domaines, mais aussi d’autres métiers comme les scientifiques des données *(data scientists)*, les scientifiques de l’apprentissage automatique *(machine learning)*, les analystes quantitatifs *(quant)*… et bien d’autres…

[![Un barbu se tien derrière un écran d'ordinateur qui affiche « partie = 13, "Entretiens" \n print(partie) » et à droite le logo de Python (deux serpents stylisés) entouré de petites icônes symbolisant la variété des domaines où s'applique Python.](9.webp)](https://github.com/linuxfr.org/articles/tree/main/python/2019-2021)

----

[Entretien avec Guido van Rossum (2018)](https://www.lemonde.fr/pixels/article/2018/07/25/je-n-imaginais-pas-que-python-connaitrait-un-tel-succes_5335917_4408996.html)
[Python — partie 1 ― Popularité](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-1)
[Python — partie 2 ― Python 2](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets)
[Python — partie 3 — Installation de Python et de paquets](https://linuxfr.org/news/python-pour-la-rentree-2019-partie-3-installation-de-python-et-de-paquets)
[Python — partie 4 — Py Pyenv ](https://linuxfr.org/news/python-pour-noel-2019-partie-4-py-pyenv)
[Python — partie 5 — Nix (et Guix)](https://linuxfr.org/news/python-partie-5-nix-et-guix)
[Python — partie 7 — Environnements virtuels](https://linuxfr.org/news/python-pour-noel-202x-partie-7-environnements-virtuels)
[Python— partie 8 — Pipenv](https://linuxfr.org/news/python-partie-8-pipenv)

----

# Entretien avec **tisaac**

![Avatar de tisaac sur linuxfr](https://img.linuxfr.org/avatars/325/081/000/avatar.png)

1. **Une petite présentation de ton parcours ?**
    
    J’ai un double background, d’une part d’ingénieur en mathématiques appliquées et d’autre part en économie. Je suis sans doute plus économiste qu’ingénieur.
    
    Dans le cadre de mes études et de mes expériences professionnelles, j’ai été amené à étudier/utiliser une série de langages et de logiciels informatique (Java, C++, matlab, [Dynare](https://www.dynare.org/) [qqn connaît Dynare ?], Stata, R, Biogeme). Pour les langages informatiques cela s’est presque exclusivement limité aux études.
    
    Aujourd’hui, on pourrait me définir comme modélisateur des transports avec un accent particulier sur les transports publics. En gros, j’interviens à différentes étapes dans l’établissement et l’exploitation de modèles à 4 étapes ou similaires (voir le [modèle à 4 étapes](https://fr.wikipedia.org/wiki/Modèle_de_déplacements_MODUS) spécifique mais bien représentatif de ce genre de modèle). Je suis aussi amené à faire des études plus ad-hoc, pudiquement appelée à dire d’expert. Par ailleurs, j’ai dans un poste précédent assumé un rôle de [*pricing analyst*](https://en.wikipedia.org/wiki/Price_analysis).
    
    Dans les deux cas (modélisation transport et pricing analyst), il y a pas mal d’analyses de données nécessaires et à force de rencontrer des Data Scientists, j’en viens à penser que je n’en suis pas très éloigné en tout cas des moins pointus.
    
2. **Comment as-tu commencé à utiliser Python ? Pourquoi ce langage ?**
    
    La première fois que j’ai croisé Python c’est durant un truc un peu bizarre, un atelier d’écriture musicale : en gros de la composition par des gens pas forcément musiciens. Les compositions étaient en lien avec le background initial des participants. J’ai donc mis en _musique_ de l’économie. Je ne me souviens plus trop mais en pratique, j’ai utilisé [Csound](https://csound.com/) qui faisait intervenir des scripts Python mais en gros cela s’est limité à des boucles for.
    
    Sinon fin de l’année dernière, je suis tombé sur un article de presse au sujet du site de formation en ligne [DataCamp](https://www.datacamp.com/) orienté Data Sciences. Je devais un peu m’ennuyer ce soir-là et j’ai testé l’un ou l’autre module et en victime du marketing, j’ai payé pour avoir accès à tous les cours. Une fois que j’ai payé, je me suis dit que je devais rentabiliser.
    
    Par ailleurs, en termes de motivation, à ce moment-là, on parlait pas mal de Data Sciences avec un collègue comme étant un truc que nous devions connaître si on voulait rester un peu employable. Finalement, je savais que j’allais avoir bientôt un projet d’estimation de modèle de choix discret un peu atypique et qui allait m’obliger à réécrire des scripts moi-même et pas seulement compter sur [Biogeme](http://biogeme.epfl.ch/).
    
    _DataCamp offre des formations en R et en Python, pourquoi avoir privilégié le second ?_ pourriez-vous me demander. Je vois trois raisons. Premièrement, quand on regarde les offres d’emploi pour Data Scientist, Python me semble beaucoup plus souvent mentionné que R. Deuxièmement, le fait que Python soit un langage informatique n’est pas pour me déplaire dans la mesure où je pense parfois à me remettre à la programmation dans mes temps libres. Troisièmement, nous utilisons [Visum](https://www.ptvgroup.com/fr/solutions/produits/ptv-visum/) et [ArcGis](https://www.esrifrance.fr/arcgis.aspx) dans lesquels il y a moyen de faire des choses customisées en écrivant des scripts Python.
    
3. **Qu’est-ce que tu as trouvé de facile ? As-tu eu des frustrations ?**
    
    Ce qui est impressionnant, c’est la puissance de certains paquets et leur nombre. En termes de frustrations, cela reste des scripts informatiques avec des bugs que tu mets parfois pas mal de temps à comprendre. À certains moments, j’aimerais avoir un meilleur background en informatique parce que je sens bien que sur certains trucs, nous ne sommes pas très efficaces.
    
    Ce qui est compliqué, c’est de comprendre les manières d’écrire de telle sorte que le programme soit le plus rapide possible. Dans certains cas, c’est assez simple à comprendre pourquoi une manière est plus efficace qu’une autre mais dans d’autres situations, c’est vachement moins évident et tu n’as en fait rien à comprendre. Tu dois juste retenir que certaines implémentations/paquets sont plus rapides que d’autres. Cet élément fait que Python a une part quand même pas du tout intuitive.
    
4. **Qu’est-ce que Python t’apporte ? Comment ferais-tu sans ?**
    
    Sans Python, j’utiliserais sans doute R et des bases de données SQL.
    
5. **Quelle a été ta progression dans la maîtrise de Python ?**
    
    C’est un peu comme la vision que ma mère a de l’anglais. Elle dit que c’est simple et assez rapide d’arriver à communiquer en anglais mais quasi impossible pour un non-natif de maîtriser toutes les subtilités de la langue. Pour sortir un truc qui fonctionne en Python, c’est vraiment pas compliqué par contre pour bien exploiter toutes ses possibilités, c’est vachement plus long. Malheureusement pour moi, je ne passe pas assez de temps à scripter en Python (j’ai plus un rôle de supervision dans l’équipe), donc je suis et je reste plutôt à un niveau assez basique.
    
6. **Tes conseils pour les débutants ?**
    
    Apprendre un peu l’esprit de Python. La manière d’écrire de manière pythonique. J’ai l’impression que pour un béotien, cela peut aider à faire des trucs plus propres et lisibles.
    
    Ne pas vouloir réinventer la roue. Il y a plein de paquets qui implémentent énormément de chose. La perte de temps de chercher les paquets pertinents pour ton problème est largement compensée par le fait de ne pas devoir écrire (et déboguer) soi-même le script.
    
    Un peu contradictoire avec le conseil précédent, fais attention à ne pas te perdre dans la myriade de paquets existants. Au départ, il est sans doute bon de se concentrer sur un nombre limité de paquets et apprendre à bien les maîtriser. [SciPy](https://www.scipy.org/) est dans mon domaine sans doute une porte d’entrée incontournable.
    
    ~~Google~~ Internet est ton ami. Il y a plein de documentations en ligne. Sans doute aussi plein de forum de discussion mais jusqu’à présent mes problèmes ont à chaque fois été résolus avec la documentation.

# Entretien avec **serge sans paille**

[**serge sans paille**](https://linuxfr.org/users/serge_ss_paille) est un habitué sur LinuxFr.org et également l’auteur du fabuleux logiciel [pythran](https://pythran.readthedocs.io/en/latest/) souvent présenté dans nos [colonnes](https://linuxfr.org/users/serge_ss_paille/journaux/pythran-0-9-3-a-une-fedora-sur-la-tete) qui permet de [transpiler](https://fr.wikipedia.org/wiki/Compilateur_source_%C3%A0_source) (convertir) le Python en C++ pour booster les performances.

1. **Une petite présentation de ton parcours ?**
    
    Alors au début je suis allé à droite, puis bas, diagonale bas-droite, droite + punch… je m’égare.
    
    Je suis ce qu’on appelle un dev C++, c’était le cas à l’époque et c’est toujours le cas. À l’époque dans ma boîte à outil script, il n’y avait que ``/bin/sh``.
    
2. **Comment as-tu commencé à utiliser Python ? Pourquoi ce langage ?**
    
    Le hasard :-) Une personne chère à mon cœur s’était inscrite à une formation, elle n’a pas pu y aller, j’y suis allé à sa place… C’était au début de ma thèse donc… vers 2008.
    
3. **Qu’est-ce que tu as trouvé de facile ? As-tu eu des frustrations ?**
    
    Les structures de données de base sont là, le flot de contrôle est simple, la bibliothèque de base est riche… Le typage est implicite, c’est facile et rapide à prendre en main.
    
    L’absence de **possibilité** d’écrire un vérificateur de type qui soit complet est une grosse frustration. Ou plutôt c’est très frustrant de voir les efforts qui sont mis pour essayer de calquer un système de type partiel sur un langage pas prévu pour.
    
4. **Qu’est-ce que Python t’apporte ? Comment ferais-tu sans ?**
    
    Un magnifique jouet, il y a beaucoup de subtilité dans ce langage qui parait pourtant simple :-) C’est un chouette sujet d’étude. Au quotidien, pour être productif sur des scripts de petite à moyenne taille, c’est mon choix par défaut. Sans lui… je ferais ça en shell, ce qui étale ma faiblesse linguistique :-/
    
5. **Quelle a été ta progression dans la maîtrise de Python ?**
    
    ```
    compétence
        ^
        |                    ____-----
        |            ____----
        |   ____-----
        |  /
        | /
        |/
        +---------------------------------> temps
    ```
    
    Maintenant, à travers mon investissement dans le (magnifique, mais vous le savez déjà) projet [pythran](https://github.com/serge-sans-paille/pythran), j’ai une bonne compréhension de ce qui tourne autour du langage et de ses performances, et de l’interface native. Il m’est arrivé de présenter à PyConFR voire de proposer des patchs mineurs (c’était il y a moins de 18 ans) à CPython.
    
6. **Qu’est ce qui te plaît le plus ?**
    
    L’accessibilité de l’implémentation de référence, cpython (le code source reste appréhendable). La communauté pas trop prise de tête. La diversité de l’écosystème. L’accent mis sur l’outillage. La lib standard.
    
7. **Tes conseils pour les débutants ?**
    
    Comme dans toute activité : pratiquer, essayer, se faire relire, s’intéresser, discuter. L’informatique peut être une activité très sociale !
    
8. **Que faudrait-il améliorer ?**
    
    Il faut savoir s’arrêter, consolider l’existant plutôt que toujours aller de l’avant. Par exemple l’ajout d’un champ ``type_comment`` dans de nombreux nœuds de l'[AST](https://fr.wikipedia.org/wiki/Arbre_de_la_syntaxe_abstraite) en 3.8, champs mis par défaut à ``None``, à moins de demander explicitement le traitement des informations de type, donne une impression de cul entre deux chaises.
    
    La gestion des dépendances natives, qui sont au cœur du langage (et oui, Python est quand même un langage de glu à la base), mais reléguées au rang de citoyen de seconde zone du système d’empaquetage, est un vrai problème (et un problème complexe hein).
    
9. **Quels sujets souhaiterais-tu lire dans les prochaines dépêches ?**
    
    Euhhh… Python et performances ? Python et typage ?

# Entretien avec **Papoteur**

[**Papoteur**](https://github.com/papoteur-mga) est un important contributeur du projet [Mageia](https://fr.wikipedia.org/wiki/Mageia). Il a développé pour Mageia l’application [IsoDumper](https://wiki.mageia.org/en/IsoDumper_:_%C3%A9crire_une_image_ISO_sur_une_clef_USB-fr) qui permet de faire facilement des clés bootables.

![Mageia](https://www.mageia.org/g/media/logo/mageia-2013.svg)

1. **Comment as-tu connu le monde des ordinateurs, en quelle année ?**
    
    Ça devait être un Digital Equipement en 1980, quelque chose comme ça.
    
2. **Quelles études as-tu faites, étaient-ce dans le domaine informatique ?**
    
    Des études technologiques, mais pas orientées informatiques. Donc avec un peu de Fortran, IV il me semble.
Autodidacte pour l’essentiel. Avec, à côté, ma femme qui, elle, est diplômée en informatique.
    
3. **Comment as-tu commencé à utiliser Python ? Pourquoi ce langage ?**
    
    J’avais utilisé du Basic et des macros Excel en milieu pro. Je n’avais pas l’intention de devenir un pro de la programmation, donc je voulais me concentrer sur un seul langage, qui soit suffisamment souple d’utilisation et universel. C et C++ me semblaient beaucoup moins abordables. PHP spécialisé sur le Web.
    
    Mon premier programme public est un outil d’écriture d’images ISO sur clé USB, à partir d’un fork. Puis quelques autres utilitaires pour Linux/Mageia.
    
4. **Qu’est-ce que tu as trouvé de facile ?**
    
    L’indentation qui représente l’imbrication facilite l’écriture (pas de contrainte sur les crochets de fermeture oubliés, décalés), même si la coexistence des espaces et des tabulations est source d’énervement. J’apprécie également les formes itératives et la souplesse d’utilisation des variables sans typage.
    
5. **As-tu eu des frustrations ?**
    
    Ce qui m’a le plus contrarié : les formes d’import de mes parties en module selon le contexte de développement ou d’installation.
    
6. **Qu’est-ce que Python t’apporte ? Comment ferais-tu sans ?**
     
    Nul ne peut avoir la prétention d’être irremplaçable. J’aurais regardé du côté de Java, C++, PHP pour ce qui est Web.
    
7. **Quel est le truc le plus balaise avec Python ?**
     
    Faire un backend qui communique en Dbus avec l’application frontale pour exécuter des actions avec droits root.
    
8. **Est-ce que tu en apprends encore tous les jours ?**
    
    Le sujet est tellement vaste qu’il est inépuisable.
    
9. **Qu’est ce qui te plaît le plus ?**
    
    En premier, c’est le langage lui-même, complété par un vaste champ de modules complémentaires. Je ne me souviens pas d’avoir sollicité la communauté, mais par contre consulté nombre de ressources pour trouver des exemples. Open source, évidemment, je n’imagine pas utiliser autre chose.
    
10. **Quels sujets souhaiterais-tu lire dans les prochaines dépêches ?**
    
    Le choix et l’utilisation d’un IDE (ou pas), en particulier pour le débogage.

# Entretien avec [**liberforce**](https://linuxfr.org/users/liberf0rce)

![Avatar de liberforce sur linuxfr](https://img.linuxfr.org/avatars/624/019/000/avatar.png)

1. **Une petite présentation de ton parcours ?**
    
    Mon cousin a 10 ans de plus que moi, et a fait des études d’électronique et informatique, il a eu un Amstrad puis un Amiga 2000, machine assez fascinante. J’ai eu un Amiga 500 à Noël pour mes 12 ans, et même si je l’ai surtout utilisé pour jouer, cela a été mon premier vrai contact avec un shell. Amigaïste un jour, Amigaïste toujours.
    
    Toujours sur les conseils de mon cousin, j’ai découvert les calculatrices HP48 en classe de première, et fait mes premiers pas en programmation sur le bestiau. Je me suis fadé le manuel raccourci, puis le gros de 500 pages… J’ai encore un émulateur HP48 sur mon smartphone quand il s’agit de faire quelques calculs.
    
    J’ai ensuite fait un DUT génie électrique et informatique industrielle option électronique (toujours sur les traces de mon cousin, passé par là 10 ans avant). Big up à l’IUT de Cachan, ce furent deux années extraordinaires. J’ai ensuite suivi ma propre voie en faisant une école d’ingénieur par apprentissage (pour gagner des sous vs en dépenser pour une école privée).
    
2. **Comment as-tu commencé à utiliser Python ? Pourquoi ce langage ?**
    
    Je crois bien que c’est sur les conseils de LinuxFr qui parlait pas mal de ce langage qui montait. J’avais une interface graphique déportée à faire pour le boulot, je m’intéressais à GNOME et GTK+. Le python avait cette réputation de facilité et surtout de lisibilité, on en parlait déjà en bien sur LinuxFr. Alors je me suis naturellement tourné vers pyGTK pour réaliser ce projet. Cela a été mon premier contact concret avec python.
    
    Je tiens à préciser aussi que j’avais (à la même époque ? Quelques années avant ?) gagné un livre sur LinuxFr dans les récompenses aux meilleurs contributeurs, et j’avais choisi un livre sur Python, c’est donc un peu grâce à vous que j’en suis là ;-).
    
3. **Qu’est-ce que tu as trouvé de facile ? As-tu eu des frustrations ?**
    
    Pfiou, ça date. 2006 ? 2007 ? Venant du C/C++, je me rappelle avoir été un désarçonné par le rôle de l’indentation dans le langage. Tous mes fichiers de l’époque sont comme mes fichiers C, indentés avec des tabulations ☺. J’avais aussi un peu effleuré perl et, sans vouloir troller, c’était le jour et la nuit tellement le code python me semblait plus lisible.
    
    Dans les frustrations, en plus de l’indentation, je crois que les args et kwargs étaient un peu obscurs au début, surtout à cause de leur notation à base d’étoiles assez différentes du C.  
    
4. **Qu’est-ce que Python t’apporte ? Comment ferais-tu sans ?**
    
    Déjà, il m’apporte des sous ☺. Je fais du python à temps plein depuis un peu plus de 2 ans. Sans ? Je ferais du Rust :-D ! Prochaine étape sans doute, quand j’aurai l’occasion.
    
5. **Quelle a été ta progression dans la maîtrise de Python ?**
    
    Je ne fais pas franchement de truc de haut vol, je reste un (très) modeste développeur loin d’avoir encore appris l’essentiel.
    
    Ma plus grande fierté en python ? Mon premier projet, une interface graphique qui montrait en « temps réel » et de manière très fluide l’état de mon système pour le boulot. J’avais pas mal bossé sur l’amélioration des performances, l’utilisation de cairo, et ça rendait du feu de dieu.
    
    Le truc le plus balaise ? Je vous le dirai quand je l’aurai écrit :-)
    
    Est-ce que j’en apprends tous les jours ? Clairement, développeur c’est un métier sans fin. Et même le python avec sa réputation de facilité a quand même des parties un peu cryptiques. Le typage statique et mypy, les évolutions du langage pour la gestion asynchrone, les subtilités des dataclass… Oui, je pense que j’en apprends encore régulièrement, surtout que le langage change et que je dois avoir en cumulé 3 ans ½ d’expérience.
    
6. **Qu’est ce qui te plaît le plus ?**
    
    La philosophie de Python, le Zen qui m’a permis de mieux comprendre certains concepts que j’avais assimilés empiriquement. « Explicit is better than implicit » est certainement ce qui me sert le plus dans la vie de tous les jours, car beaucoup de gens sont trop implicites dans leur communication. J’essaie de me mettre à la place de quelqu’un qui ne connait pas le sujet quand j’explique des choses, pour m’assurer que mon message reste compréhensible.
    
7. **Tes conseils pour les débutants ?**
    
    De nos jours il y a plein de ressources pour apprendre le python. J’avais utilisé l’application enki d’enki.com sur Android pendant un moment, c’était pas mal pour apprendre de manière progressive un petit peu chaque jour.
    
8. **Que faudrait-il améliorer ?**
    
    Unifier la partie packaging, les solutions pullulant entre les pip-tools, pipenv, poetry et consors.
    
9. **Quels sujets souhaiterais-tu lire dans les prochaines dépêches ?**
    
    Le typage et comment bien l’utiliser est un sujet hautement intéressant pour un langage qui a la réputation d’être typé dynamiquement.
    
    Les stratégies d’analyse statique aussi seraient intéressantes (quelle combinaison d’outils).
    
    Enfin, les stratégies de test, mocking, test doubles (doublures de test en VF) avec pytest par exemple.
    
    En gros, tout ce qui permet de faire du code de qualité afin de pouvoir coder sereinement.

# Entretien avec [**frague**](https://linuxfr.org/users/frague)

![Avatar de frague sur linuxfr](https://img.linuxfr.org/avatars/928/030/000/avatar.png)

1. **Une petite présentation de ton parcours ?**
    
    J'ai touché un ordinateur la première fois en classe de 3ême, c'était un [Commodore 64](https://fr.wikipedia.org/wiki/Commodore_64)... Çà ne date pas d'hier (83 ?), mais j'ai été mordu.
    
    J'ai alors découvert qu'on pouvait afficher des trucs colorée sur un écran, mais surtout qu'on pouvait demander à l'ordinateur de faire des trucs, via un langage de programmation - du BASIC.
    
    Mon premier ordi perso était un [Hector HR-MX](http://hectorvictor.free.fr/index.php?page=tEHwE7/blZIJ.O), acheté avec la paye de mon premier job d'été. Basic et Forth !
    
    Je n'ai pas fait d'études d'informatique, j'ai travaillé dans le dessin industriel, le meuble... mais l'informatique m'a toujours titillé. J'ai fini par faire une reconversion professionnelle, et je suis maintenant développeur depuis une vingtaine d'année. J'ai fini par valider mon expérience par une Licence Pro Da2I à Lille obtenue en 2004.
    
    J'ai fait un petit peu de C, du VBA, du C#... Je n'ai quasiment fait que du Web.
    
2. **Comment as tu commencé à utiliser Python ? Pourquoi ce langage ?**
    
    Vers 2011, j'avais besoin d'un cadriciel pour faire des applis Web. Mon employeur n'avait pas de préférences quant aux outils / langages de développement. Il est à noter que je travaille dans la fonction publique territoriale. 
    
    J'avais alors un petit peu touché à Php, mais je n'était pas emballé - c'était à l'époque php 5, avec ses incohérences criantes.
    
    J'étais à la recherche d'un cadriciel pas trop de haut niveau, mais qui proposait un ORM et une interface d'admin "out of the box". Je sortais d'un truc où le seul endroit où je pouvais taper du code, c'était dans les requêtes SQL, dans un client lourd qui flinguait les indentations à chaque fois que tu sauvegardais la page...  
    J'ai fait une tour du marché des cadriciels de l'époque, et je suis tombé sur Django. 
    
3. **Qu'est ce que tu as trouvé de facile ? As-tu eu des frustrations ?**
    
    Mon premier projet avec Django était un système de calcul de facturation annuelles, basé sur des périodes mensuelles. C'était assez technique, avec des calculs en fenêtres glissantes...
    
    Et bien cà a marche en 3 mois de dev, découvrant en même temps le python (2.7) et Django (1.3). Les deux m'ont séduit !
    
    D'ailleurs je l'ai ré-écrit 1 an plus tard avec l'arrivé des CBV des django 1.4...
    
    Depuis, je continue à faire du dév en python, je fais toujours du Django et un peu de Flask aussi. La richesse de l'écosystème autour de Python me fascine - Il y a toujours quelqu'un qui a fait une lib qui réponds en partie à tes besoins, tu n'a que de la colle à ajouter, et la partie métier, qui est la valeur ajoutée du truc !
     
4. **Qu'est ce que Python t'apporte ? Comment ferais-tu sans ?**
    
    Python est simple à lire et à relire. J'ai des application qui ont été commencé en 2012, et qui tournent et évoluent toujours. Je suis le seul développeur de ma collectivité, je m'occupe de tout "du sol au plafond". J'ai mes utilisateurs à disposition (mes collègues), et ils sont la plupart du temps contents de m'avoir sous la main, que ce soit pour des dévs rapides de 3 / 4 jours (Flask / DB−less) ou pour des projets plus conséquents (Django).
    
5. **Quelle a été ta progression dans la maîtrise de Python ?**
    
    Comme expliqué plus haut, j'ai appris Python "sur le tas". Ma plus grande fierté, c'est que mes applis, grandes ou petites, fonctionnent et rendent service ! J'apprends encore des trucs tous les jours...
    
6. **Qu'est ce qui te plaît le plus ?**
    
    * Le langage [x]
    * La diversité des paquets [x]
    * La communauté et l'entraide [x]
    * La gratuité ? L'accès aux sources ? Le partage *licence libre* [x]
    
    Je coche tout ! J'ai eu l'occasion d'aller à des PyConFR, la qualité et le sympathie des gens rencontrés là-bas était tout bonnement extraordinaire. Et j'apprends tout les jours, ce qui est super !
    
7. **Tes conseils pour les débutants ?**
    
    Plongez ! Il y a plein de tutos sur internet ! 
    
    Plus sérieusement, pensez à vos algos, le langage de programmation est une façon de les écrire, pas un fin en soi. Mais, par contre Python apporte une vrai lisibilité et une vraie communicabilité de ces algos, je le recommande toujours chaudement aux jeunes gens qui viennent me parler d'informatique.
    
    Sinon, aussi, utiliser un bon débogueur pas-à-pas permet de comprendre finement ce qui se passe quand un script s'exécute, çà a de vraies vertus pédagogiques. Utilisez-en un - çà permet de démystifier la magie opérante...
    
8. **Que faudrait il améliorer ?**
    
    + Packaging / environnement virtuels (c'est la grosse question en ce moment autour de python)
    + setup.cfg vs. pyproject.toml vs. dot files... C'est carrément la jungle, le dossier racine des projets...
    
9. **Quels sujets souhaiterais tu lire dans les prochaines dépêches ?**
    
    Pareil que Liberforce : typing / tests / mocking / qualitay !

# Entretien avec [**Jehan**](https://linuxfr.org/users/jehan)

![Avatar de Jehan sur linuxfr](https://img.linuxfr.org/avatars/621/031/000/avatar.jpg)

1. **Une petite présentation de ton parcours ?**
    
    Bien que j’ai eu des contacts intermittents avec l’informatique avant, c’est vraiment au lycée qu’un ami me traîne au club informatique régulièrement. C’est aussi vers le milieu du lycée que j’ai eu mon premier ordinateur (Pentium 2?).
    
    Néanmoins même si l’idée du développement me plaît, c’est surtout les jeux vidéos et notamment en réseau que je découvre à ce moment là. Contrairement à beaucoup de développeurs qui ont de la famille ingénieur et ont commencé très tôt, ma famille est dans le milieu artistique et toutes les capacités d’un ordinateur et les possibilités d’interagir avec me passaient un peu à côté.
    
    Pendant une prépa maths, un ami me vante Linux pour la première fois. À cet époque, je le rembarre gentillement, puisque ce système ne m’aurait plus permis de jouer à mes jeux vidéos préférés. Pourtant lorsque je bifurque en licence informatique (directement en troisième année), je découvre que tous les ordinateurs des salles d’informatique de l’université sont sous Linux, je demande donc "Linux" à mon ami : il me fournit un CD d’installation de [Mandrake](https://fr.wikipedia.org/wiki/Mandriva_Linux#Le_nom_et_le_logo).  Comme j’ai toujours le même ordinateur depuis le lycée et que le disque dur est plutôt petit, je supprime Windows et installe Mandrake Linux par dessus (pas de dual boot). Me voici donc pour la première fois sur un OS Libre. Plus jamais je n’ai réinstallé Windows pour mon utilisation perso depuis (presque 20 ans). À l’université, j’ai été forcé d’apprendre à maîtriser cet OS et ses logiciels rapidement, sans même avoir les bases (ligne de commande, scripts, organisation des fichiers… tout était nouveau). Même en développement, en troisième année, on nous apprenait Java et Ada95, tout en supposant qu’on savait le C (je n’en avais jamais fait, j’ai dû apprendre sur le tas en lisant du code). À ce jour, je n’ai jamais eu le moindre cours pour ce langage, mais force est de constater que cela importe peu au final! 🙂
    
    Après cela, j’ai progressivement commencé à m’intéresser au concept de logiciel libre qui m’a vite séduit. L’un des premiers projets majeurs auquel j’ai beaucoup contribué et sur lequel on m’a donné des droits d’écriture puis la maintenance fut l’émulateur de terminal [mrxvt](https://gitlab.com/Jehan_ZeMarmot/mrxvt) que j’utilisais à l’époque car j’avais besoin d’un terminal rapide sur ma machine peu puissante (les terminaux plus répandus étaient tous super lents). J’ai utilisé ce terminal de nombreuses années, surtout qu’à une époque, j’ai vagabondé et ai travaillé pendant des années sur des mini-machines type *EeePC* où j’avais vraiment besoin d’un terminal réactif. De nos jours, je n’utilise plus ce terminal dont la maintenance est malheureusement abandonnée.
    
    L’autre gros projet qui m’intéressa fut [XMPP](https://xmpp.org/), au point que j’ai été membre quelques années de la XSF (*XMPP Standards Foundation*) et qu’on retrouve mon nom dans les sections *Acknowledgements* des RFCs [6120](https://tools.ietf.org/html/rfc6120#appendix-E), [6121](https://tools.ietf.org/html/rfc6121#appendix-F) et [6122](https://tools.ietf.org/html/rfc6122#appendix-D) (la première vague de mises-à-jour du protocole vers 2011). J’ai cependant mis de côté mon implication sur ce protocole après de nombreuses années à aider à la standardisation, à la communication (j’avais notamment organisé un [évènement à la Cité des Sciences pour les 10 ans du protocole](https://linuxfr.org/news/anniversaire-decennal-de-jabberxmpp-le-28-fevrier); et d’ailleurs si maintenant les habitués de Linuxfr pensent peut-être à moi pour mes commentaires sur GIMP ou le droit d’auteur, il fut un temps où j’étais [un de ceux](https://linuxfr.org/news/xmpp-au-printemps-le-grand-rafraichissement) qui [parlaient beaucoup de XMPP](https://linuxfr.org/news/petit-etat-de-lart-de-quelques-aspects-de-la-messagerie-instantanee) ici) et avec du développement. Notamment j’avais développé des plug-ins Wordpress. L’un d’eux permettait de se [connecter sur son compte Wordpress](https://wordpress.org/plugins/xmpp-auth/) sans mot de passe, avec un échange de token via XMPP (on recevait une popup sur son client XMPP — potentiellement sur une autre machine — qui nous informait que quelqu’un essayait de se connecter, on pouvait alors accepter ou refuser, et la connexion se faisait automatique sur canal web en fonction du choix sur canal IM). De même ce plug-in permettait de commenter avec validation XMPP (similairement au fait qu’on mette une adresse email pour commenter sur un blog, sauf que le champs XMPP était réellement utilisé pour vérifier que ce n’était pas de l’usurpation d’identité et que l’adresse était utilisée, diminuant ainsi le spam). Personnellement je trouve toujours que c’était une idée cool et j’aurais aimé que ça prenne mais à l’époque les gens n’étaient pas si intéressés par ce type d’usage. Des années plus tard seulement, les concepts d’identification par canal séparé sont devenus classiques (à l’époque, je m’imaginais qu’un jour on pourrait s’identifier sur plein de sites avec son compte XMPP), sauf que ça a divergé par de l’identification GAFAM à la place, comme on le sait 😢. Gros loupé! Enfin bon, toute une époque où j’avais énormément d’idées et de projets sur base de XMPP, mais c’est le passé 🕰️.
    
    Le dernier gros projet pour lequel on me connaît mieux est donc [GIMP](https://www.gimp.org/) 🖌️🖼️, sur lequel j’ai commencé à contribuer fin 2012 avec des patchs mineurs, puis majeurs, et de plus en plus… jusqu’à en être devenu mainteneur récemment, grâce au projet [ZeMarmot](https://film.zemarmot.net/) pour lequel on fait du [financement participatif](https://liberapay.com/ZeMarmot/) depuis quelques années afin d’essayer de vivre de développement sur GIMP!
    
2. **Comment as tu commencé à utiliser Python ? Pourquoi ce langage ?**
    
    J’ai commencé à utiliser Python en 2011, je pense. À l’époque, je travaillais pour une startup à Tokyo (en télé-travail depuis la Corée du Sud) dont la plateforme web utilisait PHP. Comme Python était le langage à la mode, certains ont poussé pour un port du site vers Python (sans bonne raison d’après moi, hormis que le PHP était pas "hype" alors que Python était à la mode), puis le projet a été tué par les managers après 6 mois… 6 mois de travail perdu! C’est à ce moment là que j’ai vraiment appris le Python.
    
    Personnellement je suis technologie-agnostique, c’est à dire que je me fiche un peu des chipoteries sur les langages ou autres guerres de chapelle. J’aime bien Python, c’est un fait. Mais j’ai aussi bien aimé Objective Caml (même si je l’ai trouvé un peu lourd d’usage sur des projets plus poussés), de même que Ada95 (un des langages qui m’a le plus épaté et j’adorais sa rigueur; malheureusement je n’ai pas eu l’occasion d’énormément l’utiliser par la suite)… Même PHP, j’aimais bien (le langage a certes ses petites incohérences et on sent bien qu’il est né de façon un peu bordélique, mais il n’en reste pas moins agréable et j’ai fait des trucs très cool avec. J’avais même écrit un parseur XMPP entièrement en PHP, simpliste mais entièrement fonctionnel, rapidement et en très peu de code, pour mes plug-ins Wordpress/XMPP; ça marchait très bien! 🙂). De nos jours, j’utilise majoritairement du C (comme on peut se l’imaginer pour GIMP), et pas mal de Python sur des projets à côté, ou dès que je veux faire des petits scripts rapides et que `bash` atteint quelques limites (trop gros scripts `bash` qui deviennent alors difficiles à lire et maintenir).
    
    En gros, ma logique lorsque je veux automatiser un processus pour moi (ma raison principale de programmer), c’est d’essayer d’abord de faire un script shell POSIX, puis je passe en bash lorsque ça commence à être compliqué de faire du généraliste, et enfin en Python lorsque le code bash devient trop complexe et peu lisible. C’est souvent mon processus de choix de langage pour tout ce que j’écris de zéro pour mes besoins personnels.
    
3. **Qu’est ce que tu as trouvé de facile ? As-tu eu des frustrations ?**
    
    J’aime bien l’indentation significative de Python, ce qui permet de forcer au code propre (dans un projet comme GIMP en C, on est forcé de beaucoup re-demander aux nouveaux contributeurs de bien suivre nos règles de style de code, car la qualité tout comme le style du code sont très importants pour du code maintenable; dans un projet en Python, c’est un peu moins nécessaire d’imposer certaines règles puisqu’elles viennent avec la syntaxe du langage, même si ce n’est pas entièrement vrai et il reste des choix de style à faire).
    
    J’aime aussi bien ses capacités d’introspection, ce qui permet très facilement de créer du code modulable et auto-augmentable, capacités que j’ai utilisé sur plusieurs projets personnels comme professionnels.
    
    J’étais moins fan de fonctionnalités plus avancés de Python, car comme beaucoup de fonctionnalités avancées dans la plupart des langages, elles rendent le code plus dur à lire. Parfois quand je lis du code d’autrui qui aime utiliser les fonctionnalités les plus avancées, j’ai l’impression que certains utilisent ces syntaxes juste parce qu’elles permettent de faire du code plus petit (mais pas plus compréhensible pour autant) ou de montrer sa grande connaissance du langage, et ce aux dépends de la lisibilité et de la maintenabilité. Pour moi, c’est un problème. Mais avec le temps, je suis peut-être moi-même devenu un de ceux qui utilisent des syntaxes avancées un peu absconses au final. Je suis pas sûr. Aussi peut-être que je suis juste paresseux!
    
    Sinon j’aime beaucoup le typage fort (c’est pour que j’adore le langage Ada), même si parfois ça peut aussi rendre certains types de code problématique (notamment les conversions entre type — ce n’est pas forcément un problème conceptuel d’architecture de code ! — peuvent être parfois laborieuses dans certains langages à typage fort). Cela peut rendre un code bien plus robuste et aider à détecter certains types de bugs rapidement, à un niveau plus conceptuel. Donc on peut se demander pourquoi utiliser Python (typiquement le type de langage de script qui cache plein de types d’erreurs de par son typage faible). Néanmoins je ne suis pas sûr qu’il faille changer Python dans un tel sens pour autant. Ce qui fait sa force est aussi sa simplicité pour du code rapide à écrire. Chacun son truc…
    
4. **Qu’est ce que Python t’apporte ? Comment ferais-tu sans ?**
    
    Ça m’apporte juste le fait que ça existe et que je sais l’écrire, donc je m’embête pas. J’utilise. En fait, autant je suis technologie-agnostique, autant je ne suis pas intéressé par apprendre tous les langages informatiques possibles ou bien toutes les fonctionnalités les plus avancées de ces langages. Juste apprendre pour apprendre (attention, c’est très bien d’apprendre pour la beauté du geste, mais au bout d’un moment, on fatigue; perso je préfère apprendre pour arriver à un résultat et parce que ça m’est utile) ne m’intéresse plus autant. Être agnostique signifie juste que je m’en fiche un peu dans quel langage est écrit un logiciel auquel je veux contribuer. Je m’adapte. Bon, bien sûr, si c’est un langage que je connais bien, c’est plus simple, donc je peux me lancer plus facilement, sinon je fais avec, et je lis juste le code lentement pour comprendre ce qu’il fait et comment ce langage fonctionne (on découvre rapidement que ce n’est pas si compliqué).
    
    Par contre, pour mes projets, je me simplifie la vie et prend ce que je connais bien, donc Python. C’est tout! 😛
    
    Et donc sans? J’utiliserais un autre langage, c’est tout!
    
5. **Quelle a été ta progression dans la maîtrise de Python ?**
    
    Rapide au début, puis assez stable pendant des années, je dirais. Je cherche pas forcément à faire les trucs les plus compliqués, comme je disais plus haut, car je privilégie un code lisible et simple. J’apprends bien sûr encore de temps en temps des trucs nouveaux, mais pas tant que cela, et je ne cherche pas particulièrement.
    
    Mon projet le plus important avec Python est probablement [Crossroad](https://pypi.org/project/crossroad/), mon outil d’aide à la cross-compilation.
    
6. **Qu’est ce qui te plaît le plus ?**
    
    L’API standard est plutôt bien remplie et sa documentation est bien faite. D’ailleurs j’ai un mot clé pour la doc Python qui m’amène automatiquement sur un module dont je veux l’information. Par exemple, si je tape "*py3 time*" dans ma barre d’URL de Firefox, ça m’emmène à la documentation du module `time` pour Python 3 (j’ai aussi un mot clé `py2` mais comme on peut se l’imaginer, je n’ai plus énormément de raisons de l’utiliser).
    
    J’aime bien aussi le dépôt communautaire [Pypi](https://pypi.org/) car on y trouve énormément de modules supplémentaires utiles, même si je sais qu’il y a une bonne dose de divergences d’opinion à son sujet, notamment à cause des risques de tels dépôts moins contrôlés. Ces critiques sont d’ailleurs fondées: il ne faut pas installer n’importe quoi. Néanmoins cela n’enlève pas l’utilité du dépôt si on fait attention et si on est conscient des problèmes potentiels. Je fais toujours des recherches préalables à l’installation d’un paquet pip, notamment sur les auteurs, la licence bien sûr, et quelques vérifications du code.
    
    Ensuite j’aime beaucoup le shell interactif `ipython`, super utile pour tester rapidement du code. C’est le type d’outil qui apporte énormément au confort de développement.
    
7. **Tes conseils pour les débutants ?**
    
    Mes conseils pour les débutants ne dépendent pas du langage: corrigez/contribuez à ce qui vous intéresse. Si vous rencontrez un bug, ou si vous avez besoin d’une fonctionnalité, regardez le code et contribuez un patch. C’est le meilleur moyen d’apprendre et de progresser.
    
    C’est bien simple: les débutants qui viennent nous voir et nous demandent « *qu’est-ce que je peux faire si je veux apprendre/contribuer ?* », même si on les redirige vers des bugs simples, on ne les revoit quasi jamais. Par contre ceux qui ont rencontré un problème et veulent juste le corriger, ou ont un besoin et veulent le remplir, ceux-ci n’ont pas besoin de demander. Et même s’ils sont débutants, ils progressent toujours le plus vite. Typiquement essayez de développer **pour vous**, pour vos propres besoins, parce que vous en avez envie. Pas « pour apprendre » ou « pour remplir votre CV » ou « parce que ça fait bien » ou « parce qu’on vous a dit que c’est ce qu’il faut faire », ce qui serait la recette pour un échec sûr. Faire un code qui vous est réellement utile et qui ensuite vous sert au quotidien est tellement plus gratifiant donc ça se fait tout seul ! 😃
    
    Personnellement tous mes développements personnels depuis les ~15 ans que je développe sont juste des choses qui me tenaient à cœur ou des problèmes ou manques que je rencontrais, tout simplement (en plus des contributions sur GIMP et associés, j’ai des petits patchs épars sur des projets aussi divers que Firefox, Blender, mplayer puis mpv, Entangle, Linux Stopmotion, et des dizaines d’autres, notamment des bibliothèques utilisées partout; à chaque fois pour des besoins persos). C’est le meilleur moyen d’apprendre. C’est donc un conseil générique, sans rapport à Python, parce que c’est ce qui a marché pour moi et comme ça que j’ai toujours agi de manière naturelle (sans jamais me forcer à « apprendre coûte que coûte »).
    
8. **Que faudrait-il améliorer ?**
    
    Je ne sais pas trop. C’est pas que Python est parfait, mais je suis plus du genre à m’adapter et à accepter un langage tel qu’il est (tant qu’il n’a pas d’énormes erreurs de conceptions ou de design, bien entendu, mais ce n’est pas le cas de Python).
    
9. **Quels sujets souhaiterais-tu lire dans les prochaines dépêches ?**
    
    Autour de Python, vous voulez dire ? Peu importe, juste des trucs divers intéressants, non? J’apprécie lire les diverses dépêches sur un peu tout et je n’ai pas d’attente en particulier. Ce serait un peu triste si je ne lisais ou ne voulais lire que les trucs que je connais ou qui m’intéressent! Je préfère lire sur des trucs que je connais pas, voire dont je n’ai même pas idée, et donc qui pourraient m’intéresser (mais pour ça faut déjà savoir que ça existe).
    
    Donc  étonnez-moi ! Je connais pas tout et suis ouvert à tout. 🤗

# Entretien avec [**BlueBird75**](https://linuxfr.org/users/blueBird)

![Avatar de BlueBird sur GitHub](https://avatars.githubusercontent.com/u/216653?v=4)

1. **Une petite présentation de ton parcours ?**
    
    J’ai découvert les ordinateurs vers la 5e, en 1987, avec un MSX et son langage de programmation intégré : Microsoft Basic. Le fait de pouvoir donner des instructions à un ordinateur et de le voir les exécuter m’a fasciné. Et me fascine encore.
    
    Au Lycée, je suis passé au PC et à _Borland Turbo Pascal_. En Math Sup, j’ai appris le C et Linux (70 disquettes pour installer une Slackware). Je suis ensuite arrivé dans une école d’ingénieur où les geeks étaient tous fondus de Unix. Si tu parlais pas `shell` et `sed` couramment, tu pouvais difficilement intervenir sur le forum de discussion. Ils programmaient presque tous en _Perl_ avec _Emacs_. J’ai essayé les deux mais ça ne correspondait pas à ma vision de l’informatique : Perl était bien trop enclin à laisser passer des erreurs (langage Write-Only) et Emacs m’a rebuté. J’ai persisté en C et j’ai découvert _Vim_ à la place.
    
    J’ai eu mon diplôme d’ingénieur en télécommunications, mais j’ai rapidement laissé tomber tout ce que j’avais appris en cours pour ne faire que ce que je faisais déjà avant : du développement logiciel ! C’est mon métier et ma passion.
    
2. **Comment as-tu commencé à utiliser Python ? Pourquoi ce langage ?**
    
    Vers les années 2000, Perl était au sommet de sa gloire mais un petit langage commençait à pousser : Python avec sa version 1.5.2 . Puisque Perl m’avait déçu, j’ai voulu voir ce que donnait la concurrence. J’ai immédiatement adoré ce langage qui capturait la bonne manière de programmer : le code est extrêmement lisible, le langage essaie d’être intelligent et quand il doute, il te propose une belle erreur bien claire (par rapport au C++ ou bash que j’utilisais à l’époque par exemple). Et surtout, on est productif rapidement : les structures clés (dictionnaires, listes, tuple, string) sont disponibles immédiatement et de façon très pratiques. Contrairement au C++ où la syntaxe est extrêmement lourde pour obtenir un résultat moins confortable.
    
    Dans mon travail ou pour le logiciel libre, j’ai donc commencé à utiliser discrètement Python.
    
3. **Qu’est ce que tu as trouvé de facile ? As-tu eu des frustrations ?**
    
    Le langage est bien conçu pour le programmeur. A l’époque, n’importe quel développeur C/C++/Java pouvait lire du code Python et le comprendre. Il y a une concision et une clarté qui à mon avis, a permis au langage de décoller. On a un peu perdu cet aspect lisibilité aujourd’hui avec l’ajout de constructions plus complexes dans le langage.
    
    J’ai longtemps été frustré par l’absence de moyen de distribuer facilement du code Python, puis setuptools et pypi.org sont arrivés. Ensuite, programmant sous Windows, j’ai été frustré par la difficulté de livrer une application écrite en Python. Mais py2exe est arrivé et j’ai pu faire des applications pour le bureau de qualité professionnelle, s’intégrant très bien à Windows, sans que personne ne soupçonne que j’utilisais un langage dit de script. J’ai aussi souffert un moment du manque de bibliothèque graphique de qualité, tkinter donnant un look trop passéiste à mon goût aux applications. Puis Phil Thompson a sorti l’excellent binding PyQt et je n’ai plus jamais ralé.
    
    Ces dernières années, j’ai commencé à être frustré par le typage dynamique de Python : dans des grosses applications, on perd vraiment pas mal en compréhension du code et fiabilité. Mais Guido est arrivé avec les annotations de type et mypy pour la vérification et ma vie est redevenue rose.
    
    Avec Python, je suis un développeur comblé. Il rattrape ses faiblesses au fur à mesure des années.
    
4. **Qu’est ce que Python t’apporte ? Comment ferais-tu sans ?**
    
    Mon travail, c’est du développement en C et assembleur pour la carte à puce. Python intervient en tant qu’outil, d’une part pour écrire des tests élaborés, d’autre part, pour résoudre rapidement des problématiques d’automatisation spécifique à notre environnement.
    
    Sans Python, je ferai comme la plupart de mes collègues : j’automatiserai beaucoup moins de tâches et je galèrerai beaucoup plus. Même si en théorie, on pourrait remplacer notre usage de Python par du Visual Basic ou autre, dans les faits, seul les gens qui font du Python semble passer du temps en automatisation. Cela confirme de mon point de vue sa “rentabilité” en terme de temps de développement.
    
5. **Quelle a été ta progression dans la maîtrise de Python ?**
    
    J’aime bien aller au fond des choses, donc assez vite, j’ai acheté un bouquin de référence (merci O'Reilly) pour tout connaitre du langage. C’était plus facile il y a 20 ans, il y avait quand même beaucoup moins de subtilités. J’ai ensuite suivi toutes les évolutions, il n’y a guère que l’API C que je ne suis pas allé voir.
    
    Dans un boulot précédent, l’utilisation de Python couplé à une politique de test intelligente a permis de réduire le temps de test d’un boitier électronique de trois semaines à deux heures. Plus personnes n’a questionné l’utilisation de Python dans mon équipe plutôt que de C#.
    
    Ma plus grande fierté est à venir pour bientôt : je suis en train de pousser mon entreprise à mettre en Open Source un logiciel en Python que j’ai écrit. Une vraie révolution culturelle !
    
6. **Qu’est ce qui te plaît le plus ?**
    
    La lisibilité du code et la facilité à faire des manipulations un peu complexes en quelques lignes. Ça m’arrive souvent de faire des mini-parseur pour des formats textes dans le cadre de tâches d’automatisation. Très vite, je me retrouve avec des listes de dictionnaires de listes de chaînes de caractères et je suis heureux que les structures de bases du langage me permettent ça facilement.
    
    Sur le long terme, j’apprécie la solidité de la communauté Python et le travail de fond qu’a fait Guido Van Rossum pour la construire. Hormis quelques cas où Guido a utilisé son pouvoir de « Dictateur bienveillant », le langage avance avant tout avec un effort communautaire d’entraide. Une licence libre est bien sur essentielle pour ce travail, mais loin d’être suffisant. Faire prospérer une communauté demande un effort important. Par exemple, récemment, un core-développeur du langage a été exclu en raison de sa non coopération et de son agressivité envers ses pairs. C’est un choix difficile à faire, mais essentiel pour garder une communauté saine.
    
    J’apprécie aussi beaucoup les efforts de ces dernières années de la communauté Python pour être plus inclusif, avec un choix délibéré d’avoir
une représentation géographique plus diverses et des initiatives pour faciliter l’accueil de ceux qui ne sont pas des informaticiens masculins blancs.
    
7. **Tes conseils pour les débutants ?**
    
    Je ne suis pas trop en contact avec des débutants, mon public, c’est plutôt les programmeurs intermédiaires ou experts. Mon conseil principal, ne jamais hésiter à refactoriser : renommer pour les rendre le code plus parlant, unifier des traitements, déplacer des traitements dans des fonctions. Tout cela pour un ultime but : rendre du code plus lisible et compréhensible. Une ligne de code va être écrite une fois mais lue des milliers de fois !
    
    Pour du code Python, si le code que vous écrivez fait plus de deux cents lignes, ou est utilisé dans une équipe, ou a une durée de vie de plus d’un mois, ajoutez des annotations de type. Cela le rendra dix fois plus compréhensible. C’est encore mieux si vous vérifier effectivement vos types avec [mypy](https://mypy.readthedocs.io/en/stable/) mais rien que le fait de documenter les types rajoute un gros plus en termes de clarté.
    
    Si vous vous lancez dans la vérification de type avec mypy, commencez modeste. Le démarrage est assez chronophage. Et certains cas complexes demandent de lire pas mal de doc pour pouvoir être décrit avec des types précis. Par contre, le gain est vraiment appréciable !
    
    Pour ceux que ça intéresse, j’ai eu la chance d’en parler [en conférence à PyParis 2018](https://www.youtube.com/watch?v=URP2e7hEUFw&list=PLzjFI0G5nSsry3cm_k1tPOi9SRaAXsZAt&index=7).
    
8. **Que faudrait il améliorer ?**
    
    Il n’y pas assez de développeurs payés pour travailler sur Python lui-même. Victor Stinner parlait d’un développeur et demi au total payé pour travailler dessus alors que le langage est téléchargé des millions de fois par mois ! On sent bien que les exigences d’un projet de la taille de Python demanderaient plus de temps rémunéré ; ça met une grosse pression sur les volontaires (dont plusieurs ont fait des burnouts). Si votre entreprise dépend de Python, faites des dons à la PSF, cela améliorera la situation.
    
    La gestion de paquets Python va aussi bientôt rencontrer un gros écueil sur la gestion des dépendances. Le nombre de paquets et de dépendances augmente rapidement, et on va tomber de plus en plus souvent sur le cas où une application dépend de deux packages A et B, qui, chacun, dépendent d’une version différente du package C. Des évolutions récentes sur pip permettent de mieux gérer le cas  où il existe une version du package C qui résoud toutes les contraintes. Mais à terme, je pense qu’il faudra trouver une solution pour que les package A et B puissent chacun utiliser la version du package C qui leur convient. Ça va pas être trivial !
    
9. **Quels sujets souhaiterais-tu lire dans les prochaines dépêches ?**
    
    J’aime beaucoup les retours d’expérience professionnelle. Surtout si c’est atypique !
