---
title:  La gestion des dépendances
anchor: dependency_management
---

# La gestion des dépendances {#dependency_management_title}

Il existe une tonne de bibliothèques PHP, de frameworks et de composants pour gérer les dépendances. Votre projet va 
sûrement utiliser plusieurs d'entre eux — ce sont les dépendances d'un projet. Jusqu'à récemment, le PHP n'avait pas de 
moyen fiable pour gérer ces dépendances : même si vous les gériez de façon manuelle, vous deviez toujours vous 
inquiéter des autoloaders. Mais plus maintenant.

À l'heure actuelle, il existe deux gestionnaires de packaging pour PHP - Composer et PEAR. Lequel correspond le mieux à 
vos attentes ? Cela dépend de la taille de votre projet.

 * Utiliser **Composer** pour la gestion des dépendances d'un seul projet.
 * Utiliser **PEAR** lorsque vous devez gérer les dépendances pour un système complet.

En général, les packages Composer seront disponibles uniquement pour les projets auxquels vous les aurez explicitement 
spécifiés alors qu'un package PEAR sera disponible pour tous vos projets PHP. Bien que PEAR semble être la meilleure 
approche au premier regard, il existe de nombreux avantages à utiliser une approche de gestion des dépendances par 
projet.
