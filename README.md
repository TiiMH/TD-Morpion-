# TD-Morpion-

Partie 1 :

// Initialisation des helpers et de la grille
 
const ESICADHelpers = {
  readline: require('readline'),
  rl: null
};

const grid = [
  [' ', ' ', ' '],
  [' ', ' ', ' '],
  [' ', ' ', ' ']
];

// Fonction d'affichage de la grille

function printGrid() {
  console.log('  A B C');
  console.log('1 ' + grid[0].join(' | '));
  console.log('2 ' + grid[1].join(' | '));
  console.log('3 ' + grid[2].join(' | '));
}

// Validation du coup

function isValidMove(move) {
  const [x, y] = move.toUpperCase().split('');
  return x >= 'A' && x <= 'C' && y >= '1' && y <= '3' && grid[y - 1][x - 65] === ' ';
}

// Effectuer un coup

function makeMove(move, player) {
  const [x, y] = move.toUpperCase().split('');
  grid[y - 1][x - 65] = player;
}

// Fonction principale pour jouer la partie

async function jouerPartie() {
  ESICADHelpers.rl = ESICADHelpers.readline.createInterface({
    input: process.stdin,
    output: process.stdout
  });

  let player = 1;
  for (let moveCount = 0; moveCount < 9; moveCount++) {
    printGrid();
    const move = await new Promise(resolve => ESICADHelpers.question(`Joueur ${player}, entrez votre coup (ex: A1): `, resolve));
    if (isValidMove(move)) {
      makeMove(move, player === 1 ? 'X' : 'O');

      // Vérification de la victoire

      if (CheckWin(player === 1 ? 'X' : 'O')) {
        printGrid();
        console.log(`Joueur ${player} a gagné !`);
        ESICADHelpers;
        return player;
      }
      player = 3 - player;
    } else {
      console.log('Coup invalide, veuillez réessayer.');
      moveCount--; // Décrémenter le compteur pour réessayer le même tour.
    }
  }

  printGrid();
  console.log("Match nul !");
  ESICADHelpers;
  return 0; // Aucun joueur n'a gagné.
}

const winner = await jouerPartie();
console.log(winner !== 0 ? `Le vainqueur est le joueur ${winner} !` : "Le match est nul.");
function CheckWin(arg0) {
  throw new Error("Function not implemented.");
}
