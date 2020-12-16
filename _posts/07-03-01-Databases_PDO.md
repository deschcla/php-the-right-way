---
isChild: true
title:   Extension PDO
anchor:  pdo_extension
---

## Extension PDO {#pdo_extension_title}

PDO est une couche d'abstraction pour se connecter à une base de données &mdash; intégrée à PHP depuis la version 5.1.0 &mdash;
qui fournit une interface commune pour communiquer avec différentes bases de données. PDO ne va pas traduire vos requêtes
SQL ou émuler les fonctionnalités manquantes; il ne gère que la connexion entre différents types de bases de données avec
la même API.

Plus important encore, PDO vous permet d'injecter en toute sécurité des entrées étrangères (par ex., les identifiants)
dans vos requêtes SQL sans que vous ayez à vous soucier des attaques par injection SQL. Cela est rendu possible grâce à
l'utilisation des fonctions de PDO et des paramètres liés.

Supposons qu'un script PHP reçoit un identifiant numérique en tant que paramètre d'entrée. Cet ID devrait être utilisé
pour récupérer les enregistrements d'un utilisateur dans la base de données. Voici la mauvaise façon de s'y prendre :

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NON!
{% endhighlight %}

Ce code est mauvais. Vous insérez un paramètre en brut directement dans une requête SQL. C'est la porte ouverte pour
le piratage comme [l'injection SQL](http://wiki.hashphp.org/Validation). Imaginez un instant que si un pirate envoie un paramètre `id` en invoquant l'URL
`http://domain.com/?id=1%3BDELETE+FROM+users`. Cela va définir la variable `$_GET['id']` à `1;DELETE FROM users` ce qui
va effacer l'ensemble de vos utilisateurs ! Au lieu de faire ça, vous devriez nettoyer les entrées en utilisant la liaison
des paramètres avec PDO.

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); // <-- Nettoyé automatiquement par PDO
$stmt->execute();
{% endhighlight %}

Voici le code correct. Il utilise un paramètre lié à une expression PDO. Cela "échappe" les entrées étrangères avant
qu'elles ne soient introduites dans la base de données, ce qui empêche les attaques potentielles par injection SQL.

* [En savoir plus sur PDO][1]

Vous devriez savoir que les connexions à la base de données utilisent pas mal de ressources et il arrivait souvent
que les ressources finissaient par tarir si les connexions n'étaient pas implicitement fermées. Cependant c'était plus
souvent le cas dans les autres langages. En utilisant PDO, vous pouvez implicitement fermer la connexion en détruisant
l'objet et en s'assurant que toutes les références à cet objet ont été supprimées, c'est-à-dire, mises à NULL. Si vous
ne le faites pas explicitement, PHP va automatiquement fermer la connexion quand votre script s'arrêtera - à moins bien
sûr que vous n'utilisiez une connexion persistante.

* [En savoir plus sur les connexions avec PDO][5]

## Couches d'abstractions

Beaucoup de frameworks fournissent leur propre couche d'abstraction qui peut être ou non basée sur PDO. Cette couche va
souvent émuler les fonctionnalités d'une base de données qui seraient manquantes dans une autre base en enveloppant
vos requêtes dans des méthodes PHP vous donnant ainsi une réelle abstraction avec la base de données.
Cela engendre évidemment un léger surplus mais si vous voulez développer une application portable ayant besoin de
communiquer avec MySQL, PostgreSQL et SQLite alors ce petit surplus en vaudra la peine par souci de propreté et de
maintenance du code.

Plusieurs couches d'abstractions ont été construites en utilisant les standards d'espace de noms [PSR-0][psr0] ou
[PSR-4][psr4]; elles peuvent donc être installées dans n'importe quelle application qui vous plaira :

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [ZF2 Db][4]
* [ZF1 Db][3]

[1]: http://www.php.net/manual/fr/book.pdo.php
[2]: http://www.doctrine-project.org/projects/dbal.html
[3]: http://framework.zend.com/manual/fr/zend.db.html
[4]: http://packages.zendframework.com/docs/latest/manual/fr/index.html#zend-db
[5]: http://php.net/manual/fr/pdo.connections.php
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/Propel/

[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
