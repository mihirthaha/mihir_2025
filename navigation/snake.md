---
layout: post
title: Games Page
comments: false
permalink: /games/
---

<style>
    body {
        /* General body style */
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
    #gameover p, #setting p, #menu p, #tic-tac-toe p {
        font-size: 20px;
    }

    #gameover a, #setting a, #menu a, #tic-tac-toe a {
        font-size: 30px;
        display: block;
    }

    #gameover a:hover, #setting a:hover, #menu a:hover, #tic-tac-toe a:hover {
        cursor: pointer;
    }

    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before, #tic-tac-toe a:hover::before {
        content: ">";
        margin-right: 10px;
    }

    #menu, #tic-tac-toe {
        display: block;
    }

    #gameover, #setting {
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

    .tic-tac-toe-grid {
        display: grid;
        grid-template-columns: repeat(3, 100px);
        grid-template-rows: repeat(3, 100px);
        gap: 5px;
        justify-content: center;
        margin-top: 20px;
    }

    .tic-tac-toe-cell {
        width: 100px;
        height: 100px;
        font-size: 3rem;
        text-align: center;
        line-height: 100px;
        background-color: #f0f0f0;
        border: 1px solid #000;
        cursor: pointer;
    }

    .tic-tac-toe-cell:hover {
        background-color: #ddd;
    }
</style>

<h2>Games</h2>
<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Select a game to play:</p>
    </header>

    <!-- Main Menu for Game Selection -->
    <div id="menu" class="py-4 text-light">
        <p>Choose a game:</p>
        <a id="play_snake" class="link-alert">Snake Game</a>
        <a id="play_tic_tac_toe" class="link-alert">Tic-Tac-Toe</a>
    </div>

    <!-- Snake Game Section (Existing Snake Game Code) -->
    <div id="snake_section" style="display: none;">
        <header class="pb-3 mb-4 border-bottom border-primary text-dark">
            <p class="fs-4">Snake Score: <span id="score_value">0</span></p>
        </header>
        <canvas id="snake" class="wrap" width="320" height="320" tabindex="1"></canvas>
        <!-- Other Snake elements, settings, and scripts go here (same as in the Snake game code) -->
    </div>

    <!-- Tic-Tac-Toe Game Section -->
    <div id="tic-tac-toe" style="display: none;">
        <header class="pb-3 mb-4 border-bottom border-primary text-dark">
            <p class="fs-4">Tic-Tac-Toe</p>
        </header>
        <div class="tic-tac-toe-grid">
            <div class="tic-tac-toe-cell" data-cell="0"></div>
            <div class="tic-tac-toe-cell" data-cell="1"></div>
            <div class="tic-tac-toe-cell" data-cell="2"></div>
            <div class="tic-tac-toe-cell" data-cell="3"></div>
            <div class="tic-tac-toe-cell" data-cell="4"></div>
            <div class="tic-tac-toe-cell" data-cell="5"></div>
            <div class="tic-tac-toe-cell" data-cell="6"></div>
            <div class="tic-tac-toe-cell" data-cell="7"></div>
            <div class="tic-tac-toe-cell" data-cell="8"></div>
        </div>
        <p id="game_status"></p>
        <a id="restart_tic_tac_toe" class="link-alert">Restart Tic-Tac-Toe</a>
    </div>
</div>

