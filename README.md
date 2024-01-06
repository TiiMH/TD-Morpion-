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

Patie 2 : 

/**
* Cette interface représente une structure qui est un choix d'un menu à
plusieurs choix
*/
export interface MenuItem {
  /**
  * la propriété `label` permet d'afficher un titre visualisable dans le
  menu
  */
  label: string;
  /**
  * la propriété `function` permet de référencer une fonction qui sera
  exécutée lorsque l'utilisateur choisit le menu
  */
  function: Function;
  }

  function genererMenu(titreMenu, choix:) {
      console.log(titreMenu);
      choix.forEach((element, index) => {
          console.log(`${index + 1}) ${element.label}`);
      });
  
      let choixUtilisateur = parseInt(prompt("Numero option choisit :"));
      while (isNaN(choixUtilisateur) || choixUtilisateur < 1 || choixUtilisateur > choix.length) {
          choixUtilisateur = parseInt(prompt("Saisie invalide. Entrer le numéro de l'option choisie :"));
      }
  
      return choix[choixUtilisateur - 1].function;
  }

  function menuPrincipal() {
      let titreMenu = "Jeu de morpions";
      let choix = [
          { label: "Nouvelle partie", function: jouerPartie },
          { label: "Sauvegarde de partie", function: () => {} }, // à implémenter
          { label: "Quitter", function: () => { console.log("Au revoir !"); process.exit(); } }
      ];
  
      return genererMenu(titreMenu, choix);
  }

// Sauvegarde

const fs = require('fs');

/*
* Fonction pour sauvegarder les coups joués par les joueurs dans un fichier
* {string} nomFichier - Fichier de sauvegarde
* {object} data - Données à sauvegarder
*/

function sauvegarderPartie(nomFichier, data) {
fs.writeFileSync(nomFichier, JSON.stringify(data));
}

// Exemple d'utilisation de la fonction sauvegarderPartie
let coupsJoues = { coup1: 'A1', coup2: 'B2' };
sauvegarderPartie('sauvegarde.json', coupsJoues);

// Charger partie 

function chargerPartie(cheminFichier) {
  const fichier = require(cheminFichier);
// Restaurer une partie sauvegardée
  return JSON.parse(fichier);
}

// Charger une partie et relancer le jeu de la ou on a sauvegardé
const situation = chargerPartie('chemin/vers/fichierSauvegarde.json');
jouerPartie(situation);

//  Morpions sur longueur n

  function tailleGrille() {
    for (let i = 0; i < tailleMatrice; i++) {
      for (let j = 0; j < tailleMatrice; j++) {
        if (grille[i][j] === null) {
          return false;
        }
      }
    }
    return true;
  }

  while (!finDeJeu) {
    console.debug();
    afficherGrille();
    let x = parseInt(prompt("Entrez ligne (0 à " + (tailleMatrice - 1) + ") :"));
    let y = parseInt(prompt("Entrez colonne (0 à " + (tailleMatrice - 1) + ") :"));
    while (
      isNaN(x) ||
      isNaN(y) ||
      x < 0 ||
      y > 0 ||
      x >= tailleMatrice ||
      y >= tailleMatrice ||
      caseLibre(x, y)
    ) {
      x = parseInt(prompt("Saisie invalide. Entrez ligne :"));
      y = parseInt(prompt("Saisie invalide. Entrez colonne :"));
    }
    jouerCoup(x, y);
  }
const winner = await jouerPartie();
console.log(winner !== 0 ? `Le vainqueur est le joueur ${winner} !` : "Le match est nul.");
function CheckWin(arg0) {
  throw new Error("Function not implemented.");
}
