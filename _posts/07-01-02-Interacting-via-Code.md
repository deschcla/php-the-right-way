---
isChild: true
title: Interagir avec les bases de données
---

## Interagir avec les bases de données

Quand les développeurs commencent à utiliser PHP, ils finissent souvent par mélanger le code métier avec celui gérant 
la base de données et l'affichage ce qui donne quelque chose de ce genre là :

{% highlight php %}
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
</ul>
{% endhighlight %}

Ceci est une mauvaise pratique pour toutes sortes de raisons, principalement du au fait qu'il est plus difficile à 
déboguer, plus dur pour le lire et pour réaliser des tests.

Bien qu'il existe un certain nombre de solutions pour parer à ce problème comme l'utilisation de la [POO](/#object-oriented-programming) 
ou bien la [programmation fonctionnelle](/#functional-programming), les parties logiques de votre code doivent être 
clairement délimités.

Considérez l'exemple suivant :

{% highlight php %}
<?php
function getAllSomethings($db) {
    return $db->query('SELECT * FROM table');
}

foreach (getAllFoos() as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // MAUVAIS!!
}
{% endhighlight %}

C'est un bon début. La séparation entre l'interaction avec la base de données et l'affichage est déjà bien distincts.

Créez une classe où vous placerez les méthodes de votre code métier (votre "modèle"). Puis créez un fichier `.php` 
qui contient la logique d'affichage (votre "vue") ce qui revient grosso-modo à utiliser le pattern MVC] - un modèle 
d'architecture très courant dans la plupart des [frameworks](/#frameworks_title).

**foo.php**

{% highlight php %}
<?php

$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8', 'username', 'password');

// Rendre votre modèle accessible
include 'models/FooModel.php';

// Création d'une instance
$fooList = new FooModel($db);

// Affichage du résultat
include 'views/foo-list.php';
{% endhighlight %}


**models/FooModel.php**

{% highlight php %}
<?php
class Foo()
{
    protected $db;

    public function __construct(PDO $db)
    {
        $this->db = $db;
    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
{% endhighlight %}

**views/foo-list.php**

{% highlight php %}
<? foreach ($fooList as $row): ?>
    <?= $row['field1'] ?> - <?= $row['field1'] ?>
<? endforeach ?>
{% endhighlight %}

C'est l'essentiel de ce que font les frameworks de façon plus manuelle. Vous n'avez pas forcément besoin de l'utiliser 
constamment mais mélanger la présentation et la logique métier peut être un réel casse-tête si vous devez ensuite 
utiliser les [tests unitaires](/#unit-testing) dans votre application.

[PHPBridge] contient un excellent tutoriel appellé [Creating a Data Class] qui couvre un sujet similaire à celui-ci et 
permet de bien s'imprégner du concept d'interaction avec les bases de données.

[MVC]: http://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488 (en)
[PHPBridge]: http://phpbridge.org/ (en)
[Creating a Data Class]: http://phpbridge.org/intro-to-php/creating_a_data_class (en)
