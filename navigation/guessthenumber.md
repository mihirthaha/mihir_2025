---
layout: base
title: Guess the Number Game 
description: Play the game
permalink: /guess-the-number/
---

{% include nav/home.html %}

# Simple JavaScript Game: Guess the Number

Guess a number between 1 and 100!

<div id="game">
  <p>Enter a number between 1 and 100:</p>
  <input type="number" id="guess" min="1" max="100">
  <button onclick="checkGuess()">Submit Guess</button>
  
  <p id="result"></p>
  <p id="attempts"></p>
  <button onclick="restartGame()">Restart Game</button>
</div>

<script>
  let randomNumber = Math.floor(Math.random() * 100) + 1;
  let attempts = 0;

  function checkGuess() {
    let userGuess = document.getElementById('guess').value;
    let resultText = document.getElementById('result');
    let attemptsText = document.getElementById('attempts');
    
    if (!userGuess) {
      resultText.innerHTML = "Please enter a number!";
      return;
    }

    attempts++;
    if (userGuess < randomNumber) {
      resultText.innerHTML = "Too low!";
    } else if (userGuess > randomNumber) {
      resultText.innerHTML = "Too high!";
    } else {
      resultText.innerHTML = "Congratulations! You guessed the number!";
    }

    attemptsText.innerHTML = `Attempts: ${attempts}`;
  }

  function restartGame() {
    randomNumber = Math.floor(Math.random() * 100) + 1;
    attempts = 0;
    document.getElementById('result').innerHTML = "";
    document.getElementById('attempts').innerHTML = "";
    document.getElementById('guess').value = "";
  }
</script>

<style>
  #game {
    font-family: Arial, sans-serif;
    margin: 20px;
  }
  #guess {
    width: 50px;
  }
  #result {
    font-weight: bold;
    margin-top: 10px;
  }
</style>
