<!DOCTYPE html>
<html>
<head>
  <title>Slot Game 4x6</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.2/p5.min.js"></script>
  <style>
    body { display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; background: #222; }
    canvas { border: 2px solid #444; }
    #spinButton { 
      position: absolute; 
      bottom: 20px; 
      padding: 10px 20px; 
      font-size: 18px; 
      cursor: pointer; 
      background: #ff4444; 
      color: white; 
      border: none; 
      border-radius: 5px; 
    }
    #spinButton:hover { background: #cc3333; }
  </style>
</head>
<body>
  <button id="spinButton">Spin</button>
<script>
let symbols = ['🍎', '🍋', '🍒', '🍊', '🍇', '💎'];
let reels = [];
let spinning = false;
let spinSpeeds = [];
let reelPositions = [];
let cellSize = 100;
let rows = 4;
let cols = 6;
let margin = 10;

function setup() {
  createCanvas(cols * cellSize + margin * 2, rows * cellSize + margin * 2);
  for (let i = 0; i < cols; i++) {
    reels[i] = [];
    spinSpeeds[i] = 0;
    reelPositions[i] = 0;
    for (let j = 0; j < rows + 1; j++) {
      reels[i][j] = random(symbols);
    }
  }
  let spinButton = select('#spinButton');
  spinButton.mousePressed(startSpin);
}

function draw() {
  background(50);
  translate(margin, margin);
  for (let i = 0; i < cols; i++) {
    for (let j = 0; j < rows; j++) {
      let y = j * cellSize - reelPositions[i];
      if (y < 0) y += cellSize * rows;
      fill(255);
      rect(i * cellSize, y, cellSize, cellSize);
      fill(0);
      textSize(40);
      textAlign(CENTER, CENTER);
      text(reels[i][j], i * cellSize + cellSize / 2, y + cellSize / 2);
    }
    if (spinning) {
      reelPositions[i] += spinSpeeds[i];
      if (reelPositions[i] >= cellSize * rows) {
        reelPositions[i] -= cellSize * rows;
        for (let j = 0; j < rows; j++) {
          reels[i][j] = reels[i][j + 1];
        }
        reels[i][rows] = random(symbols);
      }
      spinSpeeds[i] *= 0.95;
      if (spinSpeeds[i] < 0.1 && random() < 0.05) {
        spinSpeeds[i] = 0;
      }
    }
  }
  if (spinning && spinSpeeds.every(speed => speed === 0)) {
    spinning = false;
    checkWin();
  }
}

function startSpin() {
  if (!spinning) {
    spinning = true;
    for (let i = 0; i < cols; i++) {
      spinSpeeds[i] = random(10, 20);
    }
  }
}

function checkWin() {
  let win = false;
  for (let j = 0; j < rows; j++) {
    let firstSymbol = reels[0][j];
    let isWinRow = true;
    for (let i = 1; i < cols; i++) {
      if (reels[i][j] !== firstSymbol) {
        isWinRow = false;
        break;
      }
    }
    if (isWinRow) {
      win = true;
      console.log(`Win on row ${j + 1}! Symbol: ${firstSymbol}`);
    }
  }
  if (win) {
    alert("You won!");
  } else {
    alert("No win this time.");
  }
}
</script>
</body>
</html>
