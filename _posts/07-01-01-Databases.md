---
title:  Bases de données
anchor: databases
---

# Bases de données {#databases_title}

Votre code PHP va souvent faire appel aux bases de données pour préserver l'information. Vous avez un certain nombre 
d'options pour vous connecter et interagir avec votre base de données. L'option recommandée _avant PHP 5.1.0_ était 
d'utiliser les pilotes natifs tels que [mysql][mysql], [mysqli][mysqli], [pgsql][pgsql], etc.

Les pilotes natifs sont géniaux si vous n'utilisez qu'un seul type de base de données dans votre application mais si, 
par exemple, vous utilisez MySQL et un peu de MSSQL, ou vous avez besoin de vous connecter à une base Oracle alors vous 
ne pourrez pas utiliser les mêmes pilotes. Vous aurez besoin d'apprendre une nouvelle API pour chaque type de BDD &mdash; ce 
qui peut devenir lourd.

[mysql]: http://php.net/mysql
[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
