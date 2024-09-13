---
layout: page
title: Snake
description: This is my Snake Game
permalink: /snake/
---

{% include nav/home.html %}

Home of My Snake


You can play the Snake Game right here!
- Use arrow keys to control the snake.
- Try to eat the green food to grow longer.
- Avoid hitting the walls or yourself.

<div id="gameContainer">
    <canvas id="snakeGame" width="400" height="400"></canvas>
</div>

<script>
    // JavaScript Snake Game Code
    const canvas = document.getElementById("snakeGame");
    const ctx = canvas.getContext("2d");

    let snake = [{ x: 200, y: 200 }];
    let direction = { x: 10, y: 0 };
    let food = { x: Math.floor(Math.random() * 40) * 10, y: Math.floor(Math.random() * 40) * 10 };
    let score = 0;

    document.addEventListener("keydown", changeDirection);

    function gameLoop() {
        if (checkGameOver()) return;

        clearCanvas();
        moveSnake();
        drawFood();
        drawSnake();
        setTimeout(gameLoop, 100);
    }

    function clearCanvas() {
    // Change the background color to your desired color (e.g., light blue)
    ctx.fillStyle = "#ADD8E6";  // Light blue background
    ctx.fillRect(0, 0, canvas.width, canvas.height);  // Fill the entire canvas with the background color
}


    function drawSnake() {
        snake.forEach(part => {
            ctx.fillStyle = "green";
            ctx.fillRect(part.x, part.y, 10, 10);
        });
    }

    function moveSnake() {
        const head = { x: snake[0].x + direction.x, y: snake[0].y + direction.y };
        snake.unshift(head);

        if (head.x === food.x && head.y === food.y) {
            score++;
            food = { x: Math.floor(Math.random() * 40) * 10, y: Math.floor(Math.random() * 40) * 10 };
        } else {
            snake.pop();
        }
    }

    function drawFood() {
        ctx.fillStyle = "red";
        ctx.fillRect(food.x, food.y, 10, 10);
    }

    function changeDirection(event) {
        const key = event.keyCode;
        if (key === 37 && direction.x === 0) { direction = { x: -10, y: 0 }; }
        if (key === 38 && direction.y === 0) { direction = { x: 0, y: -10 }; }
        if (key === 39 && direction.x === 0) { direction = { x: 10, y: 0 }; }
        if (key === 40 && direction.y === 0) { direction = { x: 0, y: 10 }; }
    }

    function checkGameOver() {
        const head = snake[0];
        const hitWall = head.x < 0 || head.x >= canvas.width || head.y < 0 || head.y >= canvas.height;
        const hitSelf = snake.slice(1).some(part => part.x === head.x && part.y === head.y);

        if (hitWall || hitSelf) {
            ctx.fillStyle = "black";
            ctx.font = "20px Arial";
            ctx.fillText("Game Over!", canvas.width / 2 - 50, canvas.height / 2);
            return true;
        }
        return false;
    }

    gameLoop();
</script>
