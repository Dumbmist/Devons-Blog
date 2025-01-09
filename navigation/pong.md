---
layout: post
title: Pong
course: pong
menu: nav/home.html
---

## Multiplayer
- Use WASD to control the left bar and IJKL to control the right

## Regular
- WASD controls the bar (up and down so just W and A)

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Classic Pong</title>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            height: 100vh;
            background-color: #FFF;
        }
        canvas {
            border: 2px solid #fff;
            background-color: #111;
        }
        .controls {
            margin-top: 20px;
        }
        button {
            padding: 10px 20px;
            margin: 0 10px;
            font-size: 16px;
            cursor: pointer;
            background-color: #444;
            color: #fff;
            border: 2px solid #fff;
            border-radius: 5px;
        }
        button:active {
            background-color: #666;
        }
        .settings-menu {
            display: none;
            flex-direction: column;
            align-items: center;
            background: #222;
            padding: 20px;
            border: 2px solid #fff;
            color: #fff;
        }
        .settings-menu button {
            margin: 10px 0;
            background-color: #555;
            color: #fff;
            border: 2px solid #fff;
        }
    </style>
</head>
<body>
    <canvas id="pong" width="600" height="400"></canvas>
    <div class="controls">
        <button id="newGame">New Game</button>
        <button id="settings">Settings</button>
    </div>
    <div id="settingsMenu" class="settings-menu">
        <h2>Settings</h2>
        <div>
            <p>Ball Speed:</p>
            <button class="speed" data-speed="4">Normal</button>
            <button class="speed" data-speed="6">Fast</button>
            <button class="speed" data-speed="8">Extra Fast</button>
        </div>
        <div>
            <p>Game Mode:</p>
            <button id="singlePlayer">Single Player</button>
            <button id="multiPlayer">Multiplayer</button>
        </div>
        <button id="closeSettings">Close</button>
    </div>

    <script>
        const canvas = document.getElementById('pong');
        const ctx = canvas.getContext('2d');
        const newGameButton = document.getElementById('newGame');
        const settingsButton = document.getElementById('settings');
        const settingsMenu = document.getElementById('settingsMenu');
        const closeSettingsButton = document.getElementById('closeSettings');
        const speedButtons = document.querySelectorAll('.speed');
        const singlePlayerButton = document.getElementById('singlePlayer');
        const multiPlayerButton = document.getElementById('multiPlayer');

        const paddleWidth = 10;
        const paddleHeight = 75;
        const ballSize = 10;
        let multiplayer = false;
        let gameRunning = false;
        let ballSpeed = 4;

        const player = { x: 0, y: canvas.height / 2 - paddleHeight / 2, score: 0, dy: 0, keys: { up: false, down: false } };
        const computer = { x: canvas.width - paddleWidth, y: canvas.height / 2 - paddleHeight / 2, score: 0, dy: 0, keys: { up: false, down: false } };

        const ball = {
            x: canvas.width / 2,
            y: canvas.height / 2,
            vx: ballSpeed * (Math.random() > 0.5 ? 1 : -1),
            vy: ballSpeed * (Math.random() > 0.5 ? 1 : -1),
        };

        function drawRect(x, y, width, height, color) {
            ctx.fillStyle = color;
            ctx.fillRect(x, y, width, height);
        }

        function drawText(text, x, y, color) {
            ctx.fillStyle = color;
            ctx.font = '20px Arial';
            ctx.fillText(text, x, y);
        }

        function gameLoop() {
            if (gameRunning) {
                update();
                render();
            }
            requestAnimationFrame(gameLoop);
        }

        function update() {
            player.y = Math.max(Math.min(player.y + player.dy, canvas.height - paddleHeight), 0);
            if (multiplayer) {
                computer.y = Math.max(Math.min(computer.y + computer.dy, canvas.height - paddleHeight), 0);
            }

            ball.x += ball.vx;
            ball.y += ball.vy;

            if (ball.y <= 0 || ball.y + ballSize >= canvas.height) {
                ball.vy *= -1;
            }

            if (
                (ball.x <= player.x + paddleWidth && ball.y + ballSize >= player.y && ball.y <= player.y + paddleHeight) ||
                (ball.x + ballSize >= computer.x && ball.y + ballSize >= computer.y && ball.y <= computer.y + paddleHeight)
            ) {
                ball.vx *= -1;
            }

            if (ball.x <= 0) {
                computer.score++;
                resetBall();
            } else if (ball.x + ballSize >= canvas.width) {
                player.score++;
                resetBall();
            }

            if (!multiplayer) {
                computer.y += (ball.y - (computer.y + paddleHeight / 2)) * 0.1;
                computer.y = Math.max(Math.min(computer.y, canvas.height - paddleHeight), 0);
            }
        }

        function render() {
            drawRect(0, 0, canvas.width, canvas.height, '#111');
            drawRect(player.x, player.y, paddleWidth, paddleHeight, '#fff');
            drawRect(computer.x, computer.y, paddleWidth, paddleHeight, '#fff');
            drawRect(ball.x, ball.y, ballSize, ballSize, '#fff');
            drawText(player.score, canvas.width / 4, 30, '#fff');
            drawText(computer.score, (canvas.width * 3) / 4, 30, '#fff');
        }

        function resetBall() {
            ball.x = canvas.width / 2;
            ball.y = canvas.height / 2;
            ball.vx = ballSpeed * (Math.random() > 0.5 ? 1 : -1);
            ball.vy = ballSpeed * (Math.random() > 0.5 ? 1 : -1);
        }

        document.addEventListener('keydown', (e) => {
            if (e.key === 'w' && !player.keys.up) {
                player.dy = -4;
                player.keys.up = true;
            } else if (e.key === 's' && !player.keys.down) {
                player.dy = 4;
                player.keys.down = true;
            }

            if (multiplayer) {
                if (e.key === 'i' && !computer.keys.up) {
                    computer.dy = -4;
                    computer.keys.up = true;
                } else if (e.key === 'k' && !computer.keys.down) {
                    computer.dy = 4;
                    computer.keys.down = true;
                }
            }
        });

        document.addEventListener('keyup', (e) => {
            if (e.key === 'w') {
                player.dy = player.keys.down ? 4 : 0;
                player.keys.up = false;
            } else if (e.key === 's') {
                player.dy = player.keys.up ? -4 : 0;
                player.keys.down = false;
            }

            if (multiplayer) {
                if (e.key === 'i') {
                    computer.dy = computer.keys.down ? 4 : 0;
                    computer.keys.up = false;
                } else if (e.key === 'k') {
                    computer.dy = computer.keys.up ? -4 : 0;
                    computer.keys.down = false;
                }
            }
        });

        newGameButton.addEventListener('click', () => {
            player.score = 0;
            computer.score = 0;
            resetBall();
            gameRunning = true;
        });

        settingsButton.addEventListener('click', () => {
            settingsMenu.style.display = 'flex';
        });

        closeSettingsButton.addEventListener('click', () => {
            settingsMenu.style.display = 'none';
        });

        speedButtons.forEach((button) => {
            button.addEventListener('click', () => {
                ballSpeed = parseInt(button.dataset.speed);
                alert(`Ball speed set to ${button.innerText}`);
            });
        });

        singlePlayerButton.addEventListener('click', () => {
            multiplayer = false;
            alert('Mode set to Single Player');
        });

        multiPlayerButton.addEventListener('click', () => {
            multiplayer = true;
            alert('Mode set to Multiplayer');
        });

        gameLoop();
    </script>
</body>
</html>
