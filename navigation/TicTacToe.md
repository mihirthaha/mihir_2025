---
layout: post
title: Games Page
comments: false
permalink: /tictactoe/
---

<!DOCTYPE html>
<html>
<head>
  <title>Tic Tac Toe</title>
  <style>
    table {
      border-collapse: collapse;
    }
    td {
      border: 1px solid #ccc;
      width: 50px;
      height: 50px;
      text-align: center;
      font-size: 24px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Tic Tac Toe</h1>
  <table>
    <tr>
      <td id="cell-0" onclick="makeMove(this, 0)"></td>
      <td id="cell-1" onclick="makeMove(this, 1)"></td>
      <td id="cell-2" onclick="makeMove(this, 2)"></td>
    </tr>
    <tr>
      <td id="cell-3" onclick="makeMove(this, 3)"></td>
      <td id="cell-4" onclick="makeMove(this, 4)"></td>
      <td id="cell-5" onclick="makeMove(this, 5)"></td>
    </tr>
    <tr>
      <td id="cell-6" onclick="makeMove(this, 6)"></td>
      <td id="cell-7" onclick="makeMove(this, 7)"></td>
      <td id="cell-8" onclick="makeMove(this, 8)"></td>
    </tr>
  </table>
  <script>
    let gameBoard = [];
    let currentPlayer = 'X';

    <!-- Initialize game board -->
    for (let i = 0; i < 9; i++) {
      gameBoard.push('');
    }

    <!-- Function to handle cell click -->
    function makeMove(cell, index) {
      if (gameBoard[index] === '') {
        gameBoard[index] = currentPlayer;
        cell.textContent = currentPlayer;
        checkForWin();
        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
      }
    }

    <!-- Function to check for win -->
    function checkForWin() {
      const winConditions = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ];
      for (let i = 0; i < winConditions.length; i++) {
        const condition = winConditions[i];
        if (gameBoard[condition[0]] === gameBoard[condition[1]] && gameBoard[condition[1]] === gameBoard[condition[2]] && gameBoard[condition[0]] !== '') {
          alert(`Player ${gameBoard[condition[0]]} wins!`);
          resetGame();
        }
      }
    }

    <!-- Function to reset game -->
    function resetGame() {
      gameBoard = [];
      for (let i = 0; i < 9; i++) {
        gameBoard.push('');
      }
      currentPlayer = 'X';
      const cells = document.querySelectorAll('td');
      cells.forEach(cell => cell.textContent = '');
    }
  </script>
</body>
</html>