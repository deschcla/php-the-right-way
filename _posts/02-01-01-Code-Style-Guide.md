---
title:  Normes
anchor: code_style_guide
---

# Normes  {#code_style_guide_title}

La communauté PHP est large et diverse, composée d'innombrables bibliothèques, de frameworks et de composants. Il est
courant pour les développeurs PHP de choisir plusieurs d'entre eux et de les combiner en un seul projet. Il est important
que le code PHP adhère (de façon aussi proche que possible) à un style commun pour rendre le partage plus facile
entre développeurs et de garder une certaine cohérence avec l'utilisation de code tiers.

Le [Framework Interop Group][fig] a proposé et approuvé une série de conventions de codage. Celles qui sont liées aux
conventions d'écriture sont le [PSR-0][psr0], le [PSR-1][psr1], le [PSR-2][psr2] et le [PSR-4][psr4]. Ces recommandations sont
un ensemble de règles que certains projets ont adoptées comme Drupal, Zend, Symfony, Laravel, CakePHP, phpBB, AWS SDK,
FuelPHP, Lithium, etc. Vous pouvez les utiliser dans vos projets ou bien la vôtre si vous en avez une.

Idéalement, vous devriez écrire du code PHP qui adhère à des standards connus. Cela peut être une combinaison des PSR ou
un des standards créés par PEAR ou Zend.

* [En savoir plus sur PSR-0][psr0]
* [En savoir plus sur PSR-1][psr1]
* [En savoir plus sur PSR-2][psr2]
* [En savoir plus sur PSR-4][psr4]
* [Lire les conventions de codage de PEAR][pear-cs]
* [Lire les conventions de codage de Zend][zend-cs]
* [Lire les conventions de codage de Symfony][symfony-cs]

Vous pouvez utiliser [PHP_CodeSniffer][phpcs] pour vérifier que votre code respecte une de ces recommandations. Des
plugins pour des éditeurs de texte comme [Sublime Text 2][st-cs] vous permettent d'avoir un aperçu des écarts en temps réel.

Utiliser le [PHP Coding Standards Fixer][phpcsfixer] de Fabien Potencier afin de formatter automatiquement la syntaxe de
votre code selon les standards définis, ce qui vous évite de le faire vous-même à la main.

Faites en sorte que l'infrastructure de votre code et que les noms des variables choisis soient en anglais. Les
commentaires peuvent être écrits dans n'importe quelle langue du moment que l'ensemble des personnes ayant à travailler
dessus puissent les comprendre.

[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[zend-cs]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
