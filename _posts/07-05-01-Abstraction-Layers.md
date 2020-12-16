---
isChild: true
title:   Couches d'abstraction
anchor:  databases_abstraction_layers
---

## Couches d'abstraction {#databases_abstraction_layers_title}

Pratiquement tous les frameworks contiennent leurs propres couches d'abstraction qui peut ou non se baser sur [PDO][1]. Il simule la plupart du temps les caractéristiques manquantes d'un système à l'autre en englobant vos requêtes dans des méthodes PHP vous donnant une réelle abstraction des données contrairement à PDO qui ne vous fournit que la partie connexion.
Cela rajoute évidemment une surcouche mais si vous devez construire une application portable qui nécessite de travailler à la fois avec MySQL, PostgreSQL et/ou SQLite alors ce petit surplus ne sera pas de trop afin d'avoir un code plus maintenable.

Certains couches d'abstraction ont été construites en utilisant la norme [PSR-0][psr0] ou [PSR-4][psr4] afin d'être utilisable par n'importe quelle application:

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [Zend-db][4]


[1]: http://php.net/book.pdo
[2]: http://www.doctrine-project.org/projects/dbal.html
[4]: https://packages.zendframework.com/docs/latest/manual/en/index.html#zendframework/zend-db
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/
[psr0]: http://www.php-fig.org/psr/psr-0/
[psr4]: http://www.php-fig.org/psr/psr-4/
