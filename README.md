<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Joanna's Ultimate Minigames: Hearts & Rainbows 🌈❤️</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary-gradient: linear-gradient(135deg, #ff6b9d, #c44569, #ff9a9e, #fecfef);
      --secondary-gradient: linear-gradient(135deg, #a8edea, #fed6e3, #ff9a9e);
      --accent-color: #ff66cc;
      --text-light: #ffffff;
      --text-dark: #333333;
      --shadow-soft: 0 8px 32px rgba(0, 0, 0, 0.1);
      --shadow-glow: 0 0 20px rgba(255, 102, 204, 0.5);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Poppins', sans-serif;
      color: var(--text-light);
      background: var(--primary-gradient);
      background-size: 400% 400%;
      animation: gradientShift 15s ease infinite;
      overflow-x: hidden;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      position: relative;
    }

    @keyframes gradientShift {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    /* Enhanced Floating Hearts */
    .hearts-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 1;
    }

    .heart {
      position: absolute;
      font-size: clamp(1rem, 2vw, 2rem);
      color: var(--accent-color);
      animation: floatUp 6s linear infinite, sparkle 2s ease-in-out infinite alternate;
      opacity: 0.8;
      text-shadow: 0 0 10px currentColor;
    }

    @keyframes floatUp {
      0% {
        transform: translateY(100vh) rotate(0deg) scale(0.5);
        opacity: 0;
      }
      10% {
        opacity: 1;
      }
      90% {
        opacity: 1;
      }
      100% {
        transform: translateY(-10vh) rotate(360deg) scale(1.5);
        opacity: 0;
      }
    }

    @keyframes sparkle {
      0% { filter: drop-shadow(0 0 5px currentColor); }
      100% { filter: drop-shadow(0 0 15px currentColor); }
    }

    header {
      text-align: center;
      padding: 2rem;
      font-size: clamp(1.5rem, 4vw, 3rem);
      font-weight: 700;
      background: rgba(0, 0, 0, 0.2);
      backdrop-filter: blur(10px);
      width: 100%;
      z-index: 10;
      position: relative;
      animation: glow 3s ease-in-out infinite alternate;
    }

    @keyframes glow {
      0% { text-shadow: 0 0 10px var(--accent-color); }
      100% { text-shadow: 0 0 20px var(--accent-color), 0 0 30px var(--accent-color); }
    }

    nav {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 1rem;
      padding: 2rem;
      z-index: 10;
    }

    nav button {
      padding: 1rem 2rem;
      font-size: 1.1rem;
      font-weight: 600;
      border: none;
      border-radius: 50px;
      cursor: pointer;
      background: var(--secondary-gradient);
      color: var(--text-light);
      box-shadow: var(--shadow-soft);
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      position: relative;
      overflow: hidden;
    }

    nav button::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
      transition: left 0.5s;
    }

    nav button:hover::before {
      left: 100%;
    }

    nav button:hover {
      transform: translateY(-5px) scale(1.05);
      box-shadow: var(--shadow-glow);
    }

    .game-container {
      display: none;
      max-width: 90vw;
      margin: 2rem auto;
      padding: 2rem;
      background: rgba(255, 255, 255, 0.95);
      border-radius: 20px;
      box-shadow: var(--shadow-soft);
      position: relative;
      z-index: 5;
      color: var(--text-dark);
      backdrop-filter: blur(10px);
      animation: slideIn 0.5s ease-out;
    }

    @keyframes slideIn {
      from { opacity: 0; transform: translateY(50px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .game-container.active {
      display: block;
    }

    .score-board {
      display: flex;
      justify-content: space-around;
      margin-bottom: 1rem;
      padding: 1rem;
      background: var(--secondary-gradient);
      border-radius: 10px;
      color: var(--text-light);
      font-weight: 600;
    }

    /* Snake Game */
    #snakeCanvas {
      border: 3px solid var(--accent-color);
      border-radius: 10px;
      background: #000;
      display: block;
      margin: 0 auto;
    }

    /* Tic Tac Toe */
    #ticTacToe {
      margin: 0 auto;
      border-collapse: collapse;
    }

    #ticTacToe td {
      width: 100px;
      height: 100px;
      text-align: center;
      vertical-align: middle;
      font-size: 3rem;
      font-weight: bold;
      border: 3px solid var(--accent-color);
      cursor: pointer;
      transition: background 0.2s;
      background: rgba(255, 255, 255, 0.8);
    }

    #ticTacToe td:hover {
      background: rgba(255, 102, 204, 0.1);
    }

    /* Memory Game */
    #memory {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
      gap: 1rem;
      max-width: 600px;
      margin: 0 auto;
    }

    .memory-card {
      aspect-ratio: 1;
      font-size: 2rem;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      background: var(--secondary-gradient);
      color: transparent;
      transition: all 0.3s;
      box-shadow: var(--shadow-soft);
      position: relative;
    }

    .memory-card.flipped {
      background: rgba(255, 255, 255, 0.9);
      color: var(--text-dark);
      transform: rotateY(180deg);
    }

    .memory-card.matched {
      background: var(--primary-gradient);
      cursor: default;
    }

    /* RPS */
    #rps {
      text-align: center;
    }

    #rps button {
      font-size: 3rem;
      margin: 1rem;
      padding: 1rem;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      background: var(--secondary-gradient);
      color: var(--text-light);
      box-shadow: var(--shadow-soft);
      transition: all 0.3s;
    }

    #rps button:hover {
      transform: scale(1.1);
      box-shadow: var(--shadow-glow);
    }

    #rpsResult {
      font-size: 1.5rem;
      margin-top: 1rem;
      padding: 1rem;
      background: rgba(0, 0, 0, 0.1);
      border-radius: 10px;
    }

    /* Music Controls */
    #musicControls {
      position: fixed;
      bottom: 1rem;
      left: 1rem;
      z-index: 20;
      display: flex;
      gap: 1rem;
      align-items: center;
    }

    #playMusicBtn, #pauseMusicBtn {
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 20px;
      cursor: pointer;
      background: var(--accent-color);
      color: var(--text-light);
      font-weight: 600;
      transition: all 0.3s;
    }

    #playMusicBtn:hover, #pauseMusicBtn:hover {
      transform: scale(1.05);
      box-shadow: var(--shadow-glow);
    }

    /* Responsive */
    @media (max-width: 768px) {
      nav {
        flex-direction: column;
        align-items: center;
      }

      #ticTacToe td {
        width: 80px;
        height: 80px;
        font-size: 2rem;
      }

      #memory {
        grid-template-columns: repeat(4, 1fr);
      }
    }

    /* Win Modal */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.7);
      z-index: 100;
      justify-content: center;
      align-items: center;
    }

    .modal-content {
      background: var(--secondary-gradient);
      padding: 2rem;
      border-radius: 20px;
      text-align: center;
      color: var(--text-light);
      box-shadow: var(--shadow-glow);
      animation: bounceIn 0.5s;
    }

    @keyframes bounceIn {
      0% { transform: scale(0.3); opacity: 0; }
      50% { transform: scale(1.05); }
      70% { transform: scale(0.9); }
      100% { transform: scale(1); opacity: 1; }
    }

    .modal h2 {
      margin-bottom: 1rem;
      font-size: 2rem;
    }

    .modal button {
      padding: 0.8rem 1.5rem;
      margin: 0.5rem;
      border: none;
      border-radius: 20px;
      background: var(--accent-color);
      color: var(--text-light);
      cursor: pointer;
      font-size: 1rem;
      transition: all 0.3s;
    }

    .modal button:hover {
      transform: translateY(-2px);
      box-shadow: var(--shadow-glow);
    }
  </style>
