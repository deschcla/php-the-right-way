---
title:   Installation sous Windows
isChild: true
anchor:  windows_setup
---

## Installation sous Windows {#windows_setup_title}

PHP est disponible sous Windows de plusieurs façons. Vous pouvez [télécharger les binaires][php-downloads] et jusqu'à récemment, vous pouviez utiliser un installateur '.msi'.
Cependant il n'est plus maintenu depuis la version 5.3.0.

Pour l'apprentissage et le développement en local, vous pouvez dorénavant utiliser le serveur intégré à PHP 8.0+, ainsi
vous n'aurez plus à vous soucier de la configuration du serveur web. Si vous souhaitez un système "tout-en-un" incluant
un serveur web et MySQL alors des outils tels que [WPI][wpi], [Zend Server CE][zsce], [XAMPP][xampp] ou encore
[WAMP][wamp] vous permettront d'avoir un environnement de développement complet rapidement. Ceci étant dit, ces
outils sont différents de ce que l'on trouve en production donc faites attention sur les différences d'environnement si
vous travaillez sur Windows et déployez sur Linux.

Si vous désirez utiliser Windows comme plateforme de production alors le serveur IIS vous donnera le meilleur compromis
entre stabilité et performance. Vous pouvez utiliser [phpmanager][phpmanager] qui est un plugin graphique pour IIS
afin d'effectuer les configurations nécessaires pour faire tourner PHP. IIS intègre FastCGI prêt à l'emploi, vous
n'avez qu'à configurer PHP en tant qu'extension. Pour plus d'informations, visitez le site dédié sur [iis.net][php-iis].

Généralement, faire tourner une application sur différents environnement de développement peut conduire à des comportements étranges ce qui peut être hasardeux une fois déployé en production.
Si vous développez sous Windows mais que vos machines de production tournent sous Linux, vous feriez mieux de considérer l'utilisation de [machines virtuelles](/#virtualization_title).

Il existe toutefois un excellent article en anglais écrit par Chris Tankersley sur les [outils à utiliser][windows-tools] si vous souhaitez travailler sous Windows.

[php-downloads]: http://windows.php.net
[phpmanager]: http://phpmanager.codeplex.com/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[zsce]: http://www.zend.com/fr/products/server/free-edition
[xampp]: https://www.apachefriends.org/fr/index.html
[wamp]: http://www.wampserver.com/
[php-iis]: http://php.iis.net/
[windows-tools]: http://ctankersley.com/2016/11/13/developing-on-windows-2016/
