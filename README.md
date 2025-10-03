<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Joanna's Minigame Hearts & Rainbows</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, pink, lavender, skyblue);
      margin: 0;
      padding: 0;
      text-align: center;
    }
    header {
      background: #ff66b2;
      color: white;
      padding: 20px;
      font-size: 2em;
      font-weight: bold;
      box-shadow: 0 4px 6px rgba(0,0,0,0.2);
    }
    nav {
      margin: 20px;
    }
    nav button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 1em;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      background: #ff99cc;
      color: white;
    }
    nav button:hover {
      background: #ff66b2;
    }
    canvas {
      background: white;
      border: 2px solid #ff66b2;
      display: none;
      margin: 20px auto;
    }
    #ticTacToe {
      display: none;
      margin: 20px auto;
    }
    #ticTacToe td {
      width: 60px;
      height: 60px;
      text-align: center;
      vertical-align: middle;
      font-size: 2em;
      border: 2px solid #ff66b2;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <header>Joanna's Minigame Hearts & Rainbows</header>

  <nav>
    <button onclick="showGame('snake')">Play Snake</button>
    <button onclick="showGame('tictactoe')">Play Tic-Tac-Toe</button>
  </nav>

  <!-- Snake Game -->
  <canvas id="snake" width="300" height="300"></canvas>

  <!-- Tic Tac Toe -->
  <table id="ticTacToe"></table>

  <script>
    // Switch games
    function showGame(game) {
      document.getElementById('snake').style.display = 'none';
      document.getElementById('ticTacToe').style.display = 'none';
      if (game === 'snake') {
        document.getElementById('snake').style.display = 'block';
        startSnake();
      } else if (game === 'tictactoe') {
        document.getElementById('ticTacToe').style.display = 'table';
        startTicTacToe();
      }
    }

    // Snake Game
    let snakeCanvas = document.getElementById('snake');
    let ctx = snakeCanvas.getContext('2d');
    let snake, food, dx, dy, snakeInterval;

    function startSnake() {
      clearInterval(snakeInterval);
      snake = [{x: 150, y: 150}];
      dx = 10;
      dy = 0;
      food = randomFood();
      snakeInterval = setInterval(drawSnake, 100);
      document.addEventListener("keydown", changeDirection);
    }

    function drawSnake() {
      ctx.clearRect(0,0,300,300);
      ctx.fillStyle = 'green';
      snake.forEach(part => ctx.fillRect(part.x, part.y, 10, 10));
      ctx.fillStyle = 'red';
      ctx.fillRect(food.x, food.y, 10, 10);

      let head = {x: snake[0].x + dx, y: snake[0].y + dy};
      snake.unshift(head);

      if (head.x === food.x && head.y === food.y) {
        food = randomFood();
      } else {
        snake.pop();
      }

      if (head.x < 0 || head.y < 0 || head.x >= 300 || head.y >= 300 ||
          snake.slice(1).some(p => p.x === head.x && p.y === head.y)) {
        alert("Game Over!");
        startSnake();
      }
    }

    function changeDirection(e) {
      if (e.key === 'ArrowUp' && dy === 0) { dx = 0; dy = -10; }
      if (e.key === 'ArrowDown' && dy === 0) { dx = 0; dy = 10; }
      if (e.key === 'ArrowLeft' && dx === 0) { dx = -10; dy = 0; }
      if (e.key === 'ArrowRight' && dx === 0) { dx = 10; dy = 0; }
    }

    function randomFood() {
      return {
        x: Math.floor(Math.random()*30)*10,
        y: Math.floor(Math.random()*30)*10
      };
    }

    // Tic Tac Toe
    let board, currentPlayer;
    function startTicTacToe() {
      board = [["", "", ""], ["", "", ""], ["", "", ""]];
      currentPlayer = "X";
      let table = document.getElementById('ticTacToe');
      table.innerHTML = "";
      for (let i=0; i<3; i++) {
        let row = document.createElement('tr');
        for (let j=0; j<3; j++) {
          let cell = document.createElement('td');
          cell.onclick = () => makeMove(i,j,cell);
          row.appendChild(cell);
        }
        table.appendChild(row);
      }
    }

    function makeMove(i,j,cell) {
      if (board[i][j] === "") {
        board[i][j] = currentPlayer;
        cell.textContent = currentPlayer;
        if (checkWin()) {
          alert(currentPlayer + " Wins!");
          startTicTacToe();
        } else if (board.flat().every(x => x !== "")) {
          alert("It's a Draw!");
          startTicTacToe();
        } else {
          currentPlayer = currentPlayer === "X" ? "O" : "X";
        }
      }
    }

    function checkWin() {
      for (let i=0; i<3; i++) {
        if (board[i][0] && board[i][0]===board[i][1] && board[i][1]===board[i][2]) return true;
        if (board[0][i] && board[0][i]===board[1][i] && board[1][i]===board[2][i]) return true;
      }
      if (board[0][0] && board[0][0]===board[1][1] && board[1][1]===board[2][2]) return true;
      if (board[0][2] && board[0][2]===board[1][1] && board[1][1]===board[2][0]) return true;
      return false;
    }
  </script>
</body>
</html>