</head>
<body>
  <div class="hearts-container" id="heartsContainer"></div>

  <header>Joanna's Ultimate Minigames: Hearts & Rainbows 🌈❤️</header>

  <nav>
    <button onclick="showGame('snake')">🐍 Snake</button>
    <button onclick="showGame('tictactoe')">❌⭕ Tic Tac Toe</button>
    <button onclick="showGame('memory')">🃏 Memory Flip</button>
    <button onclick="showGame('rps')">✊✋✌ Rock Paper Scissors</button>
  </nav>

  <!-- Snake Game -->
  <div id="snakeContainer" class="game-container">
    <div class="score-board">
      <span>Score: <span id="snakeScore">0</span></span>
    </div>
    <canvas id="snakeCanvas" width="400" height="400"></canvas>
  </div>

  <!-- Tic Tac Toe -->
  <div id="tictactoeContainer" class="game-container">
    <div class="score-board">
      <span>X Wins: <span id="xWins">0</span></span>
      <span>O Wins: <span id="oWins">0</span></span>
    </div>
    <table id="ticTacToe"></table>
  </div>

  <!-- Memory Game -->
  <div id="memoryContainer" class="game-container">
    <div class="score-board">
      <span>Flips: <span id="memoryFlips">0</span></span>
      <span>Time: <span id="memoryTime">0</span>s</span>
    </div>
    <div id="memory"></div>
    <button onclick="resetMemory()" style="margin-top: 1rem; padding: 0.5rem 1rem; background: var(--accent-color); color: white; border: none; border-radius: 10px; cursor: pointer;">Reset</button>
  </div>

  <!-- Rock Paper Scissors -->
  <div id="rpsContainer" class="game-container">
    <div class="score-board">
      <span>Your Wins: <span id="playerWins">0</span></span>
      <span>AI Wins: <span id="aiWins">0</span></span>
    </div>
    <div id="rps">
      <p>Choose your move:</p>
      <button onclick="rpsPlay('rock')">✊ Rock</button>
      <button onclick="rpsPlay('paper')">✋ Paper</button>
      <button onclick="rpsPlay('scissors')">✌ Scissors</button>
      <p id="rpsResult"></p>
    </div>
    <button onclick="resetRPS()" style="margin-top: 1rem; padding: 0.5rem 1rem; background: var(--accent-color); color: white; border: none; border-radius: 10px; cursor: pointer;">Reset Scores</button>
  </div>

  <!-- Win Modal -->
  <div id="winModal" class="modal">
    <div class="modal-content">
      <h2 id="modalTitle">Victory!</h2>
      <p id="modalMessage"></p>
      <button onclick="closeModal()">Play Again</button>
      <button onclick="showMenu()">Menu</button>
    </div>
  </div>

  <!-- Music Controls -->
  <div id="musicControls">
    <button id="playMusicBtn">▶ Play Phonk</button>
    <button id="pauseMusicBtn" style="display: none;">⏸ Pause</button>
  </div>
  <audio id="bgMusic" loop preload="auto">
    <source src="https://cdn.pixabay.com/audio/2023/05/01/audio_d2a6a36c3b.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>

  <script>
    // Global variables
    let currentGame = null;
    let music = document.getElementById('bgMusic');
    let playBtn = document.getElementById('playMusicBtn');
    let pauseBtn = document.getElementById('pauseMusicBtn');
    let modal = document.getElementById('winModal');

    // Automatic Phonk Playback Attempt
    window.addEventListener('load', () => {
      music.volume = 0.5; // Set volume to 50%
      const playPromise = music.play();
      if (playPromise !== undefined) {
        playPromise.then(() => {
          console.log('Phonk autoplay started');
          playBtn.style.display = 'none';
          pauseBtn.style.display = 'inline-block';
        }).catch(error => {
          console.log('Autoplay prevented:', error);
          playBtn.style.display = 'inline-block';
          pauseBtn.style.display = 'none';
        });
      }
    });

    // Music Controls
    playBtn.onclick = () => {
      music.play();
      playBtn.style.display = 'none';
      pauseBtn.style.display = 'inline-block';
    };

    pauseBtn.onclick = () => {
      music.pause();
      pauseBtn.style.display = 'none';
      playBtn.style.display = 'inline-block';
    };

    // Enhanced Floating Hearts
    function spawnHeart() {
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.animationDuration = (4 + Math.random() * 4) + 's';
      heart.innerHTML = ['❤️', '💖', '💕', '💗'][Math.floor(Math.random() * 4)];
      document.getElementById('heartsContainer').appendChild(heart);
      setTimeout(() => heart.remove(), 8000);
    }
    setInterval(spawnHeart, 800);

    // Game Switching
    function showGame(game) {
      document.querySelectorAll('.game-container').forEach(container => container.classList.remove('active'));
      document.getElementById(game + 'Container').classList.add('active');
      currentGame = game;
      if (game === 'snake') startSnake();
      if (game === 'tictactoe') startTicTacToe();
      if (game === 'memory') startMemory();
      if (game === 'rps') resetRPS(); // Refresh RPS
    }

    function showMenu() {
      document.querySelectorAll('.game-container').forEach(container => container.classList.remove('active'));
      currentGame = null;
    }

    function closeModal() {
      modal.style.display = 'none';
      if (currentGame) {
        if (currentGame === 'tictactoe') startTicTacToe();
        if (currentGame === 'memory') startMemory();
        if (currentGame === 'snake') startSnake();
      }
    }

    // Snake Game Enhanced
    let snakeCanvas = document.getElementById('snakeCanvas');
    let ctx = snakeCanvas.getContext('2d');
    let snake = [{x: 200, y: 200}];
    let dx = 20, dy = 0;
    let food = {};
    let snakeInterval;
    let snakeScore = 0;

    function startSnake() {
      clearInterval(snakeInterval);
      snake = [{x: 200, y: 200}];
      dx = 20; dy = 0;
      snakeScore = 0;
      updateScore('snake', 0);
      food = randomFood();
      snakeInterval = setInterval(drawSnake, 150);
      document.addEventListener('keydown', changeDirection);
    }

    function drawSnake() {
      ctx.clearRect(0, 0, 400, 400);
      // Draw snake with gradient
      snake.forEach((part, index) => {
        ctx.fillStyle = `hsl(${120 - index * 2}, 100%, 50%)`;
        ctx.fillRect(part.x, part.y, 20, 20);
        ctx.strokeStyle = '#fff';
        ctx.strokeRect(part.x, part.y, 20, 20);
      });
      // Draw food
      ctx.fillStyle = '#ff0000';
      ctx.beginPath();
      ctx.arc(food.x + 10, food.y + 10, 10, 0, 2 * Math.PI);
      ctx.fill();
      let head = {x: snake[0].x + dx, y: snake[0].y + dy};
      snake.unshift(head);
      if (head.x === food.x && head.y === food.y) {
        snakeScore += 10;
        updateScore('snake', snakeScore);
        food = randomFood();
      } else {
        snake.pop();
      }
      // Collision detection
      if (head.x < 0 || head.y < 0 || head.x >= 400 || head.y >= 400 || snake.slice(1).some(p => p.x === head.x && p.y === head.y)) {
        clearInterval(snakeInterval);
        showWinModal('Game Over! Final Score: ' + snakeScore, 'snake');
        document.removeEventListener('keydown', changeDirection);
      }
    }

    function changeDirection(e) {
      const LEFT = 37, UP = 38, RIGHT = 39, DOWN = 40;
      if ((e.keyCode === LEFT && dx !== 20) || (e.keyCode === RIGHT && dx !== -20)) { dx = e.keyCode === LEFT ? -20 : 20; dy = 0; }
      if ((e.keyCode === UP && dy !== 20) || (e.keyCode === DOWN && dy !== -20)) { dx = 0; dy = e.keyCode === UP ? -20 : 20; }
    }

    function randomFood() {
      return {x: Math.floor(Math.random() * 20) * 20, y: Math.floor(Math.random() * 20) * 20};
    }

    // Tic Tac Toe Enhanced
    let board = [], currentPlayer = 'X', xWins = 0, oWins = 0;

    function startTicTacToe() {
      board = [['', '', ''], ['', '', ''], ['', '', '']];
      currentPlayer = 'X';
      updateScore('x', xWins);
      updateScore('o', oWins);
      let table = document.getElementById('ticTacToe');
      table.innerHTML = '';
      for (let i = 0; i < 3; i++) {
        let row = document.createElement('tr');
        for (let j = 0; j < 3; j++) {
          let cell = document.createElement('td');
          cell.onclick = () => makeMove(i, j, cell);
          row.appendChild(cell);
        }
        table.appendChild(row);
      }
    }

    function makeMove(i, j, cell) {
      if (board[i][j] === '') {
        board[i][j] = currentPlayer;
        cell.textContent = currentPlayer;
        cell.style.color = currentPlayer === 'X' ? '#ff0000' : '#0000ff';
        if (checkWin()) {
          if (currentPlayer === 'X') xWins++; else oWins++;
          updateScore('x', xWins);
          updateScore('o', oWins);
          showWinModal(currentPlayer + ' Wins!', 'tictactoe');
        } else if (board.flat().every(x => x !== '')) {
          showWinModal('It\'s a Draw!', 'tictactoe');
        } else {
          currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
        }
      }
    }

    function checkWin() {
      const wins = [
        [0,1,2], [3,4,5], [6,7,8],
        [0,3,6], [1,4,7], [2,5,8],
        [0,4,8], [2,4,6]
      ];
      for (let win of wins) {
        let [a, b, c] = [win[0]%3, win[0]%3 + (win[1]%3)*3, wait no, better flat index
        actually:
      for (let i = 0; i < 3; i++) {
        if (board[i][0] && board[i][0] === board[i][1] && board[i][1] === board[i][2]) return true;
        if (board[0][i] && board[0][i] === board[1][i] && board[1][i] === board[2][i]) return true;
      }
      if (board[0][0] && board[0][0] === board[1][1] && board[1][1] === board[2][2]) return true;
      if (board[0][2] && board[0][2] === board[1][1] && board[1][1] === board[2][0]) return true;
      return false;
    }

    // Memory Game Enhanced
    let memoryCards = [], memoryFlipped = [], memoryFlips = 0, memoryStartTime, memoryInterval;

    function startMemory() {
      let memory = document.getElementById('memory');
      memory.innerHTML = '';
      const symbols = ["🍓","🍓","🍒","🍒","🍉","🍉","🥝","🥝","🍍","🍍","🍇","🍇","🫐","🫐","🍑","🍑"];
      symbols.sort(() => 0.5 - Math.random());
      memoryFlips = 0;
      updateScore('memoryFlips', 0);
      memoryStartTime = Date.now();
      clearInterval(memoryInterval);
      memoryInterval = setInterval(updateMemoryTime, 1000);
      memoryFlipped = [];
      symbols.forEach((sym, index) => {
        let card = document.createElement('button');
        card.className = 'memory-card';
        card.dataset.sym = sym;
        card.dataset.index = index;
        card.textContent = '❓';
        card.onclick = () => flipCard(card);
        memory.appendChild(card);
      });
    }

    function flipCard(card) {
      if (memoryFlipped.length < 2 && !card.classList.contains('flipped') && !card.classList.contains('matched')) {
        card.classList.add('flipped');
        card.textContent = card.dataset.sym;
        memoryFlipped.push(card);
        memoryFlips++;
        updateScore('memoryFlips', memoryFlips);
        if (memoryFlipped.length === 2) {
          setTimeout(() => {
            if (memoryFlipped[0].dataset.sym === memoryFlipped[1].dataset.sym) {
              memoryFlipped.forEach(c => c.classList.add('matched'));
              if (document.querySelectorAll('.matched').length === 16) {
                clearInterval(memoryInterval);
                showWinModal('You Matched All! Flips: ' + memoryFlips + ' in ' + Math.floor((Date.now() - memoryStartTime)/1000) + 's', 'memory');
              }
            } else {
              memoryFlipped.forEach(c => {
                c.classList.remove('flipped');
                c.textContent = '❓';
              });
            }
            memoryFlipped = [];
          }, 1000);
        }
      }
    }

    function updateMemoryTime() {
      let time = Math.floor((Date.now() - memoryStartTime) / 1000);
      updateScore('memoryTime', time);
    }

    function resetMemory() {
      startMemory();
    }

    // RPS Enhanced
    let playerWins = 0, aiWins = 0;

    function rpsPlay(choice) {
      const options = ['rock', 'paper', 'scissors'];
      const ai = options[Math.floor(Math.random() * 3)];
      let result = '';
      if (choice === ai) {
        result = "It's a draw!";
      } else if (
        (choice === 'rock' && ai === 'scissors') ||
        (choice === 'paper' && ai === 'rock') ||
        (choice === 'scissors' && ai === 'paper')
      ) {
        playerWins++;
        result = "You win!";
        updateScore('player', playerWins);
      } else {
        aiWins++;
        result = "AI wins!";
        updateScore('ai', aiWins);
      }
      document.getElementById('rpsResult').innerHTML = `You: ${choice} | AI: ${ai} → ${result}`;
    }

    function resetRPS() {
      playerWins = 0;
      aiWins = 0;
      updateScore('player', 0);
      updateScore('ai', 0);
      document.getElementById('rpsResult').textContent = '';
    }

    // Utility Functions
    function updateScore(type, value) {
      if (type === 'snake') document.getElementById('snakeScore').textContent = value;
      if (type === 'x') document.getElementById('xWins').textContent = value;
      if (type === 'o') document.getElementById('oWins').textContent = value;
      if (type === 'memoryFlips') document.getElementById('memoryFlips').textContent = value;
      if (type === 'memoryTime') document.getElementById('memoryTime').textContent = value;
      if (type === 'player') document.getElementById('playerWins').textContent = value;
      if (type === 'ai') document.getElementById('aiWins').textContent = value;
    }

    function showWinModal(message, game) {
      document.getElementById('modalTitle').textContent = '🎉 Victory! 🎉';
      document.getElementById('modalMessage').textContent = message;
      modal.style.display = 'flex';
      if (game === 'snake') {
        clearInterval(snakeInterval);
        document.removeEventListener('keydown', changeDirection);
      } else if (game === 'memory') {
        clearInterval(memoryInterval);
      }
    }

    // Initialize
    showMenu(); // Start with no game selected
  </script>
</body>
</html>
