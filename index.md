---
layout: base
title: Student Home 
description: Home Page
hide: true
---

## **Mihir Thaha's AP CSP Project**
My CSP journey starts here.
  
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <canvas id="gameCanvas" width="400" height="400"></canvas>
    <script src="script.js"></script>
</body>
</html>

/* style.css */
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f0f0f0;
}

canvas {
    border: 1px solid #000;
}


// script.js

const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

const box = 20;
const canvasSize = 400;
const canvasPixels = canvasSize / box;

let snake = [{ x: 9 * box, y: 9 * box }];
let food = {
    x: Math.floor(Math.random() * canvasPixels) * box,
    y: Math.floor(Math.random() * canvasPixels) * box
};
let score = 0;
let direction = 'RIGHT';
let isChangingDirection = false;

document.addEventListener('keydown', changeDirection);

function changeDirection(event) {
    if (isChangingDirection) return;
    isChangingDirection = true;

    const key = event.keyCode;
    const goingUp = direction === 'UP';
    const goingDown = direction === 'DOWN';
    const goingRight = direction === 'RIGHT';
    const goingLeft = direction === 'LEFT';

    if (key === 37 && !goingRight) {
        direction = 'LEFT';
    }
    if (key === 38 && !goingDown) {
        direction = 'UP';
    }
    if (key === 39 && !goingLeft) {
        direction = 'RIGHT';
    }
    if (key === 40 && !goingUp) {
        direction = 'DOWN';
    }
}

function drawGame() {
    if (hasGameEnded()) return;

    isChangingDirection = false;

    ctx.clearRect(0, 0, canvasSize, canvasSize);

    drawFood();
    moveSnake();
    drawSnake();

    setTimeout(drawGame, 100);
}

function drawSnake() {
    ctx.fillStyle = 'green';
    ctx.strokeStyle = 'darkgreen';

    snake.forEach((snakePart) => {
        ctx.fillRect(snakePart.x, snakePart.y, box, box);
        ctx.strokeRect(snakePart.x, snakePart.y, box, box);
    });
}

function drawFood() {
    ctx.fillStyle = 'red';
    ctx.fillRect(food.x, food.y, box, box);
}

function moveSnake() {
    const head = { x: snake[0].x, y: snake[0].y };

    if (direction === 'LEFT') head.x -= box;
    if (direction === 'UP') head.y -= box;
    if (direction === 'RIGHT') head.x += box;
    if (direction === 'DOWN') head.y += box;

    snake.unshift(head);

    if (head.x === food.x && head.y === food.y) {
        score += 1;
        food = {
            x: Math.floor(Math.random() * canvasPixels) * box,
            y: Math.floor(Math.random() * canvasPixels) * box
        };
    } else {
        snake.pop();
    }
}

function hasGameEnded() {
    for (let i = 4; i < snake.length; i++) {
        const hasCollided = snake[i].x === snake[0].x && snake[i].y === snake[0].y;
        if (hasCollided) return true;
    }

    const hitLeftWall = snake[0].x < 0;
    const hitRightWall = snake[0].x >= canvasSize;
    const hitTopWall = snake[0].y < 0;
    const hitBottomWall = snake[0].y >= canvasSize;

    return hitLeftWall || hitRightWall || hitTopWall || hitBottomWall;
}

drawGame();

