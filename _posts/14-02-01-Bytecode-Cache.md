---
title:   Cache du bytecode
isChild: true
anchor:  bytecode_caching
---

## Cache du bytecode {#bytecode_caching_title}

Quand un fichier PHP est exécuté, il est d'abord compilé sous forme de bytecode (aussi connu sous le nom d'opcode)
puis ce bytecode est ensuite exécuté.
Si le fichier PHP n'est pas modifié, le bytecode restera toujours le même ce qui signifie que sa compilation lors de
chaque appel sera une perte de ressources CPU.

C'est là que le cache du bytecode intervient. Il empêche la compilation récurrente en stockant le bytecode en mémoire
et en le ré-utilisant à chaque appel successif. Mettre en place le cache ne prend que quelques minutes mais cela
augmentera de façon significative la réactivité de votre application. Il n'y a donc aucune raison de ne pas l'utiliser.

Avec PHP 5.5, il existe un cache intégré pour le bytecode appelé [OPcache](http://php.net/manual/fr/book.opcache.php).
Il est aussi disponible pour les versions précédentes.

Les autres caches pour bytecode sont:

* [APC](http://php.net/manual/fr/book.apc.php) (PHP 5.4 et antérieur)
* [XCache](http://xcache.lighttpd.net/)
* [Zend Optimizer+](http://www.zend.com/products/server/) (fait parti de Zend Server)
* [WinCache](http://www.iis.net/download/wincacheforphp) (extension pour MS Windows Server)
