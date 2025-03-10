---
layout: post
title: Snake Game
course: snake
menu: nav/home.html
---

(USE WASD OR ARROW KEYS TO MOVE)
- WASD is smoother  - better for gameplay
- Try out the random walls extension (more difficult)
- The E key gives a slight speed boost for 5 seconds (there is a cooldown of 10s)
- Golden apple = 5 points

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


<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Snake score: <span id="score_value">0</span></p>
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
                <input id="speed1" type="radio" name="speed" value="120" checked/>
                <label for="speed1">Slow</label>
                <input id="speed2" type="radio" name="speed" value="75"/>
                <label for="speed2">Normal</label>
                <input id="speed3" type="radio" name="speed" value="35"/>
                <label for="speed3">Fast</label>
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
            ctx.fillStyle = "#000000 ";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            // Paint snake
            for(let i = 0; i < snake.length; i++){
                activeDot(snake[i].x, snake[i].y);
            }
            // Paint food
            activeDot(food.x, food.y, true);
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
                case 65:
                case 37:     
                    if (snake_dir !== 1)    // not right
                        snake_next_dir = 3; // then switch left
                    break;
                case 87:
                case 38:    
                    if (snake_dir !== 2)    // not down
                        snake_next_dir = 0; // then switch up
                    break;
                case 68:
                case 39:     
                    if (snake_dir !== 3)    // not left
                        snake_next_dir = 1; // then switch right
                    break;
                case 83:
                case 40:    
                    if (snake_dir !== 0)    // not up
                        snake_next_dir = 2; // then switch down
                    break;
            }
        }
        /* Dot for Food or Snake part */
        /////////////////////////////////////////////////////////////
        let activeDot = function(x, y, isFood = false){
            let snakeLength = snake.length;

            let color = "#00FF00";
            if (!isFood) {

                const hue = (snakeLength * 30) % 360;
                color = `hsl(${hue}, 100%, 50%)`;
            }

            ctx.fillStyle = isFood ? "#FF0000" : color; 
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

        const randomWallSettingHTML = `
            <p>Random Walls:
                <input id="randomWallOn" type="radio" name="randomWall" value="1"/>
                <label for="randomWallOn">On</label>
                <input id="randomWallOff" type="radio" name="randomWall" value="0" checked/>
                <label for="randomWallOff">Off</label>
            </p>`;

        document.getElementById("setting").innerHTML += randomWallSettingHTML;

        let randomWalls = [];
        let randomWallActive = false;

        const generateRandomWalls = function() {
            randomWalls = [];
            const wallCount = Math.floor(Math.random() * 8) + 10; 
            for (let i = 0; i < wallCount; i++) {
                const clusterSize = Math.floor(Math.random() * 5) + 3;
                const startX = Math.floor(Math.random() * (canvas.width / BLOCK));
                const startY = Math.floor(Math.random() * (canvas.height / BLOCK));
                const direction = Math.random() > 0.5 ? 'horizontal' : 'vertical';

                for (let j = 0; j < clusterSize; j++) {
                    let wallX = startX;
                    let wallY = startY;

                    if (direction === 'horizontal') {
                        wallX += j;
                    } else {
                        wallY += j;
                    }

                    if (wallX < canvas.width / BLOCK && wallY < canvas.height / BLOCK) {
                        randomWalls.push({ x: wallX, y: wallY });
                    }
                }
            }
        };

        const drawRandomWalls = function() {
            ctx.fillStyle = "#FFFFFF";
            for (let wall of randomWalls) {
                ctx.fillRect(wall.x * BLOCK, wall.y * BLOCK, BLOCK, BLOCK);
            }
        };

        const checkWallCollision = function() {
            for (let wall of randomWalls) {
                if (checkBlock(snake[0].x, snake[0].y, wall.x, wall.y)) {
                    showScreen(SCREEN_GAME_OVER);
                    return true;
                }
            }
            return false;
        };

        // Bug fixes - no apples in walls
        const spawnApple = function() {
            do {
                apple.x = Math.floor(Math.random() * (canvas.width / BLOCK));
                apple.y = Math.floor(Math.random() * (canvas.height / BLOCK));
            } while (randomWalls.some(wall => wall.x === apple.x && wall.y === apple.y));
        };

        const originalMainLoop = mainLoop;
        mainLoop = function() {
            if (randomWallActive && checkWallCollision()) return;

            originalMainLoop();

            if (randomWallActive) drawRandomWalls();
        };

        const randomWallSetting = document.getElementsByName("randomWall");
        for (let i = 0; i < randomWallSetting.length; i++) {
            randomWallSetting[i].addEventListener("click", function() {
                for (let j = 0; j < randomWallSetting.length; j++) {
                    if (randomWallSetting[j].checked) {
                        randomWallActive = randomWallSetting[j].value === "1";
                        if (randomWallActive) generateRandomWalls();
                    }
                }
            });
        }

        // Reset hopefully
        const originalNewGame = newGame;
        newGame = function() {
            if (randomWallActive) generateRandomWalls(); 
            originalNewGame();
        };

        let speedBoostActive = false;
        let boostCooldown = false;

        const activateSpeedBoost = function() {
            if (!boostCooldown && !speedBoostActive) {
                speedBoostActive = true;
                setSnakeSpeed(75);

                setTimeout(function() {
                    speedBoostActive = false;
                    setSnakeSpeed(150); 
                    boostCooldown = true;

                    setTimeout(function() {
                        boostCooldown = false;
                    }, 10000); 
                }, 5000); 
            }
        };

        window.addEventListener("keydown", function(evt) {
            if (evt.code === "KeyE") {
                activateSpeedBoost();
            }
        }, false);

        let goldenApple = null;
        let goldenAppleTimer = null;

        function spawnGoldenApple() {
            do {
                goldenApple = {
                    x: Math.floor(Math.random() * (canvas.width / BLOCK)),
                    y: Math.floor(Math.random() * (canvas.height / BLOCK))
                };
            } while (
                snake.some(segment => segment.x === goldenApple.x && segment.y === goldenApple.y) ||
                checkBlock(food.x, food.y, goldenApple.x, goldenApple.y)
            );

            goldenAppleTimer = setTimeout(() => goldenApple = null, 10000);
        }

        function drawGoldenApple() {
            if (goldenApple) {
                ctx.fillStyle = "#FFD700";
                ctx.beginPath();
                ctx.arc(
                    goldenApple.x * BLOCK + BLOCK / 2,
                    goldenApple.y * BLOCK + BLOCK / 2,
                    BLOCK / 2,
                    0,
                    Math.PI * 2
                );
                ctx.fill();
            }
        }

        const originalGameLoop = mainLoop;
        mainLoop = function() {
            originalGameLoop();

            if (goldenApple && snake[0].x === goldenApple.x && snake[0].y === goldenApple.y) {
                score += 5; 
                altScore(score); 
                snake.push({ ...snake[snake.length - 1] }); 
                goldenApple = null; 
                clearTimeout(goldenAppleTimer);
            }

            drawGoldenApple();
        };

        setInterval(() => {
            if (!goldenApple) spawnGoldenApple();
        }, 15000);

    })();
</script>