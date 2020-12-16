---
title:   Bénéfices
isChild: true
anchor:  templating_benefits
---

## Bénéfices {#templating_benefits_title}

L'intérêt principal d'utiliser les templates tient dans la séparation nette qui se créée entre la logique de présentation
et le reste de l'application. Les templates sont seuls responsables de l'affichage du contenu formaté. Ils ne sont pas
responsables de la récupération des données, ni de la persistance ou d'autres tâches complexes. Cela conduit à du code
plus propre et plus lisible, ce qui est particulièrement utile lorsque l'on travaille en équipe où l'on peut trouver
à la fois des développeurs côté serveur (responsables de la partie "contrôleurs, modèles") et les designers qui, eux,
travaillent sur le code côté client.

Les templates améliorent aussi l'organisation du code pour l'affichage. Ils sont généralement placés dans un répertoire
"views", chacun étant défini dans un seul fichier. Cette approche encourage la réutilisation de code où de larges blocs
de code sont découpés de façon à obtenir un ensemble de briques "atomiques" et utilisables plus facilement. Par exemple,
l'en-tête et le pied de page de votre site peuvent être définis dans des templates qui seront par la suite inclus
respectivement au début et à la fin de chaque template d'une page.

Finalement, selon la bibliothèque que vous utilisez, les templates peuvent vous offrir plus de sécurité en échappant
par exemple automatiquement les variables définis par les entrées d'un utilisateur. Quelques bibliothèques vous offrent
même la possibilité d'isoler les variables et les fonctions (on parlera de _sandboxing_) définis dans une liste blanche
de façon, par exemple, à limiter les dégats collatéraux provoqués par une mauvaise utilisation faites par les designers.
