## Exercice	2 : Le	2048 (obligatoire)

Vous trouverez les règles du 2048 à l’URL suivante :
https://fr.wikipedia.org/wiki/2048_(jeu_vidéo)
Alors que dans le premier exercice on s’est concentré sur la partie graphique de l’application (et
on a utilisé les éléments HTML et le DOM pour modéliser la grille de jeu), dans ce deuxième
exercice nous allons nous concentrer sur les fonctionnalités et la gestion des données en
JavaScript.
En effet, le premier exercice mélangeait volontairement la partie « noyau fonctionnel » de
l’application et la partie présentation.
Dans ce deuxième exercice, nous allons faire l’effort de séparer ces deux parties.
En partant du fichier XHTML5 « 2048.html » (que vous n’avez pas le droit de modifier) écrivez
le fichier CSS et JavaScript pour réaliser le jeu 2048 (vous devrez suivre les consignes données).
Bien lire l’ensemble des consignes avant de commencer à coder.
La grille sera modélisée sous la forme d’un tableau de tableau et initialisée dans une fonction
init().
Chaque case de la grille sera modélisée par un objet :

````javascript
// myBox object initializer
const myBox = {
    value: "",
    lastInsert: false
};
// The last Box
let lastBox = Object.create(myBox);
````

ayant une valeur (value) et un booléen (lastInsert, « false » à l’initialisation) qui servira à indiquer
si la valeur contenue est une nouvelle valeur insérée dans la grille par la fonction insertValue().

La fonction init() :

- Créera la grille, l’initialisera (chaque case aura pour valeur une chaîne vide).
- Abonnera la fenêtre à l’action « appui sur une touche du clavier » (la fonction appelée
  sera keyboardAction()).
- Ajoutera 2 valeurs aléatoirement dans la grille.

Affichera la grille via la fonction displayGrid().
La fonction keyboardAction() appelera les fonctions moveUp(), moveDown(), moveLeft() et
moveRight() en fonction de la touche de direction pressée.
Les autres touches seront ignorées. Les touches qui nous intéressent ont un keyCode entre 37 et 40.
La fonction displayGrid() mettra à jour le DOM en fonction de la grille. La dernière case ajoutée
sera en rouge. Pour le moment on ne s’occupe pas des autres effets graphiques (couleur des cases,
animations, …).
Chacune des fonctions move{Up,Down}() fonctionnera de la fonction suivante :

- Pour toutes les lignes (ou les colonnes en fonction du sens),
- si la ligne courante (ou la colonne) n’est pas vide :
  o tasser les cases dans le sens demandé,
  o fusionner les cases de même valeur,
  o tasser à nouveau les cases pour supprimer les blancs générés par la fonction de
  fusion.
- S’il y a eu au moins un mouvement ou une fusion dans les actions précédentes
  o ajouter une nouvelle valeur dans la grille,
  o afficher la grille.

L’ajout d’une valeur dans la grille sera faites par la fonction insertValue(value, coordinate)

- la valeur sera déterminée par une fonction getNewValue() qui retournera un 2 avec une
  probabilité de 0.9 et un 4 dans le reste des cas. La fonction Math.random() vous retourne
  une valeur dans l’intervalle [0 ; 1[.
- la coordonnée sera un objet composé de deux attributs, ligne et colonne. Elle
  correspondra à une case vide de la grille, déterminée aléatoirement par la fonction
  getEmptyBox().

Les fonctions tampTowards{Left,Right}(row) ou tampTowards{Up,Down}(column)
déplaceront l’ensemble des éléments de la ligne (ou de la colonne) dans la direction spécifiées
pour supprimer les cases vides. Il n’y a pas de fusion de nombre dans ce cas.

Les fonctions mergeTo{Left,Right}(row) ou mergeTo{Up,Down}(column) fusionneront les
éléments de même valeur qui sont cote à cote. En respectant la direction spécifiée.
Attention, ici on ne déplace pas de cases, certaines doublent de valeur, d’autres deviennent vide.
Les fonctions isEmptyRow(row) et isEmptyColumn(column) retourne vrai si la ligne (ou la
colonne) ne contient que des éléments de valeur vide.
