---
layout: base
title: Snake
permalink: /snake/
---

{% include nav/home.html %}

<style>
    body {
        background-color: #0000FF; /* Blue background color */
    }
    .wrap {
        margin-left: auto;
        margin-right: auto;
    }

    canvas {
        display: none;
        border-style: solid;
        border-width: 10px;
        border-color: #FFFFFF;
    }
    canvas:focus {
        outline: none;
    }

    /* All screens style */
    #gameover p, #setting p, #menu p {
        font-size: 20px;
    }

    #gameover a, #setting a, #menu a {
        font-size: 30px;
        display: block;
    }

    #gameover a:hover, #setting a:hover, #menu a:hover {
        cursor: pointer;
    }

    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before {
        content: ">";
        margin-right: 10px;
    }

    #menu {
        display: block;
    }

    #gameover {
        display: none;
    }

    #setting {
        display: none;
    }

    #setting input {
        display: none;
    }

    #setting label {
        cursor: pointer;
    }

    #setting input:checked + label {
        background-color: #FFF;
        color: #000;
    }
</style>

<h2>Snake</h2>

<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Score: <span id="score_value">0</span></p>
    </header>
    <div class="container bg-secondary" style="text-align:center;">
        <!-- Main Menu -->
        <div id="menu" class="py-4 text-light">
            <p>Welcome to Snake, press <span style="background-color: #FFFFFF; color: #000000">space</span> to begin</p>
            <a id="new_game" class="link-alert">new game</a>
            <a id="setting_menu" class="link-alert">settings</a>
        </div>
        <!-- Game Over -->
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press <span style="background-color: #FFFFFF; color: #000000">space</span> to try again</p>
            <a id="new_game1" class="link-alert">new game</a>
            <a id="setting_menu1" class="link-alert">settings</a>
        </div>
        <!-- Play Screen -->
        <canvas id="snake" class="wrap" width="320" height="320" tabindex="1"></canvas>
        <!-- Settings Screen -->
        <div id="setting" class="py-4 text-light">
            <p>Settings Screen, press <span style="background-color: #FFFFFF; color: #000000">space</span> to go back to playing</p>
            <a id="new_game2" class="link-alert">new game</a>
            <br>
            <p>Speed:
                <input id="speed1" type="radio" name="speed" value="200" checked/>
                <label for="speed1">Very Slow</label>
                <input id="speed2" type="radio" name="speed" value="150"/>
                <label for="speed2">Slow</label>
                <input id="speed3" type="radio" name="speed" value="100"/>
                <label for="speed3">Normal</label>
                <input id="speed4" type="radio" name="speed" value="50"/>
                <label for="speed4">Fast</label>
                <input id="speed5" type="radio" name="speed" value="25"/>
                <label for="speed5">Very Fast</label>
            </p>
            <p>Wall:
                <input id="wallon" type="radio" name="wall" value="1" checked/>
                <label for="wallon">On</label>
                <input id="walloff" type="radio" name="wall" value="0"/>
                <label for="walloff">Off</label>
            </p>
        </div>
    </div>
</div>

<script>
(function(){
    const canvas = document.getElementById("snake");
    const ctx = canvas.getContext("2d");
    const BLOCK = 10;
    let snake = [];
    let food = {x: 0, y: 0};
    let score = 0;
    let snakeSpeed = 150;
    let snakeDir = 1; // 0: Up, 1: Right, 2: Down, 3: Left
    let nextDir = snakeDir;
    let wall = 1;
    let gameLoop;

    function initGame() {
        snake = [{x: 8, y: 8}, {x: 7, y: 8}, {x: 6, y: 8}];
        score = 0;
        nextDir = 1;
        placeFood();
        gameLoop = setInterval(updateGame, snakeSpeed);
    }

    function placeFood() {
        food.x = Math.floor(Math.random() * (canvas.width / BLOCK));
        food.y = Math.floor(Math.random() * (canvas.height / BLOCK));
    }

    function updateGame() {
        // Update snake direction
        snakeDir = nextDir;

        // Get the new head position
        const head = {x: snake[0].x, y: snake[0].y};
        if (snakeDir === 0) head.y--;
        if (snakeDir === 1) head.x++;
        if (snakeDir === 2) head.y++;
        if (snakeDir === 3) head.x--;

        // Check collisions with walls
        if (wall === 1) {
            if (head.x < 0 || head.x >= canvas.width / BLOCK || head.y < 0 || head.y >= canvas.height / BLOCK) {
                gameOver();
                return;
            }
        } else {
            head.x = (head.x + canvas.width / BLOCK) % (canvas.width / BLOCK);
            head.y = (head.y + canvas.height / BLOCK) % (canvas.height / BLOCK);
        }

        // Check for collision with itself
        for (let i = 0; i < snake.length; i++) {
            if (head.x === snake[i].x && head.y === snake[i].y) {
                gameOver();
                return;
            }
        }

        // Move snake by adding new head
        snake.unshift(head);

        // Check for food collision
        if (head.x === food.x && head.y === food.y) {
            score++;
            placeFood();
        } else {
            snake.pop();
        }

        drawGame();
    }

    function drawGame() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        // Draw snake
        ctx.fillStyle = "green";
        for (let i = 0; i < snake.length; i++) {
            ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
        }

        // Draw food
        ctx.fillStyle = "red";
        ctx.fillRect(food.x * BLOCK, food.y * BLOCK, BLOCK, BLOCK);

        // Update score
        document.getElementById("score_value").textContent = score;
    }

    function gameOver() {
        clearInterval(gameLoop);
        alert("Game Over! Your score was " + score);
        showScreen(-1); // Show menu
    }

    function showScreen(screen) {
        document.getElementById("snake").style.display = screen === 0 ? "block" : "none";
        document.getElementById("menu").style.display = screen === -1 ? "block" : "none";
        document.getElementById("gameover").style.display = screen === 1 ? "block" : "none";
        document.getElementById("setting").style.display = screen === 2 ? "block" : "none";
    }

    function newGame() {
        clearInterval(gameLoop);
        showScreen(0); // Show snake canvas
        initGame();
    }

    document.getElementById("new_game").onclick = newGame;
    document.getElementById("new_game1").onclick = newGame;
    document.getElementById("new_game2").onclick = newGame;

    window.addEventListener("keydown", function(event) {
        if (event.code === "ArrowUp" && snakeDir !== 2) nextDir = 0;
        if (event.code === "ArrowRight" && snakeDir !== 3) nextDir = 1;
        if (event.code === "ArrowDown" && snakeDir !== 0) nextDir = 2;
        if (event.code === "
