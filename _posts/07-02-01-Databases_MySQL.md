---
isChild: true
title:   Extension MySQL
anchor:  mysql_extension
---

## Extension MySQL {#mysql_extension_title}

L'extension [mysql] pour PHP est aujourd'hui au point mort et est [officiellement dépréciée depuis PHP 5.5.0](http://php.net/manual/fr/migration55.deprecated.php) ce qui
signifie qu'elle sera retirée dans les prochaines versions. Si vous utilisez n'importe quelle fonction commençant par
`mysql_*` (comme `mysql_connect()`) dans votre application alors cela donnera des erreurs dans votre code. Vous serez
donc obligé de faire la transition vers [mysqli] ou [PDO].

**Si vous venez de commencer votre projet alors n'utilisez surtout pas l'extension [mysql] mais préférez [mysqli] ou PDO**

* [PHP: Choisir une API pour MySQL](http://php.net/manual/fr/mysqlinfo.api.choosing.php)
* [Tutoriel sur PDO pour les développeurs MySQL](http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers)

[PDO]: http://php.net/pdo
[mysql]: http://php.net/mysql
[mysqli]: http://php.net/mysqli
