<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Joanna's Minigame Hearts & Rainbows</title>
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      color: white;
      overflow-x: hidden;
      text-align: center;
    }
    header {
      background: rgba(0,0,0,0.6);
      color: white;
      padding: 20px;
      font-size: 2em;
      font-weight: bold;
      position: relative;
      z-index: 2;
    }
    nav {
      margin: 20px;
      position: relative;
      z-index: 2;
    }
    nav button {
      margin: 10px;
      padding: 14px 28px;
      font-size: 1.1em;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      background: linear-gradient(135deg, #ff66cc, #ff9966);
      color: white;
      box-shadow: 0 0 12px rgba(255,255,255,0.4);
      transition: transform 0.2s;
    }
    nav button:hover {
      transform: scale(1.1);
    }
    canvas, table, .game {
      background: rgba(255,255,255,0.9);
      border-radius: 12px;
      box-shadow: 0 0 15px rgba(0,0,0,0.3);
      margin: 20px auto;
      padding: 10px;
      display: none;
      position: relative;
      z-index: 2;
    }
    #ticTacToe td {
      width: 80px;
      height: 80px;
      text-align: center;
      vertical-align: middle;
      font-size: 2em;
      border: 2px solid #ff66cc;
      cursor: pointer;
    }
    /* Rainbow Hearts background */
    .background {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      overflow: hidden;
      z-index: 0;
      background: linear-gradient(135deg, #ff66cc, #ff9966, #66ccff, #cc66ff);
      background-size: 600% 600%;
      animation: rainbowShift 10s ease infinite;
    }
    @keyframes rainbowShift {
      0%{background-position:0% 50%}
      50%{background-position:100% 50%}
      100%{background-position:0% 50%}
    }
    .heart {
      position: absolute;
      font-size: 24px;
      animation: floatUp 8s linear infinite;
      opacity: 0.7;
    }
    @keyframes floatUp {
      from { transform: translateY(100vh) scale(1); opacity: 1; }
      to { transform: translateY(-10vh) scale(0.5); opacity: 0; }
    }
    audio, #playMusicBtn {
      position: fixed;
      bottom: 10px;
      left: 10px;
      z-index: 3;
    }
  </style>
