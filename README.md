# CODSOFT-TIC-TAC-TOE-GAME
Write a C++ program to build a simple console-based Tic-Tac-Toe game that allows two players to play against each other

#include <iostream>
#include <vector>

using namespace std;


vector<vector<char>> board = {{'1', '2', '3'}, {'4', '5', '6'}, {'7', '8', '9'}};


char player1 = 'X';
char player2 = 'O';


void displayBoard() {
  for (const auto& row : board) {
    for (const auto& cell : row) {
      cout << cell << " ";
    }
    cout << endl;
  }
}


void playerInput(char player) {
  int move;
  cout << "Player " << player << ", enter your move (1-9): ";
  cin >> move;

  
  for (auto& row : board) {
    for (auto& cell : row) {
      if (cell == '0' + move) {
        cell = player;
        break;
      }
    }
  }
}


bool checkForWin(char player) {
  // Check rows
  for (const auto& row : board) {
    if (row[0] == player && row[1] == player && row[2] == player) {
      return true;
    }
  }

  
  for (int i = 0; i < 3; i++) {
    if (board[0][i] == player && board[1][i] == player && board[2][i] == player) {
      return true;
    }
  }

  
  if (board[0][0] == player && board[1][1] == player && board[2][2] == player) {
    return true;
  }
  if (board[0][2] == player && board[1][1] == player && board[2][0] == player) {
    return true;
  }

  return false;
}


bool checkForDraw() {
  for (const auto& row : board) {
    for (const auto& cell : row) {
      if (cell != 'X' && cell != 'O') {
        return false;
      }
    }
  }
  return true;
}

int main() {
  bool playAgain = true;

  while (playAgain) {
    displayBoard();

    playerInput(player1);
    displayBoard();

    if (checkForWin(player1)) {
      cout << "Player X wins!" << endl;
      break;
    }

    playerInput(player2);
    displayBoard();

    if (checkForWin(player2)) {
      cout << "Player O wins!" << endl;
      break;
    }

    if (checkForDraw()) {
      cout << "It's a draw!" << endl;
      break;
    }
  }

  cout << "Do you want to play again? (y/n): ";
  char answer;
  cin >> answer;

  if (answer == 'y') {
    playAgain = true;
  } else {
    playAgain = false;
  }

  return 0;
}
