# stop watch web application
#html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Stopwatch</title>
  <link rel="stylesheet" href="C:\Users\ADMIN\Desktop\hero\style.css" />
    <link rel="stylesheet" href=C:\Users\ADMIN\Desktop\hero\script.js />
</head>
<body>
  <div class="container">
    <h1>Stopwatch</h1>
    <div id="display">00:00:00</div>
    <div class="buttons">
      <button id="startStop">Start</button>
      <button id="reset">Reset</button>
      <button id="lap">Lap</button>
    </div>
    <ul id="laps"></ul>
  </div>
  <script src="script.js"></script>
</body>
</html>
#css
body {
  font-family: Arial, sans-serif;
  background-color: #1c1c2b;
  color: #ffffff;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.container {
  text-align: center;
  background-color: #2e2e3e;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

#display {
  font-size: 48px;
  margin: 20px 0;
  font-weight: bold;
}

.buttons button {
  padding: 10px 20px;
  margin: 5px;
  font-size: 18px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  background-color: #4c4cff;
  color: white;
  transition: background-color 0.3s;
}

.buttons button:hover {
  background-color: #3333cc;
}

#laps {
  list-style-type: none;
  padding: 0;
  margin-top: 20px;
}

#laps li {
  background-color: #444;
  padding: 8px;
  margin: 4px;
  border-radius: 5px;
}
#js
let startTime = 0;
let elapsedTime = 0;
let timerInterval;
let running = false;

const display = document.getElementById("display");
const startStopBtn = document.getElementById("startStop");
const resetBtn = document.getElementById("reset");
const lapBtn = document.getElementById("lap");
const lapsContainer = document.getElementById("laps");

function updateDisplay(time) {
  const date = new Date(time);
  const minutes = String(date.getUTCMinutes()).padStart(2, '0');
  const seconds = String(date.getUTCSeconds()).padStart(2, '0');
  const milliseconds = String(Math.floor(date.getUTCMilliseconds() / 10)).padStart(2, '0');
  display.textContent = `${minutes}:${seconds}:${milliseconds}`;
}

function startStop() {
  if (!running) {
    startTime = Date.now() - elapsedTime;
    timerInterval = setInterval(() => {
      elapsedTime = Date.now() - startTime;
      updateDisplay(elapsedTime);
    }, 10);
    startStopBtn.textContent = "Pause";
    running = true;
  } else {
    clearInterval(timerInterval);
    startStopBtn.textContent = "Start";
    running = false;
  }
}

function reset() {
  clearInterval(timerInterval);
  elapsedTime = 0;
  running = false;
  updateDisplay(elapsedTime);
  startStopBtn.textContent = "Start";
  lapsContainer.innerHTML = "";
}

function recordLap() {
  if (elapsedTime === 0) return;
  const lapTime = display.textContent;
  const li = document.createElement("li");
  li.textContent = `Lap: ${lapTime}`;
  lapsContainer.appendChild(li);
}

startStopBtn.addEventListener("click", startStop);
resetBtn.addEventListener("click", reset);
lapBtn.addEventListener("click", recordLap);
