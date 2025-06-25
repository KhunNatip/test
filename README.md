# test
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Slot Game</title>
  <style>
    body {
      text-align: center;
      font-family: Arial, sans-serif;
      background: #111;
      color: white;
      margin-top: 50px;
    }
    .slot {
      font-size: 60px;
      margin: 20px;
    }
    .reels {
      display: flex;
      justify-content: center;
      gap: 20px;
    }
    button {
      font-size: 20px;
      padding: 10px 20px;
      margin-top: 20px;
      background: limegreen;
      color: black;
      border: none;
      cursor: pointer;
    }
    #message {
      margin-top: 30px;
      font-size: 24px;
      color: yellow;
    }
  </style>
</head>
<body>
  <h1>🎰 Slot Machine Game</h1>
  <div class="reels">
    <div class="slot" id="slot1">🍒</div>
    <div class="slot" id="slot2">🍋</div>
    <div class="slot" id="slot3">🍊</div>
  </div>
  <button onclick="spin()">🎲 Spin</button>
  <div id="message"></div>

  <script>
    const symbols = ["🍒", "🍋", "🍊", "🔔", "⭐", "🍇"];
    let playCount = 0;
    const maxPlays = 10;

    function getRandomSymbol() {
      return symbols[Math.floor(Math.random() * symbols.length)];
    }

    function spin() {
      if (playCount >= maxPlays) {
        document.getElementById("message").textContent = "🎉 You've reached 10 plays!";
        return;
      }

      const s1 = getRandomSymbol();
      const s2 = getRandomSymbol();
      const s3 = getRandomSymbol();

      document.getElementById("slot1").textContent = s1;
      document.getElementById("slot2").textContent = s2;
      document.getElementById("slot3").textContent = s3;

      playCount++;

      if (s1 === s2 && s2 === s3) {
        document.getElementById("message").textContent = `🎊 Jackpot! (${playCount}/10)`;
      } else {
        document.getElementById("message").textContent = `Try again... (${playCount}/10)`;
      }

      if (playCount === maxPlays) {
        document.querySelector("button").disabled = true;
        document.getElementById("message").textContent += " Game Over!";
      }
    }
  </script>
</body>
</html>
