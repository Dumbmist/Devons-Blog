---
layout: post
title: Hangman
course: hangman
menu: nav/home.html
---

# Harder than it looks
- There is a leaderboard though

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hangman</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #222; color: #fff; text-align: center; margin: 0; padding: 0; }
        .game-container { margin-top: 50px; }
        #word { font-size: 30px; letter-spacing: 10px; }
        #lives { font-size: 20px; }
        button { padding: 10px 20px; font-size: 20px; background-color: #444; border: none; color: #fff; cursor: pointer; }
        input { font-size: 20px; width: 200px; padding: 5px; text-align: center; }
        #guessedLetters { margin-top: 20px; }
        #lostWord { font-size: 20px; margin-top: 20px; color: #ff6666; }
        .leaderboard { margin-top: 30px; text-align: left; }
        .leaderboard ul { list-style-type: none; padding: 0; }
        .leaderboard li { padding: 5px; }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>Hangman</h1>
        <p id="word"></p>
        <p id="lives">Lives: 7</p>
        <input type="text" id="letterInput" maxlength="1">
        <button onclick="guessLetter()">Guess</button>
        <button onclick="startNewGame()">New Game</button>
        <p id="message"></p>
        <p>Guessed Letters: <span id="guessedLetters">None</span></p>
        <p id="lostWord"></p>
    </div>

    <div class="leaderboard">
        <h2>Leaderboard</h2>
        <ul id="leaderboardList"></ul>
    </div>

    <div class="name-container">
        <h2>Enter Your Name</h2>
        <input type="text" id="playerNameInput" placeholder="Enter your name">
        <button onclick="setPlayerName()">Submit</button>
    </div>

    <script>
        const words = ['elephant', 'android', 'symphony', 'geography', 'vaccine', 'courage', 'planet', 'fascinating', 'juxtapose', 'universe', 'remarkable', 'unravel', 'fantasy', 'microphone', 'perception', 'stamina', 'incredible', 'philosophy', 'serenity', 'vivid', 'innovation', 'celebration', 'epiphany', 'yeti', 'secret', 'monkwy', 'christmas', 'spanish', 'wizardry', 'indigo', 'journey', 'serendipity', 'odyssey', 'mystery', 'paradox', 'quixotic'];
        let selectedWord, guessedLetters, lives, playerName, winStreak;
        let leaderboard = JSON.parse(localStorage.getItem('leaderboard')) || [];
        const adminSecret = 'admin123';
        let gameStarted = false;

        function setPlayerName() {
            playerName = document.getElementById('playerNameInput').value.trim();
            if (playerName === adminSecret) {
                localStorage.clear();
                alert('Game state has been reset!');
                location.reload();
            } else if (playerName) {
                document.querySelector('.name-container').style.display = 'none';
                startNewGame();
            } else {
                alert('Please enter a name.');
            }
        }

        function startNewGame() {
            if (gameStarted) {
                resetGame();
                return;
            }

            selectedWord = words[Math.floor(Math.random() * words.length)];
            guessedLetters = [];
            lives = 7;
            document.getElementById('lives').textContent = `Lives: ${lives}`;
            document.getElementById('letterInput').disabled = false;
            document.getElementById('message').textContent = '';
            document.getElementById('lostWord').textContent = '';
            document.getElementById('letterInput').value = '';
            displayWord();
            document.getElementById('guessedLetters').textContent = 'None';
            gameStarted = true;
        }

        function displayWord() {
            let display = '';
            for (let i = 0; i < selectedWord.length; i++) {
                display += guessedLetters.includes(selectedWord[i]) ? selectedWord[i] : '_';
            }
            document.getElementById('word').textContent = display;
        }

        function guessLetter() {
            let input = document.getElementById('letterInput').value.toLowerCase();
            if (!input || guessedLetters.includes(input)) return;
            guessedLetters.push(input);

            if (!selectedWord.includes(input)) {
                lives--;
                document.getElementById('lives').textContent = `Lives: ${lives}`;
            }

            document.getElementById('guessedLetters').textContent = guessedLetters.join(', ');
            displayWord();
            document.getElementById('letterInput').value = '';

            if (lives === 0) {
                document.getElementById('message').textContent = 'Game Over!';
                document.getElementById('lostWord').textContent = `The word was: ${selectedWord}`;
                document.getElementById('letterInput').disabled = true;
                winStreak = 0;
                updateLeaderboard(false);
                askForNewName();
            } else if (!document.getElementById('word').textContent.includes('_')) {
                document.getElementById('message').textContent = 'You Win!';
                winStreak++;
                updateLeaderboard(true);
            }
        }

        function askForNewName() {
            document.querySelector('.name-container').style.display = 'block';
            document.getElementById('word').textContent = '';
            document.getElementById('guessedLetters').textContent = '';
            document.getElementById('message').textContent = '';
            document.getElementById('lostWord').textContent = '';
            document.getElementById('lives').textContent = 'Lives: 7';
            gameStarted = false;
        }

        function updateLeaderboard(isWin) {
            const playerIndex = leaderboard.findIndex(player => player.name === playerName);
            if (playerIndex >= 0) {
                if (isWin) {
                    leaderboard[playerIndex].streak++;
                } else {
                    leaderboard[playerIndex].streak = 0;
                }
            } else if (isWin) {
                leaderboard.push({ name: playerName, streak: 1 });
            }

            leaderboard = leaderboard.sort((a, b) => b.streak - a.streak).slice(0, 5);
            localStorage.setItem('leaderboard', JSON.stringify(leaderboard));

            displayLeaderboard();
        }

        function displayLeaderboard() {
            const leaderboardList = document.getElementById('leaderboardList');
            leaderboardList.innerHTML = '';
            leaderboard.forEach(player => {
                const li = document.createElement('li');
                li.textContent = `${player.name}: ${player.streak} Wins`;
                leaderboardList.appendChild(li);
            });
        }

        function resetGame() {
            selectedWord = words[Math.floor(Math.random() * words.length)];
            guessedLetters = [];
            lives = 7;
            document.getElementById('lives').textContent = `Lives: ${lives}`;
            document.getElementById('letterInput').disabled = false;
            document.getElementById('message').textContent = '';
            document.getElementById('lostWord').textContent = '';
            document.getElementById('letterInput').value = '';
            displayWord();
            document.getElementById('guessedLetters').textContent = 'None';
        }

        displayLeaderboard();
    </script>
</body>
</html>
