<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Rock Paper Scissors</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      min-height: 100vh;
      font-family: Arial, sans-serif;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      background:
        radial-gradient(circle at top left, #5b21b6, transparent 35%),
        radial-gradient(circle at bottom right, #0ea5e9, transparent 35%),
        #111827;
    }

    .game-container {
      width: min(950px, 94%);
      padding: 30px;
      text-align: center;
      border-radius: 25px;
      background: rgba(17, 24, 39, 0.8);
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.45);
      backdrop-filter: blur(12px);
    }

    h1 {
      font-size: clamp(2rem, 5vw, 3.5rem);
      margin-bottom: 20px;
      color: #facc15;
      text-shadow: 0 0 15px rgba(250, 204, 21, 0.6);
    }

    .top-bar {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 15px;
      flex-wrap: wrap;
      margin-bottom: 25px;
    }

    button {
      border: none;
      cursor: pointer;
      font-size: 1rem;
      font-weight: bold;
      transition: 0.25s ease;
    }

    #startBtn,
    #musicBtn {
      padding: 12px 22px;
      border-radius: 30px;
      color: #111827;
      background: #facc15;
    }

    #startBtn:hover,
    #musicBtn:hover {
      transform: translateY(-3px) scale(1.04);
      background: #fde047;
    }

    .scoreboard {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 35px;
      margin: 20px 0;
    }

    .score-box {
      min-width: 130px;
      padding: 15px;
      border-radius: 15px;
      background: rgba(255, 255, 255, 0.12);
    }

    .score-box h2 {
      font-size: 1.1rem;
      margin-bottom: 8px;
    }

    .score {
      font-size: 2.5rem;
      color: #facc15;
      font-weight: bold;
    }

    .versus {
      font-size: 1.8rem;
      font-weight: bold;
      color: #f87171;
    }

    .game-area {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 60px;
      margin: 30px 0;
    }

    .fighter {
      min-width: 180px;
    }

    .fighter h3 {
      margin-bottom: 12px;
      color: #bae6fd;
    }

    .choice-display {
      min-height: 130px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 6rem;
      border-radius: 20px;
      background: rgba(255, 255, 255, 0.1);
      box-shadow: inset 0 0 20px rgba(255, 255, 255, 0.08);
    }

    .animate-choice {
      animation: pop 0.45s ease;
    }

    @keyframes pop {
      0% {
        transform: scale(0.5) rotate(-15deg);
        opacity: 0;
      }

      70% {
        transform: scale(1.15) rotate(5deg);
        opacity: 1;
      }

      100% {
        transform: scale(1) rotate(0);
      }
    }

    #result {
      min-height: 35px;
      margin: 20px 0;
      font-size: 1.5rem;
      font-weight: bold;
      color: #facc15;
    }

    .instructions {
      margin-bottom: 15px;
      color: #cbd5e1;
    }

    .controls {
      display: flex;
      justify-content: center;
      gap: 15px;
      flex-wrap: wrap;
    }

    .choice-btn {
      width: 150px;
      padding: 18px 10px;
      border-radius: 18px;
      color: white;
      background: linear-gradient(145deg, #2563eb, #7c3aed);
      box-shadow: 0 7px 0 #1e1b4b;
    }

    .choice-btn span {
      display: block;
      font-size: 3rem;
      margin-bottom: 5px;
    }

    .choice-btn:hover:not(:disabled) {
      transform: translateY(-5px);
      box-shadow: 0 12px 0 #1e1b4b;
    }

    .choice-btn:active:not(:disabled) {
      transform: translateY(3px);
      box-shadow: 0 3px 0 #1e1b4b;
    }

    .choice-btn:disabled {
      opacity: 0.45;
      cursor: not-allowed;
    }

    @media (max-width: 600px) {
      .game-container {
        padding: 20px 12px;
      }

      .game-area {
        gap: 12px;
      }

      .fighter {
        min-width: 135px;
      }

      .choice-display {
        min-height: 100px;
        font-size: 4rem;
      }

      .choice-btn {
        width: 105px;
        padding: 12px 5px;
      }

      .choice-btn span {
        font-size: 2.2rem;
      }
    }
  </style>
</head>

<body>
  <main class="game-container">
    <h1>Rock Paper Scissors</h1>

    <div class="top-bar">
      <button id="startBtn">Start Game</button>
      <button id="musicBtn">🔇 Music Off</button>
    </div>

    <section class="scoreboard">
      <div class="score-box">
        <h2>You</h2>
        <div id="playerScore" class="score">0</div>
      </div>

      <div class="versus">VS</div>

      <div class="score-box">
        <h2>Computer</h2>
        <div id="computerScore" class="score">0</div>
      </div>
    </section>

    <section class="game-area">
      <div class="fighter">
        <h3>Your Choice</h3>
        <div id="playerChoice" class="choice-display">❔</div>
      </div>

      <div class="fighter">
        <h3>Computer Choice</h3>
        <div id="computerChoice" class="choice-display">❔</div>
      </div>
    </section>

    <div id="result">Press “Start Game” to begin!</div>

    <p class="instructions">Choose your move:</p>

    <section class="controls">
      <button class="choice-btn" data-choice="rock" disabled>
        <span>✊</span>
        Rock
      </button>

      <button class="choice-btn" data-choice="paper" disabled>
        <span>✋</span>
        Paper
      </button>

      <button class="choice-btn" data-choice="scissors" disabled>
        <span>✌️</span>
        Scissors
      </button>
    </section>
  </main>

  <script>
    const startBtn = document.getElementById("startBtn");
    const musicBtn = document.getElementById("musicBtn");
    const playerScoreText = document.getElementById("playerScore");
    const computerScoreText = document.getElementById("computerScore");
    const playerChoiceDisplay = document.getElementById("playerChoice");
    const computerChoiceDisplay = document.getElementById("computerChoice");
    const resultText = document.getElementById("result");
    const choiceButtons = document.querySelectorAll(".choice-btn");

    const icons = {
      rock: "✊",
      paper: "✋",
      scissors: "✌️"
    };

    let playerScore = 0;
    let computerScore = 0;
    let gameStarted = false;

    let audioContext;
    let musicPlaying = false;
    let musicTimer;

    function initializeAudio() {
      if (!audioContext) {
        audioContext = new (window.AudioContext || window.webkitAudioContext)();
      }

      if (audioContext.state === "suspended") {
        audioContext.resume();
      }
    }

    function playSound(frequency, duration = 0.15, type = "sine") {
      if (!audioContext) return;

      const oscillator = audioContext.createOscillator();
      const gain = audioContext.createGain();

      oscillator.type = type;
      oscillator.frequency.value = frequency;

      gain.gain.setValueAtTime(0.15, audioContext.currentTime);
      gain.gain.exponentialRampToValueAtTime(
        0.001,
        audioContext.currentTime + duration
      );

      oscillator.connect(gain);
      gain.connect(audioContext.destination);

      oscillator.start();
      oscillator.stop(audioContext.currentTime + duration);
    }

    function startMusic() {
      if (musicPlaying) return;

      initializeAudio();
      musicPlaying = true;
      musicBtn.textContent = "🔊 Music On";

      const notes = [261.63, 329.63, 392.0, 329.63];
      let noteIndex = 0;

      musicTimer = setInterval(() => {
        if (musicPlaying) {
          playSound(notes[noteIndex], 0.25, "triangle");
          noteIndex = (noteIndex + 1) % notes.length;
        }
      }, 550);
    }

    function stopMusic() {
      musicPlaying = false;
      clearInterval(musicTimer);
      musicBtn.textContent = "🔇 Music Off";
    }

    function resetGame() {
      playerScore = 0;
      computerScore = 0;

      playerScoreText.textContent = "0";
      computerScoreText.textContent = "0";
      playerChoiceDisplay.textContent = "❔";
      computerChoiceDisplay.textContent = "❔";
      resultText.textContent = "Choose your move!";
    }

    function getComputerChoice() {
      const choices = ["rock", "paper", "scissors"];
      return choices[Math.floor(Math.random() * choices.length)];
    }

    function determineWinner(player, computer) {
      if (player === computer) return "draw";

      if (
        (player === "rock" && computer === "scissors") ||
        (player === "paper" && computer === "rock") ||
        (player === "scissors" && computer === "paper")
      ) {
        return "player";
      }

      return "computer";
    }

    function animateDisplay(element) {
      element.classList.remove("animate-choice");
      void element.offsetWidth;
      element.classList.add("animate-choice");
    }

    startBtn.addEventListener("click", () => {
      initializeAudio();
      resetGame();

      gameStarted = true;
      choiceButtons.forEach(button => {
        button.disabled = false;
      });

      resultText.textContent = "Choose your move!";
      startBtn.textContent = "Restart Game";

      if (!musicPlaying) {
        startMusic();
      }

      playSound(500, 0.2);
    });

    musicBtn.addEventListener("click", () => {
      initializeAudio();

      if (musicPlaying) {
        stopMusic();
      } else {
        startMusic();
      }
    });

    choiceButtons.forEach(button => {
      button.addEventListener("click", () => {
        if (!gameStarted) return;

        const playerChoice = button.dataset.choice;
        const computerChoice = getComputerChoice();
        const winner = determineWinner(playerChoice, computerChoice);

        playerChoiceDisplay.textContent = icons[playerChoice];
        computerChoiceDisplay.textContent = icons[computerChoice];

        animateDisplay(playerChoiceDisplay);
        animateDisplay(computerChoiceDisplay);

        if (winner === "player") {
          playerScore++;
          playerScoreText.textContent = playerScore;
          resultText.textContent = "🎉 You win this round!";
          playSound(700, 0.3);
        } else if (winner === "computer") {
          computerScore++;
          computerScoreText.textContent = computerScore;
          resultText.textContent = "😅 Computer wins this round!";
          playSound(180, 0.3, "sawtooth");
        } else {
          resultText.textContent = "🤝 It’s a draw!";
          playSound(400, 0.2);
        }
      });
    });
  </script>
</body>
</html>
