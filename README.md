# **2048 avec p5.js - Guide Étape par Étape**

## **Introduction**

Bienvenue dans ce projet de création du jeu 2048 avec p5.js ! Ce guide est conçu pour aider les lycéens à découvrir la programmation tout en s'amusant. Vous allez apprendre à réaliser un jeu simple et visuel avec p5.js, une bibliothèque JavaScript idéale pour créer des applications graphiques.

Nous allons créer une version fonctionnelle du célèbre jeu 2048. Ce guide est décomposé en plusieurs étapes, avec des morceaux de code à compléter. L'objectif est de vous encourager à réfléchir et à trouver les solutions par vous-mêmes. N'oubliez pas, l'apprentissage est encore plus enrichissant lorsque vous explorez et recherchez par vous-mêmes !

## **Présentation de p5.js**

p5.js est une bibliothèque JavaScript qui simplifie la création de visuels interactifs. Elle est très utilisée pour des projets artistiques, graphiques et éducatifs. Vous allez l'utiliser dans un éditeur en ligne pratique, qui vous permet de tester votre code directement dans votre navigateur.

Pour ce projet, nous allons utiliser l'éditeur en ligne de p5.js : editor.p5js.org. Il ne nécessite aucune installation, ce qui rend le début de ce projet très simple.

## **Étapes du projet**

### **1. Mise en place de l'environnement**

***Action*** : Rendez-vous sur editor.p5js.org.

***Action :*** Créez un nouveau projet en cliquant sur "New Sketch".

***Explication :*** L'éditeur p5.js vous permet d'écrire du code JavaScript et de voir directement le résultat graphique. Cela rend l'exploration et l'apprentissage très interactifs.

***Action :*** Prenez quelques minutes pour explorer l'éditeur et tester un code simple comme :

`function setup() {
  createCanvas(400, 400);
  background(220); // Crée un fond gris clair
}`

***Défi :*** Modifiez le fond pour qu'il soit d'une autre couleur de votre choix. Ceci vous aidera à comprendre comment fonctionne le canevas.

### **2. Création de la grille 4x4 avec des variables constantes**

***Objectif :*** Créer une grille 4x4 qui représentera le plateau du jeu en utilisant des variables constantes pour rendre le code plus flexible.

***Explication :*** Nous allons définir des constantes pour la taille de la grille et du canevas, ainsi qu'un objet pour les couleurs des tuiles.

***Action :*** Ajoutez les variables constantes suivantes en haut de votre code :

`const GRID_SIZE = 4;
const CANVAS_SIZE = 400;
const TILE_COLORS = {
  0: [205, 193, 180],
  2: [238, 228, 218],
  4: [237, 224, 200],
  8: [242, 177, 121],
  16: [245, 149, 99],
  32: [246, 124, 95],
  64: [246, 94, 59],
  128: [237, 207, 114],
  256: [237, 204, 97],
  512: [237, 200, 80],
  1024: [237, 197, 63],
  2048: [237, 194, 46]
};`

`const EMPTY_TILE = 0;`

***Action :*** Créez une fonction qui initialise un tableau à deux dimensions rempli de zéros.

__Code à compléter :__

`function blankGrid() {
  // Crée une grille vide GRID_SIZE x GRID_SIZE remplie de zéros
  return Array.from({ length: GRID_SIZE }, () => _____.fill(_____));
}`

***Défi :*** Complétez la fonction blankGrid() pour qu'elle utilise GRID_SIZE et EMPTY_TILE.

### 3. Ajouter des cases aléatoires (2 ou 4)
***Objectif :*** Au début du jeu, deux cases aléatoires doivent être remplies avec une valeur de 2 ou de 4.

***Explication :*** Pour rendre le jeu intéressant, nous devons initialiser la grille avec deux tuiles qui apparaîtront dans des positions aléatoires.

***Action :*** Écrivez une fonction qui sélectionne une case vide de la grille et y place un 2 ou un 4.

__Code à compléter :__

`function addNumber(grid) {
  let options = [];
  for (let i = 0; i < GRID_SIZE; i++) {
    for (let j = 0; j < GRID_SIZE; j++) {
      if (grid[i][j] === _____) {
        options.push({ x: i, y: j });
      }
    }
  }
  if (options.length > 0) {
    let spot = random(options);
    grid[spot.x][spot.y] = random(1) > 0.5 ? ___ : ___;
  }
}`

***Défi :*** Complétez les espaces vides pour que la fonction ajoute un 2 ou un 4 dans une case vide.

### 4. Dessiner la grille sur le canevas
***Objectif :*** Représenter visuellement la grille sur le canevas.

***Explication :*** Il est essentiel de dessiner la grille et les tuiles à l'écran pour visualiser le jeu.

***Action :*** Créez une fonction qui dessine la grille, chaque case représentant une valeur de la grille.

_Code à compléter :__

`function drawGrid(grid) {
  let w = CANVAS_SIZE / GRID_SIZE;
  for (let i = 0; i < GRID_SIZE; i++) {
    for (let j = 0; j < GRID_SIZE; j++) {
      let val = grid[i][j];
      let col = TILE_COLORS[val] || [60, 60, 60];
      fill(...col);
      stroke(0);
      rect(j * w, i * w, w, w);
      if (val !== EMPTY_TILE) {
        textAlign(CENTER, CENTER);
        textSize(32);
        fill(0);
        text(val, j * w + w / 2, i * w + w / 2);
      }
    }
  }
}`

***Défi :*** Essayez de modifier les tailles de police ou les couleurs pour personnaliser l'apparence du jeu.

