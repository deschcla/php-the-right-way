---
title:   Installation sous Mac
isChild: true
anchor:  mac_setup
---

## Installation sous Mac  {#mac_setup_title}

Le système d'exploitation OSX contient une version précompilée de PHP mais est généralement en retard sur la dernière 
version stable. Yosemite contient la version 5.5.9, El Capitan 5.5.29, Sierra 5.6.24. Il est à noter que High Sierra possède la dernière version majeure de PHP, plus précisement la version 7.1.6.  

### Installation via un gestionnaire de paquets

Pour mettre à jour la version de PHP sur OSX vous pouvez passer via 
de nombreux [gestionnaire de paquets][mac-package-managers], [php-osx de Liip][php-osx-downloads] étant recommandé.

### Installation depuis la source

L'autre option est de le [compiler soi-même][mac-compile]. Dans ce cas, faites attention à ce que l'IDE Xcode soit 
 installé ou bien son [substitut en ligne de commande][apple-developer] téléchargeable 
sur le Mac Developer Center d'Apple.

### Installation "Tout-en-un"

Pour une installation "tout-en-un" incluant PHP, le serveur web Apache et la base de données MySQL, le tout contrôlé 
par une jolie interface graphique, essayez [MAMP][mamp-downloads] ou [XAMPP][xampp].

[mac-package-managers]: http://www.php.net/manual/fr/install.macosx.packages.php
[mac-compile]: http://www.php.net/manual/fr/install.macosx.compile.php
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
[apple-developer]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/index.html
[php-osx-downloads]: http://php-osx.liip.ch/
[xampp]: http://www.apachefriends.org/fr/index.html
