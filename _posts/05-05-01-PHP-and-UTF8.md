---
title:   Travailler avec de l'UTF-8
isChild: true
anchor:  php_and_utf8
---

## Travailler avec de l'UTF-8 {#php_and_utf8_title}

_Cette section a été traduite à partir de la page d'[Alex Cabal](https://alexcabal.com/) sur les
[meilleures pratiques PHP](https://phpbestpractices.org/#utf-8) et sert de base pour vous donner des conseils sur
l'utilisation de l'UTF-8_.

### Il n'y a pas de recette magique. Faites attention, soyez consciencieux et cohérent.

Jusqu'à présent PHP n'inclut pas de support bas niveau pour l'unicode. Il existe des moyens de s'assurer que les chaînes
de caractères encodées en UTF-8 seront traitées correctement mais cela n'est pas facile et demande une attention particulière
tout le long de la chaîne de traitement, allant de la page HTML à vos requêtes SQL en passant par le PHP. Les prochains
paragraphes vont tenter de vous résumer la bonne approche à adopter face à du contenu Unicode.

### UTF-8 au niveau de PHP

Les opérations basiques sur les chaînes de caractères comme la concaténation ou l'affectation de chaînes à des variables
ne demandent rien de particulier en ce qui concerne l'UTF-8. En revanche, la plupart des fonctions manipulant les chaînes
comme `strpos()` et `strlen()` ont besoin d'une attention particulière. Ces fonctions ont en effet souvent leur contre-partie
`mb_*` comme `mb_strpos()` et `mb_strlen()`. Ces fonctions `mb_*` proviennent de
l'[extension pour les chaînes de caractères multi-octets] et ont été conçus spécialement pour les chaînes Unicode.

Vous devez utiliser les fonctions `mb_*` à chaque fois que vous manipulez une chaîne de caractère Unicode. Par exemple,
si vous utilisez `substr()` sur une chaîne UTF-8, il y a de forte chance pour que le résultat contienne des caractères
à moitié tronqués. La fonction correcte dans ce genre de cas serait d'utiliser `mb_substr()`.

La difficulté réside dans le fait de se souvenir à chaque fois d'utiliser les fonctions `mb_*` quand c'est nécessaire.
Si jamais vous l'oubliez ne serait-ce qu'une seule fois alors votre chaîne Unicode aura de grande chance d'être incompréhensible
en sortie de traitement.

Les fonctions traitant les chaînes n'ont pas toutes leur équivalent `mb_*`. S'il y en a une qui est dans ce cas alors
vous n'avez pas de chance.

Vous devriez utiliser la fonction `mb_internal_encoding()` en haut de tout vos scripts PHP (ou en haut d'un fichier d'en-tête
global) et la fonction `mb_http_output()` juste après si vous devez afficher du texte en sortie. Définir explicitement
l'encodage de caractère de vos chaînes vous simplifiera énormement la vie.

Par ailleurs, beaucoup de fonctions PHP opérant sur les chaînes ont un paramètre optionnel vous permettant de spécifier
l'encodage de caractère. Vous devriez alors toujours indiquer explicitement que vous utilisez de l'UTF-8. Par exemple,
la fonction `htmlentities()` possède une option pour l'encodage des caractères. Notez que depuis PHP 5.4.0, l'UTF-8 est
l'encodage par défaut pour `htmlentities()` et `htmlspecialchars()`.

Au final, si vous développez et déployez une application utilisant l'UTF-8 sans être certain que l'extension `mbstring`
sera présente, pensez alors à utiliser des alternatives comme le package Composer [patchwork/utf8]. Il utilisera `mbstring`
si jamais il le trouve sinon il utilisera les fonctions non-UTF8.

[extension pour les chaînes de caractères multi-octets]: http://php.net/manual/fr/book.mbstring.php
[patchwork/utf8]: https://packagist.org/packages/patchwork/utf8 (en)

### UTF-8 au niveau de la base de données

Si votre script PHP a accès à MySQL, il y a une forte chance que vos chaînes de caractères soient stockées en tant que chaînes
non-UTF8 même si vous suivez les précautions vues plus haut.

Pour vous assurer que vos chaînes aillent de PHP vers MySQL en UTF-8, vérifiez que votre base de données et les tables
qu'elle contient sont toutes enregistrées avec l'encodage de caractères et la collation `utf8mb4` et que votre connexion
PDO soit aussi mise sur cet encodage. Voir l'exemple plus bas. Ceci est _extrêmement important_.

Notez que pour utiliser le support complet pour UTF-8, vous devez utiliser l'encodage de caractères `utf8mb4` et non
`utf8` ! Voir les détails plus loin pour comprendre pourquoi.

### UTF-8 au niveau du navigateur web

Utilisez la fonction `mb_http_output()` pour vous assurer que votre script PHP affichera du texte en UTF-8 dans votre
navigateur.

Le navigateur devra ensuite être averti par le biais de la réponse HTTP que cette page est encodée en UTF-8. L'approche
historique pour faire cela était d'inclure le [tag `<meta>`](http://htmlpurifier.org/docs/enduser-utf8.html) dans le tag
`<head>`. Cette approche est parfaitement valide mais indiquer l'encodage directement dans l'en-tête HTTP `Content-Type`
est en fait [plus rapide](https://developers.google.com/speed/docs/best-practices/rendering#SpecifyCharsetEarly).

{% highlight php %}
<?php
// Indique à PHP que nous allons effectivement manipuler du texte UTF-8
mb_internal_encoding('UTF-8');

// indique à PHP que nous allons afficher du texte UTF-8 dans le navigateur web
mb_http_output('UTF-8');

// Notre chaîne UTF-8 de test
$string = 'Êl síla erin lû e-govaned vîn.';

// Découpe une sous partie de la chaîne à l'aide d'une fonction multi-octet
// Notez que la découpe se fait au niveau d'un caractère non-ascii pour la démonstration
$string = mb_substr($string, 0, 15);

// Connexion à une base de données pour stocker la chaîne transformée
// Voir les exemples d'utilisation de PDO dans ce document
// Notez la commande `set names utf8mb4`
$link = new \PDO(
                    'mysql:host=your-hostname;dbname=your-db;charset=utf8mb4',
                    'your-username',
                    'your-password',
                    array(
                        \PDO::ATTR_ERRMODE => \PDO::ERRMODE_EXCEPTION,
                        \PDO::ATTR_PERSISTENT => false
                    )
                );

// Stocke notre chaîne en tant que chaîne UTF-8 dans la base de données
// Votre base ainsi que ses tables doivent être encodées avec utf8mb4 (character set et collation).
$handle = $link->prepare('insert into ElvishSentences (Id, Body) values (?, ?)');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->bindValue(2, $string);
$handle->execute();

// Récupère la chaîne que l'on vient juste de stocker pour prouver qu'elle a été correctement stockée
$handle = $link->prepare('select * from ElvishSentences where Id = ?');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->execute();

// stocke le résultat dans un objet que l'on affichera dans notre HTML
$result = $handle->fetchAll(\PDO::FETCH_OBJ);

header('Content-Type: text/html; charset=utf-8');
?><!doctype html>
<html>
    <head>
        <title>page de test UTF-8</title>
    </head>
    <body>
        <?php
        foreach($result as $row){
            print($row->Body);  // Cela devrait correctement afficher notre contenu en UTF-8
        }
        ?>
    </body>
</html>
{% endhighlight %}

### Pour aller plus loin

* [Manuel PHP: Opérations sur les chaînes de caractères](http://php.net/manual/fr/language.operators.string.php)
* [Manuel PHP: Fonctions sur les chaînes de caractères](http://php.net/manual/fr/ref.strings.php)
    * [`strpos()`](http://php.net/manual/fr/function.strpos.php)
    * [`strlen()`](http://php.net/manual/fr/function.strlen.php)
    * [`substr()`](http://php.net/manual/fr/function.substr.php)
* [Manuel PHP: Fonctions sur les chaînes multi-octets](http://php.net/manual/fr/ref.mbstring.php)
    * [`mb_strpos()`](http://php.net/manual/fr/function.mb-strpos.php)
    * [`mb_strlen()`](http://php.net/manual/fr/function.mb-strlen.php)
    * [`mb_substr()`](http://php.net/manual/fr/function.mb-substr.php)
    * [`mb_internal_encoding()`](http://php.net/manual/fr/function.mb-internal-encoding.php)
    * [`mb_http_output()`](http://php.net/manual/fr/function.mb-http-output.php)
    * [`htmlentities()`](http://php.net/manual/fr/function.htmlentities.php)
    * [`htmlspecialchars()`](http://www.php.net/manual/fr/function.htmlspecialchars.php)
* [PHP UTF-8 Cheatsheet](http://blog.loftdigital.com/blog/php-utf-8-cheatsheet)(en)
* [Stack Overflow: What factors make PHP Unicode-incompatible?](http://stackoverflow.com/questions/571694/what-factors-make-php-unicode-incompatible)(en)
* [Stack Overflow: Best practices in PHP and MySQL with international strings](http://stackoverflow.com/questions/140728/best-practices-in-php-and-mysql-with-international-strings)(en)
* [How to support full Unicode in MySQL databases](http://mathiasbynens.be/notes/mysql-utf8mb4)(en)
* [Bringing Unicode to PHP with Portable UTF-8](http://www.sitepoint.com/bringing-unicode-to-php-with-portable-utf8/)(en)
