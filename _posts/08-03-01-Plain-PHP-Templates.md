---
title: Templates en PHP pur
isChild: true
---

## Templates en PHP "pur" {#templates_en_php_pur_title}

Les templates "pur" PHP sont ceux qui n'utilisent que du code PHP natif. C'est un choix naturel étant donné que PHP est 
lui-même un language de templating. Ce terme signifie tout simplement que vous pouvez combiner du code PHP avec un autre 
langage comme l'HTML. Cela peut être considéré comme un atout du fait même que les développeurs n'ont pas à apprendre 
une syntaxe particulière. Par ailleurs, ces templates tendent à être plus rapide étant donné qu'il n'y a pas de phase de 
compilation.

Tous les frameworks PHP modernes utilisent un système de templating, la plupart se basant uniquement sur la syntaxe PHP. 
En dehors des frameworks, des bibliothèques comme [Plates](http://platesphp.com/) ou [Aura.View](https://github.com/auraphp/Aura.View) 
rendent le travail avec les templates en PHP "pur" plus facile en offrant des fonctionnalités "modernes" telles que 
l'héritage, le layout et des extensions.

Exemple d'un template en PHP "pur" (utilisant [Plates](http://platesphp.com/)):

{% highlight php %}
<?php $this->insert('header', ['title' => 'Profil utilisateur']) ?>

<h1>Profil utilisateur</h1>
<p>Bonjour, <?=$this->escape($name)?></p>

<?php $this->insert('footer') ?>
{% endhighlight %}