</head>
<body>
  <div class="background" id="bg"></div>
  <header>Joanna's Minigame Hearts & Rainbows 🌈❤️</header>

  <nav>
    <button onclick="showGame('snake')">🐍 Snake</button>
    <button onclick="showGame('tictactoe')">❌⭕ Tic Tac Toe</button>
    <button onclick="showGame('memory')">🃏 Memory Flip</button>
    <button onclick="showGame('rps')">✊✋✌ Rock Paper Scissors</button>
  </nav>

  <!-- Snake Game -->
  <canvas id="snake" width="320" height="320"></canvas>

  <!-- Tic Tac Toe -->
  <table id="ticTacToe"></table>

  <!-- Memory Game -->
  <div id="memory" class="game"></div>

  <!-- Rock Paper Scissors -->
  <div id="rps" class="game">
    <p>Choose your move:</p>
    <button onclick="rpsPlay('rock')">✊ Rock</button>
    <button onclick="rpsPlay('paper')">✋ Paper</button>
    <button onclick="rpsPlay('scissors')">✌ Scissors</button>
    <p id="rpsResult"></p>
  </div>

  <!-- Music Button -->
  <button id="playMusicBtn">▶ Play Phonk Music</button>
  <audio id="bgMusic" loop>
    <source src="https://cdn.pixabay.com/audio/2023/05/01/audio_d2a6a36c3b.mp3" type="audio/mpeg">
  </audio>

  <script>
    // Music play fix for all devices
    const music = document.getElementById('bgMusic');
    const playBtn = document.getElementById('playMusicBtn');
    playBtn.onclick = () => {
      music.play();
      playBtn.style.display = 'none';
    };

    // Floating hearts
    function spawnHeart(){
      const heart=document.createElement('div');
      heart.className='heart';
      heart.style.left=Math.random()*100+'vw';
      heart.style.animationDuration=(5+Math.random()*5)+'s';
      heart.textContent='❤️';
      document.getElementById('bg').appendChild(heart);
      setTimeout(()=>heart.remove(),8000);
    }
    setInterval(spawnHeart,600);

    // Switch games
    function showGame(game){
      ['snake','ticTacToe','memory','rps'].forEach(id=>{
        document.getElementById(id).style.display='none';
      });
      if(game==='snake'){document.getElementById('snake').style.display='block';startSnake();}
      if(game==='tictactoe'){document.getElementById('ticTacToe').style.display='table';startTicTacToe();}
      if(game==='memory'){document.getElementById('memory').style.display='block';startMemory();}
      if(game==='rps'){document.getElementById('rps').style.display='block';}
    }

    /* SNAKE */
    let snakeCanvas=document.getElementById('snake');
    let ctx=snakeCanvas.getContext('2d');
    let snake,food,dx,dy,snakeInterval;
    function startSnake(){
      clearInterval(snakeInterval);
      snake=[{x:160,y:160}];
      dx=10; dy=0;
      food=randomFood();
      snakeInterval=setInterval(drawSnake,100);
      document.onkeydown=changeDirection;
    }
    function drawSnake(){
      ctx.clearRect(0,0,320,320);
      ctx.fillStyle='lime';
      snake.forEach(p=>ctx.fillRect(p.x,p.y,10,10));
      ctx.fillStyle='red';
      ctx.fillRect(food.x,food.y,10,10);
      let head={x:snake[0].x+dx,y:snake[0].y+dy};
      snake.unshift(head);
      if(head.x===food.x&&head.y===food.y){food=randomFood();}else{snake.pop();}
      if(head.x<0||head.y<0||head.x>=320||head.y>=320||snake.slice(1).some(p=>p.x===head.x&&p.y===head.y)){
        alert("Game Over!");startSnake();
      }
    }
    function changeDirection(e){
      if(e.key==='ArrowUp'&&dy===0){dx=0;dy=-10;}
      if(e.key==='ArrowDown'&&dy===0){dx=0;dy=10;}
      if(e.key==='ArrowLeft'&&dx===0){dx=-10;dy=0;}
      if(e.key==='ArrowRight'&&dx===0){dx=10;dy=0;}
    }
    function randomFood(){return{x:Math.floor(Math.random()*32)*10,y:Math.floor(Math.random()*32)*10};}

    /* TIC TAC TOE */
    let board,currentPlayer;
    function startTicTacToe(){
      board=[["","",""],["","",""],["","",""]];
      currentPlayer="X";
      let table=document.getElementById('ticTacToe');
      table.innerHTML="";
      for(let i=0;i<3;i++){
        let row=document.createElement('tr');
        for(let j=0;j<3;j++){
          let cell=document.createElement('td');
          cell.onclick=()=>makeMove(i,j,cell);
          row.appendChild(cell);
        }
        table.appendChild(row);
      }
    }
    function makeMove(i,j,cell){
      if(board[i][j]===""){
        board[i][j]=currentPlayer;
        cell.textContent=currentPlayer;
        if(checkWin()){alert(currentPlayer+" Wins!");startTicTacToe();}
        else if(board.flat().every(x=>x!="")){alert("Draw!");startTicTacToe();}
        else currentPlayer=currentPlayer==="X"?"O":"X";
      }
    }
    function checkWin(){
      for(let i=0;i<3;i++){
        if(board[i][0]&&board[i][0]===board[i][1]&&board[i][1]===board[i][2])return true;
        if(board[0][i]&&board[0][i]===board[1][i]&&board[1][i]===board[2][i])return true;
      }
      if(board[0][0]&&board[0][0]===board[1][1]&&board[1][1]===board[2][2])return true;
      if(board[0][2]&&board[0][2]===board[1][1]&&board[1][1]===board[2][0])return true;
      return false;
    }

    /* MEMORY */
    let memoryFlipped;
    function startMemory(){
      let memory=document.getElementById('memory');
      memory.innerHTML="";
      const symbols=["🍓","🍓","🍒","🍒","🍉","🍉","🥝","🥝","🍍","🍍","🍇","🍇"];
      symbols.sort(()=>0.5-Math.random());
      memoryFlipped=[];
      symbols.forEach(sym=>{
        let card=document.createElement('button');
        card.textContent="❓";
        card.style.fontSize="2em";
        card.style.margin="5px";
        card.onclick=()=>flipCard(card,sym);
        memory.appendChild(card);
      });
    }
    function flipCard(card,sym){
      if(memoryFlipped.length<2&&card.textContent==="❓"){
        card.textContent=sym;
        memoryFlipped.push({card,sym});
        if(memoryFlipped.length===2){
          if(memoryFlipped[0].sym===memoryFlipped[1].sym){memoryFlipped=[];}
          else{setTimeout(()=>{memoryFlipped.forEach(c=>c.card.textContent="❓");memoryFlipped=[];},1000);}
        }
      }
    }

    /* ROCK PAPER SCISSORS */
    function rpsPlay(choice){
      const options=['rock','paper','scissors'];
      const ai=options[Math.floor(Math.random()*3)];
      let result="";
      if(choice===ai) result="It's a draw!";
      else if((choice==='rock'&&ai==='scissors')||(choice==='paper'&&ai==='rock')||(choice==='scissors'&&ai==='paper')) result="You win!";
      else result="AI wins!";
      document.getElementById('rpsResult').textContent=`You: ${choice} | AI: ${ai} → ${result}`;
    }
  </script>
</body>
</html>