<script>
    // Game Selection Logic
    document.getElementById("play_snake").onclick = function () {
        document.getElementById("menu").style.display = "none";
        document.getElementById("snake_section").style.display = "block";
    };

    document.getElementById("play_tic_tac_toe").onclick = function () {
        document.getElementById("menu").style.display = "none";
        document.getElementById("tic-tac-toe").style.display = "block";
    };

    // Tic-Tac-Toe Logic
    const cells = document.querySelectorAll('.tic-tac-toe-cell');
    const statusText = document.getElementById('game_status');
    let currentPlayer = 'X';
    let gameActive = true;
    let board = ['', '', '', '', '', '', '', '', ''];

    function checkWinner() {
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
            const [a, b, c] = winConditions[i];
            if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                return board[a];
            }
        }
        return board.includes('') ? null : 'Draw';
    }

    function handleClick(e) {
        const cellIndex = e.target.getAttribute('data-cell');
        if (board[cellIndex] !== '' || !gameActive) return;
        board[cellIndex] = currentPlayer;
        e.target.textContent = currentPlayer;
        const winner = checkWinner();
        if (winner) {
            statusText.textContent = winner === 'Draw' ? "It's a draw!" : `${winner} wins!`;
            gameActive = false;
        } else {
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
        }
    }

    function restartGame() {
        board = ['', '', '', '', '', '', '', '', ''];
        currentPlayer = 'X';
        gameActive = true;
        cells.forEach(cell => cell.textContent = '');
        statusText.textContent = '';
    }

    cells.forEach(cell => cell.addEventListener('click', handleClick));
    document.getElementById('restart_tic_tac_toe').addEventListener('click', restartGame);

    // Include the existing Snake game script here (same as the Snake game code provided)
    <style>

    body{
    }
    .wrap{
        margin-left: auto;
        margin-right: auto;
    }

    canvas{
        display: none;
        border-style: solid;
        border-width: 10px;
        border-color: #FFFFFF;
    }
    canvas:focus{
        outline: none;
    }

    /* All screens style */
    #gameover p, #setting p, #menu p{
        font-size: 20px;
    }

    #gameover a, #setting a, #menu a{
        font-size: 30px;
        display: block;
    }

    #gameover a:hover, #setting a:hover, #menu a:hover{
        cursor: pointer;
    }

    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before{
        content: ">";
        margin-right: 10px;
    }

    #menu{
        display: block;
    }

    #gameover{
        display: none;
    }

    #setting{
        display: none;
    }

    #setting input{
        display:none;
    }

    #setting label{
        cursor: pointer;
    }

    #setting input:checked + label{
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
                <input id="speed0" type="radio" name="speed" value="150"/>
                <label for="speed0">Slowest</label>
                <input id="speed1" type="radio" name="speed" value="120" checked/>
                <label for="speed1">Slow</label>
                <input id="speed2" type="radio" name="speed" value="75"/>
                <label for="speed2">Normal</label>
                <input id="speed3" type="radio" name="speed" value="35"/>
                <label for="speed3">Fast</label>
                <input id="speed4" type="radio" name="speed" value="15" />
                <label for="speed4">Super Fast</label>
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
        /* Attributes of Game */
        /////////////////////////////////////////////////////////////
        // Canvas & Context
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");
        // HTML Game IDs
        const SCREEN_SNAKE = 0;
        const screen_snake = document.getElementById("snake");
        const ele_score = document.getElementById("score_value");
        const speed_setting = document.getElementsByName("speed");
        const wall_setting = document.getElementsByName("wall");
        // HTML Screen IDs (div)
        const SCREEN_MENU = -1, SCREEN_GAME_OVER=1, SCREEN_SETTING=2;
        const screen_menu = document.getElementById("menu");
        const screen_game_over = document.getElementById("gameover");
        const screen_setting = document.getElementById("setting");
        // HTML Event IDs (a tags)
        const button_new_game = document.getElementById("new_game");
        const button_new_game1 = document.getElementById("new_game1");
        const button_new_game2 = document.getElementById("new_game2");
        const button_setting_menu = document.getElementById("setting_menu");
        const button_setting_menu1 = document.getElementById("setting_menu1");
        // Game Control
        const BLOCK = 10;   // size of block rendering
        let SCREEN = SCREEN_MENU;
        let snake;
        let snake_dir;
        let snake_next_dir;
        let snake_speed;
        let food = {x: 0, y: 0};
        let score;
        let wall;
        /* Display Control */
        /////////////////////////////////////////////////////////////
        // 0 for the game
        // 1 for the main menu
        // 2 for the settings screen
        // 3 for the game over screen
        let showScreen = function(screen_opt){
            SCREEN = screen_opt;
            switch(screen_opt){
                case SCREEN_SNAKE:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "none";
                    break;
                case SCREEN_GAME_OVER:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "block";
                    break;
                case SCREEN_SETTING:
                    screen_snake.style.display = "none";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "block";
                    screen_game_over.style.display = "none";
                    break;
            }
        }
        /* Actions and Events  */
        /////////////////////////////////////////////////////////////
        window.onload = function(){
            // HTML Events to Functions
            button_new_game.onclick = function(){newGame();};
            button_new_game1.onclick = function(){newGame();};
            button_new_game2.onclick = function(){newGame();};
            button_setting_menu.onclick = function(){showScreen(SCREEN_SETTING);};
            button_setting_menu1.onclick = function(){showScreen(SCREEN_SETTING);};
            // speed
            setSnakeSpeed(150);
            for(let i = 0; i < speed_setting.length; i++){
                speed_setting[i].addEventListener("click", function(){
                    for(let i = 0; i < speed_setting.length; i++){
                        if(speed_setting[i].checked){
                            setSnakeSpeed(speed_setting[i].value);
                        }
                    }
                });
            }
            // wall setting
            setWall(1);
            for(let i = 0; i < wall_setting.length; i++){
                wall_setting[i].addEventListener("click", function(){
                    for(let i = 0; i < wall_setting.length; i++){
                        if(wall_setting[i].checked){
                            setWall(wall_setting[i].value);
                        }
                    }
                });
            }
            // activate window events
            window.addEventListener("keydown", function(evt) {
                // spacebar detected
                if(evt.code === "Space" && SCREEN !== SCREEN_SNAKE)
                    newGame();
            }, true);
        }
        /* Snake is on the Go (Driver Function)  */
        /////////////////////////////////////////////////////////////
        let mainLoop = function(){
            let _x = snake[0].x;
            let _y = snake[0].y;
            snake_dir = snake_next_dir;   // read async event key
            // Direction 0 - Up, 1 - Right, 2 - Down, 3 - Left
            switch(snake_dir){
                case 0: _y--; break;
                case 1: _x++; break;
                case 2: _y++; break;
                case 3: _x--; break;
            }
            snake.pop(); // tail is removed
            snake.unshift({x: _x, y: _y}); // head is new in new position/orientation
            // Wall Checker
            if(wall === 1){
                // Wall on, Game over test
                if (snake[0].x < 0 || snake[0].x === canvas.width / BLOCK || snake[0].y < 0 || snake[0].y === canvas.height / BLOCK){
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            }else{
                // Wall Off, Circle around
                for(let i = 0, x = snake.length; i < x; i++){
                    if(snake[i].x < 0){
                        snake[i].x = snake[i].x + (canvas.width / BLOCK);
                    }
                    if(snake[i].x === canvas.width / BLOCK){
                        snake[i].x = snake[i].x - (canvas.width / BLOCK);
                    }
                    if(snake[i].y < 0){
                        snake[i].y = snake[i].y + (canvas.height / BLOCK);
                    }
                    if(snake[i].y === canvas.height / BLOCK){
                        snake[i].y = snake[i].y - (canvas.height / BLOCK);
                    }
                }
            }
            // Snake vs Snake checker
            for(let i = 1; i < snake.length; i++){
                // Game over test
                if (snake[0].x === snake[i].x && snake[0].y === snake[i].y){
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            }
            // Snake eats food checker
            if(checkBlock(snake[0].x, snake[0].y, food.x, food.y)){
                snake[snake.length] = {x: snake[0].x, y: snake[0].y};
                altScore(++score);
                addFood();
                activeDot(food.x, food.y);
            }
            // Repaint canvas
            ctx.beginPath();
            ctx.fillStyle = "royalblue";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            // Paint snake
            for(let i = 0; i < snake.length; i++){
                activeDot(snake[i].x, snake[i].y);
            }
            // Paint food
            activeDot(food.x, food.y);
            // Debug
            //document.getElementById("debug").innerHTML = snake_dir + " " + snake_next_dir + " " + snake[0].x + " " + snake[0].y;
            // Recursive call after speed delay, déjà vu
            setTimeout(mainLoop, snake_speed);
        }
        /* New Game setup */
        /////////////////////////////////////////////////////////////
        let newGame = function(){
            // snake game screen
            showScreen(SCREEN_SNAKE);
            screen_snake.focus();
            // game score to zero
            score = 0;
            altScore(score);
            // initial snake
            snake = [];
            snake.push({x: 0, y: 15});
            snake_next_dir = 1;
            // food on canvas
            addFood();
            // activate canvas event
            canvas.onkeydown = function(evt) {
                changeDir(evt.keyCode);
            }
            mainLoop();
        }
        /* Key Inputs and Actions */
        /////////////////////////////////////////////////////////////
        let changeDir = function(key){
            // test key and switch direction
            switch(key) {
                case 37:    // left arrow
                    if (snake_dir !== 1)    // not right
                        snake_next_dir = 3; // then switch left
                    break;
                case 38:    // up arrow
                    if (snake_dir !== 2)    // not down
                        snake_next_dir = 0; // then switch up
                    break;
                case 39:    // right arrow
                    if (snake_dir !== 3)    // not left
                        snake_next_dir = 1; // then switch right
                    break;
                case 40:    // down arrow
                    if (snake_dir !== 0)    // not up
                        snake_next_dir = 2; // then switch down
                    break;
            }
        }
        /* Dot for Food or Snake part */
        /////////////////////////////////////////////////////////////
        let activeDot = function(x, y){
            ctx.fillStyle = "#FFFFFF";
            ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
        }
        /* Random food placement */
        /////////////////////////////////////////////////////////////
        let addFood = function(){
            food.x = Math.floor(Math.random() * ((canvas.width / BLOCK) - 1));
            food.y = Math.floor(Math.random() * ((canvas.height / BLOCK) - 1));
            for(let i = 0; i < snake.length; i++){
                if(checkBlock(food.x, food.y, snake[i].x, snake[i].y)){
                    addFood();
                }
            }
        }
        /* Collision Detection */
        /////////////////////////////////////////////////////////////
        let checkBlock = function(x, y, _x, _y){
            return (x === _x && y === _y);
        }
        /* Update Score */
        /////////////////////////////////////////////////////////////
        let altScore = function(score_val){
            ele_score.innerHTML = String(score_val);
        }
        /////////////////////////////////////////////////////////////
        // Change the snake speed...
        // 150 = slow
        // 100 = normal
        // 50 = fast
        let setSnakeSpeed = function(speed_value){
            snake_speed = speed_value;
        }
        /////////////////////////////////////////////////////////////
        let setWall = function(wall_value){
            wall = wall_value;
            if(wall === 0){screen_snake.style.borderColor = "#606060";}
            if(wall === 1){screen_snake.style.borderColor = "#FFFFFF";}
        }
    })();
</script>
