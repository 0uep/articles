# Articles LinuxFr.org

🇫🇷 L’ambition de ce dépôt Git est permettre à tous les contributeurs de LinuxFr.org de stocker ici tous les fichiers associés à leurs dépêches et journaux : images, animations, musiques, vidéos et tout autres fichiers. Idéalement, avec la dernière version des articles.

🇬🇧 This Git repo aims to allow all LinuxFr.org contributors to store all the files associated to their articles: images, animations, musics, videos and any other files. Ideally, with the last version of the related articles.

```
sudo apt install git git-lfs   # Debian / Ubuntu
git clone https://github.com/linuxfrorg/articles
```

## Textes & images

### 🇫🇷 Tous les fichiers des articles LinuxFr.org

L’espace de rédaction de LinuxFr.org permet un travail collaboratif.
Néanmoins, ce n’est pas le cas des illustrations qui ne sont pas hébergées sur LinuxFr.org.
Et il n’est pas rare que des dépêches se retrouvent avec des liens cassés au bout de quelques années. 😟

Ce dépôt Git a donc un double objectif :
- espace collaboratif pour les images (et autres fichiers média) ;
- meilleure pérennité des fichiers associés aux dépêches.

### 🇬🇧 All the LinuxFr.org articles files

LinuxFr.org has a collaborative space allowing multiple contributors to write together new articles.
However, this only concerns the text: Illustration is missing collaborative autoring tools, and even hosting!
Unfortunately, some articles end up with broken links after a few years. 😟

Therefore, this Git repo has a double purpose:

* collaborative space for images (and other media files)
* better durability of the files associated to the LinuxFr.org articles

## Git LFS (Large File Storage)

### 🇫🇷 Illimité

Un dépôt Git peut contenir tout l’historique d’un projet très actif sur de nombreuses années et nécessiter peu d’espace de stockage.
Par contre, cela ne fonctionne qu’avec des fichiers *texte* : le code source.

Les images et autres illustrations sont bien souvent des fichiers volumineux et au format *binaire* qui les rendent peu compatibles avec la philosophie Git, surtout quand ces fichiers sont souvent modifiés.

Nous expérimentons la fonctionnalité LFS afin de pouvoir cloner ce dépôt Git avec tout l’historique tout en évitant de devoir stocker en local toutes les révisions de chaque fichier ce qui pourrait consommer beaucoup d’espace de stockage. D’autres alternatives pourraient être envisagées, comme la suppression des 
anciennes révisions de chaque fichier binaire volumineux, ou le fait de cloner avec seulement la dernière révision de chaque fichier.

Si des fichiers très volumineux sont stockés, comme un court métrage avec ses *rushs* en haute résolution (beaucoup de To), nous pouvons imaginer l’utilisation des branches, afin de contenir l’espace nécessaire au clonage de ce dépôt Git. Une autre alternative seraient la création d’autant de dépôts Git que d’articles utilisant des fichiers aussi volumineux. On avisera le moment venu…

### 🇬🇧 Unlimited

A Git repository can contain the entire history of a very active project over many years and still require little storage space. However, this only works with *text* files: the source code.

Images and other illustrations are often large files in binary format which makes them not very compatible with the Git philosophy, especially when these files are often modified.

We are experimenting with the LFS feature in order to be able to clone this Git repository with all the history while avoiding having to store locally all the revisions of each file which could consume a lot of storage space. Other alternatives could be considered, such as deleting the old revisions of each large binary file, or cloning with only the latest revision of each file.

If very large files are stored, like a movie with high resolution rushes (many TB), we can imagine using branches, to contain the space needed to clone this Git repository. Another alternative would be the creation of as many Git repositories as topics using such large files. We will advise when the time comes…

## Original & export

### 🇫🇷 Pensez à archiver les originaux

Idéalement, les différents fichiers et les scripts ayant permis la réalisation des illustrations finales devraient aussi être archivés. La présence de différentes ébauches est également possible. Nous acceptons même l’export dans différents formats.

### 🇬🇧 Also archive the originals

Ideally, the different files and scripts that allowed the realization of the final illustrations should also be archived. The presence of different drafts is also possible. We even accept export in different formats.

## Licence

### 🇫🇷 Toute licence acceptée

La licence des fichiers illustrant les dépêches (et journaux) LinuxFr.org ne sont pas toujours connus.
Bien que nous soyons amoureux des licences libres, nous restons pragmatiques et acceptons des fichiers dont l’origine a été oubliée…
Néanmoins, quand cela est possible, merci de fournir la licence de chaque sous-élement qui compose le fichier final.

### 🇬🇧 Any licence accepted

The license of the files illustrating the LinuxFr.org articles are not always known.
Although we are in love with free licences, we remain pragmatic and accept files whose origin has been forgotten…
Nevertheless, when it is possible, please provide the licence of each sub-element that composes the final file.
