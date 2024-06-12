---
layout: default
nav_order: 6
title: KICAD
---

# <span style="color:#003366">_kicad_</span>

Après avoir utiliser Wokwi afin de définir les différentes fonctionnalités qui nous serons utiles et les pins que nous allons utiliser, nous passons à la création de la carte électronique pour se faire nous utilisons Kicad un logiciel open source.

## <span style="color:#003366">_Editeur de Schématique_</span>

Pour commencer nous utilisons l’éditeur de schématique afin de placer nos différents composants et de les connectés. Nous plaçons l’esp 32 de 38 broches en premier puisqu’il compose la pièce principale, nous utilisons ici un devkit afin de simplifier notre carte électronique et nous avons choisi un 38 broches pour son pins 5V qui nous permet d’alimenter en 5V en plus du 3V3 présent aussi sur les autres devkit. Nous choisissons d’utiliser des connecteurs pour les interrupteurs, l’écran et l’alimentation afin de simplifier l’assemblage futur. Nous avons du importer dans les librairies les joystick car ceci n’étaient pas présent de base. Nous avons ajouter aussi une led afin de servir de témoin lumineux pour l’alimentation.
Une fois tout nos composants plaçaient nous les relions aux pins leurs correspondant décidé lors du wokwi pour cela nous utilisons des fils et des labels.

![Illustration assemblage](images/13.png)

## <span style="color:#003366">_Empreintes_</span>

Une fois notre schématique terminer nous devons prendre chaque composants et leurs attribués des empreintes pour cela nous utilisons la commande E. Dans le menu des empreintes nous avons un large choix avec plusieurs empreintes pouvant correspondre à un même composant pour décider duquel choisir il faut se référé au composant que nous avons commander, si l’empreinte désirer ne se trouve pas dans la bibliothèque il faut l’ajouter.

![Illustration assemblage](images/18.png)

## <span style="color:#003366">_Éditeur de PCB kicad_</span>

On passe sur la phase 2 ici on commence par définir la forme et la taille de notre carte. On place ensuite les empreintes de façon optimales on défini une taille de gravure de 0.8mm(c’est la taille des industriels qui produisent nos cartes) pour pouvoir relier les composants. Pour relier les composants entre eux on doit faire attention à ce que ceci ne se croisent pas pour cela on possède 2 faces sur lesquels on peut tracer nos gravures, on relie seulement les pins relié à la phase. Pour la masse on réalise ce qu on appel un plan de masse qui va faire du reste de notre carte (la où il n’y a pas les gravures) une masse afin de l’éditer on se sert de la touche B.

![Illustration assemblage](images/15.png)

## <span style="color:#003366">_Réglages_</span>

Afin de vérifier notre carte nous possédons plusieurs solutions on peut imprimer sur papier la carte pour vérifier la taille des trous pour les pins. On peut également visualisé la carte en 3D pour se rendre compte du résultat. On peut aussi l’imprimer en 3D afin de se rendre compte de sa corpulence réel. Enfin toutes ces fonctionnalités nous permettes de régler la place des composants et le choix des empreintes afin de limiter les erreurs avant la production.  Une fois fini on peut envoyer notre fichier à l’industriels pour l’impression.

![Illustration assemblage](images/14.png)
![Illustration assemblage](images/16.png)
![Illustration assemblage](images/17.png)

Page web réalisée par Célien BONELLO, étudiant à UniLaSalle Amiens.