### 5. Gestion des mouvements des cases
***Objectif :*** Implémenter les mouvements des cases vers le haut, bas, gauche et droite.

***Explication :*** L'utilisateur doit pouvoir déplacer les tuiles en utilisant les touches du clavier.

***Action :*** Implémentez la fonction keyPressed() pour gérer les entrées clavier.

__Code à compléter :__

`function keyPressed() {
  let moved = false;
  let past = copyGrid(grid);
  switch (keyCode) {
    case RIGHT_ARROW:
      grid = slideRight(grid);
      break;
    case LEFT_ARROW:
      grid = _____(grid);
      break;
    case DOWN_ARROW:
      grid = _____(grid);
      break;
    case UP_ARROW:
      grid = _____(grid);
      break;
    default:
      return;
  }
  if (!compare(past, grid)) {
    moved = true;
  }
  if (moved) {
    addNumber(grid);
  }
}`

***Défi :*** Complétez les fonctions de déplacement pour slideLeft, slideDown et slideUp.

### 6. Fusionner les cases identiques
***Objectif :*** Lorsque deux cases avec la même valeur se rencontrent, elles doivent se combiner.

***Explication :*** Lorsqu'on déplace les tuiles, si deux tuiles adjacentes ont la même valeur, elles se fusionnent en une seule avec une valeur doublée.

***Action :*** Modifiez les fonctions de glissement pour inclure la fusion des tuiles.

__Code à compléter :__
`
function slideAndCombine(row) {
  row = slide(row);
  row = combine(row);
  return slide(row);
}`

`function slide(row) {
  let newRow = row.filter(val => val);
  let missing = GRID_SIZE - newRow.length;
  let zeros = Array(missing).fill(EMPTY_TILE);
  return zeros.concat(newRow);
}`

`function combine(row) {
  for (let i = row.length - 1; i >= 1; i--) {
    if (row[i] === row[i - 1] && row[i] !== EMPTY_TILE) {
      row[i] *= ___;
      row[i - 1] = _____;
    }
  }
  return row;
}`

***Défi :*** Complétez la fonction combine() pour qu'elle double la valeur des tuiles fusionnées et remplace la tuile précédente par une case vide.

### 7. Ajouter une nouvelle case après chaque mouvement
***Objectif :*** Après chaque mouvement, une nouvelle case (valant 2 ou 4) doit apparaître dans une case vide.

***Explication :*** Pour maintenir le jeu dynamique, une nouvelle tuile apparaît après chaque mouvement valide.

***Action :*** Assurez-vous que la fonction keyPressed() ajoute une nouvelle tuile uniquement si un mouvement a eu lieu.

__Code à compléter :__

`if (!compare(past, grid)) {
  moved = true;
}
if (moved) {
  addNumber(grid);
}`

***Défi :*** Implémentez les fonctions copyGrid() et compare() pour comparer les grilles avant et après le mouvement.

### 8. Gérer les conditions de victoire et de défaite
***Objectif :*** Détecter si le joueur a gagné (lorsqu'une case atteint 2048) ou s'il a perdu (aucun mouvement possible).

***Explication :*** Le jeu doit indiquer si le joueur a atteint la tuile 2048 ou s'il ne peut plus effectuer de mouvements.

***Action :*** Écrivez les fonctions isGameOver() et isGameWon().

__Code à compléter :__

`function isGameOver(grid) {
  for (let i = 0; i < GRID_SIZE; i++) {
    for (let j = 0; j < GRID_SIZE; j++) {
      if (grid[i][j] === EMPTY_TILE) {
        return false;
      }
      if (i !== GRID_SIZE - 1 && grid[i][j] === grid[i + 1][j]) {
        return false;
      }
      if (j !== GRID_SIZE - 1 && grid[i][j] === grid[i][j + 1]) {
        return false;
      }
    }
  }
  return true;
}`

`function isGameWon(grid) {
  for (let i = 0; i < GRID_SIZE; i++) {
    for (let j = 0; j < GRID_SIZE; j++) {
      if (grid[i][j] === _____) {
        return true;
      }
    }
  }
  return false;
}`

***Défi :*** Complétez isGameWon() pour qu'elle renvoie true lorsque la valeur 2048 est atteinte.

### 9. Amélioration visuelle (facultatif)
***Objectif :*** Ajouter des animations ou des effets visuels pour rendre le jeu plus plaisant.

***Idées :***

***Animations :*** Ajoutez des transitions douces lorsque les tuiles se déplacent ou fusionnent.

***Scores :*** Affichez le score actuel et les meilleurs scores précédents.

***Messages :*** Affichez des messages de victoire ou de défaite avec des styles attractifs.

***Personnalisation :*** Changez les couleurs ou les polices pour donner un style unique à votre jeu.

***Défi :*** Choisissez une ou plusieurs améliorations et implémentez-les dans votre jeu.

# Conclusion
Félicitations ! Vous avez maintenant une version fonctionnelle du jeu 2048 réalisée avec p5.js. Ce projet vous a permis de découvrir des concepts clés en programmation tels que les tableaux, les fonctions, la gestion des événements clavier et la manipulation du canevas graphique.

N'hésitez pas à continuer d'explorer et à améliorer votre jeu. Vous pouvez ajouter de nouvelles fonctionnalités, optimiser le code ou même créer de nouveaux jeux en utilisant ce que vous avez appris.

Si vous rencontrez des difficultés, consultez la documentation de p5.js ou demandez de l'aide à vos enseignants ou camarades. L'important est de rester curieux et de s'amuser en programmant !

***Bonne chance et amusez-vous bien !***
