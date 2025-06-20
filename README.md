<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>NeoChrono - Unique Stopwatch</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: radial-gradient(circle at top left, #0f2027, #203a43, #2c5364);
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }h1 {
  font-size: 2.5rem;
  margin-bottom: 20px;
  letter-spacing: 2px;
}

#time {
  font-size: 4rem;
  margin: 20px;
  font-weight: bold;
}

.buttons, .laps {
  margin: 10px;
}

button {
  background: #1abc9c;
  border: none;
  color: #fff;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1rem;
  transition: background 0.3s ease;
}

button:hover {
  background: #16a085;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background: rgba(255, 255, 255, 0.1);
  margin: 5px 0;
  padding: 5px 10px;
  border-radius: 5px;
}

  </style>
</head>
<body>
  <h1>NeoChrono Stopwatch</h1>
  <div id="time">00:00:00</div>
  <div class="buttons">
    <button onclick="startStop()">Start</button>
    <button onclick="resetTime()">Reset</button>
    <button onclick="recordLap()">Lap</button>
  </div>
  <div class="laps">
    <h3>Lap Times</h3>
    <ul id="lapList"></ul>
  </div>  <script>
    let [hours, minutes, seconds] = [0, 0, 0];
    let displayTime = document.getElementById("time");
    let timer = null;

    function updateDisplay() {
      let h = hours < 10 ? "0" + hours : hours;
      let m = minutes < 10 ? "0" + minutes : minutes;
      let s = seconds < 10 ? "0" + seconds : seconds;
      displayTime.innerText = `${h}:${m}:${s}`;
    }

    function stopwatch() {
      seconds++;
      if (seconds === 60) {
        seconds = 0;
        minutes++;
      }
      if (minutes === 60) {
        minutes = 0;
        hours++;
      }
      updateDisplay();
    }

    function startStop() {
      if (timer === null) {
        timer = setInterval(stopwatch, 1000);
        event.target.innerText = "Pause";
      } else {
        clearInterval(timer);
        timer = null;
        event.target.innerText = "Start";
      }
    }

    function resetTime() {
      clearInterval(timer);
      timer = null;
      [hours, minutes, seconds] = [0, 0, 0];
      updateDisplay();
      document.querySelector(".buttons button").innerText = "Start";
      document.getElementById("lapList").innerHTML = "";
    }

    function recordLap() {
      const lapList = document.getElementById("lapList");
      const li = document.createElement("li");
      li.innerText = displayTime.innerText;
      lapList.appendChild(li);
    }
  </script></body>
</html>
