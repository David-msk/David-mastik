<!DOCTYPE html>
<html lang="ro">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Păcănele Simple</title>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
    background: #222;
    color: #eee;
    padding: 20px;
  }
  #reels {
    font-size: 80px;
    margin: 30px 0;
  }
  button {
    font-size: 24px;
    padding: 10px 30px;
    margin: 10px;
    cursor: pointer;
  }
  #balance {
    font-size: 28px;
    margin-top: 20px;
  }
  #message {
    font-size: 22px;
    margin-top: 15px;
    min-height: 28px;
  }
</style>
</head>
<body>

<h1>Păcănele Simple</h1>
<div id="balance">Bani: 100 lei</div>
<div id="reels">❓ ❓ ❓</div>
<button id="playBtn">Joacă (10 lei)</button>
<div id="message"></div>

<script>
  const symbols = ['🍒', '🔔', '🍋', '⭐', '7️⃣', '💎'];
  let balance = 100;
  const bet = 10;
  const reelsDiv = document.getElementById('reels');
  const balanceDiv = document.getElementById('balance');
  const messageDiv = document.getElementById('message');
  const playBtn = document.getElementById('playBtn');

  function spinReels() {
    return [
      symbols[Math.floor(Math.random() * symbols.length)],
      symbols[Math.floor(Math.random() * symbols.length)],
      symbols[Math.floor(Math.random() * symbols.length)],
    ];
  }

  function checkWin(reels) {
    // Dacă toate 3 simbolurile sunt egale - jackpot 5x
    if (reels[0] === reels[1] && reels[1] === reels[2]) {
      return bet * 5;
    }
    // Dacă 2 simboluri la rând sunt egale - câștig 2x
    if (reels[0] === reels[1] || reels[1] === reels[2] || reels[0] === reels[2]) {
      return bet * 2;
    }
    return 0; // pierdere
  }

  function updateUI(reels, win) {
    reelsDiv.textContent = reels.join(' ');
    balanceDiv.textContent = `Bani: ${balance} lei`;
    if (win > 0) {
      messageDiv.textContent = `Ai câștigat ${win} lei!`;
      messageDiv.style.color = 'lightgreen';
    } else {
      messageDiv.textContent = 'Ai pierdut, mai încearcă!';
      messageDiv.style.color = 'tomato';
    }
  }

  playBtn.addEventListener('click', () => {
    if (balance < bet) {
      messageDiv.textContent = 'Nu mai ai bani să joci!';
      messageDiv.style.color = 'yellow';
      return;
    }
    balance -= bet;
    const reels = spinReels();
    const win = checkWin(reels);
    balance += win;
    updateUI(reels, win);
  });
</script>

</body>
</html>
