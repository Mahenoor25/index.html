<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Typing Speed Test</title>
  <style>
    :root {
      --bg-color: #2d2d2d;
      --text-color: white;
      --accent-color: #764ba2;
    }

    body.light {
      --bg-color: #f4f4f4;
      --text-color: #333;
      --accent-color: #764ba2;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
      background: var(--bg-color);
      color: var(--text-color);
      margin: 0;
      padding: 0;
      transition: background 0.3s, color 0.3s;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }

    .container {
      background: var(--bg-color);
      padding: 30px;
      border-radius: 15px;
      width: 90%;
      max-width: 600px;
      text-align: center;
      box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    }

    .quote {
      font-size: 1.2rem;
      margin-bottom: 20px;
    }

    textarea {
      width: 100%;
      height: 100px;
      padding: 10px;
      font-size: 1rem;
      border-radius: 10px;
      border: none;
      outline: none;
      resize: none;
      background: #fff;
      color: #000;
    }

    .stats {
      margin-top: 20px;
      font-size: 1rem;
    }

    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 1rem;
      background: var(--accent-color);
      border: none;
      border-radius: 10px;
      color: white;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      opacity: 0.9;
    }

    .theme-toggle {
      position: absolute;
      top: 20px;
      right: 20px;
      background: none;
      color: var(--text-color);
      border: 2px solid var(--accent-color);
      padding: 5px 10px;
      border-radius: 8px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <button class="theme-toggle" onclick="toggleTheme()">Toggle Mode</button>
  <div class="container">
    <h2>Typing Speed Test</h2>
    <div class="quote" id="quote">Loading...</div>
    <textarea id="input" placeholder="Start typing here..."></textarea>
    <div class="stats" id="stats">Time: 0s | WPM: 0 | Accuracy: 0%</div>
    <button onclick="resetTest()">Try Again</button>
  </div>

  <script>
    const quotes = [
      "Typing fast improves productivity and saves time.",
      "Practice makes a man perfect in every field.",
      "Learning to code opens many opportunities.",
      "Hard work is the key to success and growth.",
      "Focus and determination lead to excellence."
    ];

    const quoteEl = document.getElementById("quote");
    const inputEl = document.getElementById("input");
    const statsEl = document.getElementById("stats");

    let startTime, interval;
    let currentQuote = "";

    function setNewQuote() {
      currentQuote = quotes[Math.floor(Math.random() * quotes.length)];
      quoteEl.textContent = currentQuote;
    }

    function startTimer() {
      startTime = new Date();
      interval = setInterval(() => {
        const elapsed = Math.floor((new Date() - startTime) / 1000);
        const wordsTyped = inputEl.value.trim().split(/\s+/).length;
        const wpm = Math.round((wordsTyped / elapsed) * 60);
        const accuracy = calculateAccuracy();

        statsEl.textContent = `Time: ${elapsed}s | WPM: ${isNaN(wpm) ? 0 : wpm} | Accuracy: ${accuracy}%`;
      }, 1000);
    }

    function calculateAccuracy() {
      let typed = inputEl.value.trim();
      let correct = 0;
      for (let i = 0; i < typed.length && i < currentQuote.length; i++) {
        if (typed[i] === currentQuote[i]) correct++;
      }
      return currentQuote.length
        ? Math.floor((correct / currentQuote.length) * 100)
        : 0;
    }

    inputEl.addEventListener("input", () => {
      if (inputEl.value.length === 1) startTimer();
      if (inputEl.value === currentQuote) clearInterval(interval);
    });

    function resetTest() {
      inputEl.value = "";
      clearInterval(interval);
      statsEl.textContent = "Time: 0s | WPM: 0 | Accuracy: 0%";
      setNewQuote();
    }

    function toggleTheme() {
      document.body.classList.toggle("light");
    }

    // Initial setup
    setNewQuote();
  </script>
</body>
</html>


