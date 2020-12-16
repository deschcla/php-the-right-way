---
isChild: true
anchor:  vagrant
---

## Vagrant {#vagrant_title}

[Vagrant][vagrant] vous permet de mettre en place une machine
virtuelle en seulement quelques étapes.
Ces systèmes de base peuvent ensuite être configurés manuellement ou via des outils comme [Puppet][puppet] ou
[Chef][chef]. Configurer ces systèmes de façon automatisée est un bon moyen de s'assurer que les différents systèmes
mis en place seront configurés de la même manière sans avoir à maintenir une liste de commandes pour l'installation.
Vous pouvez aussi "détruire" votre système et en recréer un nouveau de façon entièrement automatisée, ce qui facilite
les nouvelles installations.

Vagrant crée des dossiers partagés utilisés pour permettre à l'hôte et à la machine virtuelle d'accéder
de façon bidirectionnelle à votre code, ce qui signifie que vous pouvez créer et éditer vos fichiers sur le système
hôte et exécuter votre code sur la machine virtuelle.

### Un coup de pouce

Si vous avez besoin d'aide pour commencer à utiliser Vagrant, il existe 3 services qui pourraient vous être utiles :

- [Rove][rove]: Un service qui vous autorise à pré-générer des builds Vagrant typiques avec PHP. L'installation se fait
avec Chef.
- [Puphpet][puphpet]: une interface graphique simple pour mettre en place des machines virtuelles pour développer en PHP.
 **Il se concentre énormement sur PHP**. Par ailleurs, des VMs locales peuvent être utilisées pour déployer des services
clouds. L'installation se fait avec Puppet.
- [Protobox][protobox]: est composé d'une couche au-dessus de Vagrant et d'une interface web pour installer des machines
virtuelles pour le développement web. Un seul document YAML contrôle tout ce qui peut être installé sur la machine
virtuelle.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/
