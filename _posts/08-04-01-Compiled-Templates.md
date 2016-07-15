---
title:   Templates compilés
isChild: true
anchor:  compiled_templates
---

## Templates compilés {#compiled_templates_title}

Bien que le PHP ait évolué en un langage orienté objet mature, il ne s'est 
[pas énormément amélioré](http://fabien.potencier.org/article/34/templating-engines-in-php) en tant que langage de 
templating. Les templates compilés comme [Twig](http://twig.sensiolabs.org/) ou [Smarty](http://www.smarty.net/) 
remplissent ce vide en offrant une nouvelle syntaxe, adaptée aux exigences des applications modernes. Cela va de 
l'échappement automatique à l'héritage en passant par des structures de contrôles simplifiées. Ces templates ont été 
conçus dans l'idée de faciliter l'écriture, la sécurité et la maintenance du code gérant la partie visuelle de l'application. 
Les templates compilés peuvent même être partagés entre différents langages, [Mustache](http://mustache.github.io/) étant 
un bon exemple de cela. Étant donné que ces templates doivent être compilés, il y a une légère baisse de performances. 
Cependant, cela peut être anecdotique si un système de cache approprié est utilisé.

Exemple d'un template compilé (utilisant [Twig](http://twig.sensiolabs.org/)):

{% highlight text %}
{% raw %}
{% include 'header.html' with {'title': 'Profil utilisateur'} %}

<h1>Profil utilisateur</h1>
<p>Bonjour, {{ name }}</p>

{% include 'footer.html' %}
{% endraw %}
{% endhighlight %}
