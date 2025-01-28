# Habao
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chúc Mừng Năm Mới 2025 🎆</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      font-family: 'Arial', sans-serif;
    }

    .background {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: url('https://img.freepik.com/premium-photo/chinese-happy-new-year-background_257043-16065.jpg') no-repeat center center;
      background-size: cover;
      z-index: -3;
    }

    h1 {
      font-size: 4rem;
      color: #ff4500;
      text-shadow: 0 0 15px #ff6347, 0 0 25px #ff4500;
      text-align: center;
      animation: glow 2s infinite alternate;
      margin-top: 200px;
    }

    @keyframes glow {
      from {
        text-shadow: 0 0 10px #ffa500, 0 0 20px #ffd700;
      }
      to {
        text-shadow: 0 0 20px #ff4500, 0 0 30px #ff6347;
      }
    }

    .intro {
      font-size: 1.5rem;
      text-align: center;
      color: #b22222;
      font-weight: bold;
      margin-bottom: 20px;
    }

    .game-section {
      text-align: center;
      margin: 60px auto;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: -2;
    }
  </style>
</head>
<body>
  <div class="background"></div>

  <h1>Chúc Mừng Năm Mới 2025! 🎇</h1>
  <p class="intro">Chúc bạn một năm mới an khang, thịnh vượng và vạn sự như ý! 🌸</p>

  <div class="game-section">
    <p>Sắp xếp các từ sau thành một câu có nghĩa: <strong>"T/B/n/y/T/ô/r/h/u/ề/g/n/a"</strong></p>
    <input type="text" id="answer" placeholder="Nhập câu trả lời của bạn...">
    <br>
    <button onclick="checkAnswer()">Trả Lời</button>
    <p class="result" id="result"></p>
  </div>

  <canvas id="fireworks"></canvas>

  <script>
    const canvas = document.getElementById("fireworks");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    const particles = [];
    const snowflakes = [];

    function createFirework() {
      const x = Math.random() * canvas.width;
      const y = Math.random() * canvas.height * 0.5;
      const colors = ["#ff4500", "#ffa500", "#ffd700", "#32cd32", "#1e90ff", "#ff69b4"];
      for (let i = 0; i < 200; i++) {
        particles.push({
          x,
          y,
          radius: Math.random() * 3 + 1,
          angle: Math.random() * Math.PI * 2,
          speed: Math.random() * 6 + 2,
          color: colors[Math.floor(Math.random() * colors.length)],
          alpha: 1,
        });
      }
    }

    function updateParticles() {
      particles.forEach((p, i) => {
        p.x += Math.cos(p.angle) * p.speed;
        p.y += Math.sin(p.angle) * p.speed;
        p.alpha -= 0.02;
        if (p.alpha <= 0) particles.splice(i, 1);
      });
    }

    function drawParticles() {
      particles.forEach((p) => {
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(${hexToRgb(p.color)}, ${p.alpha})`;
        ctx.fill();
      });
    }

    function createSnowflake() {
      snowflakes.push({
        x: Math.random() * canvas.width,
        y: -10,
        radius: Math.random() * 4 + 1,
        speed: Math.random() * 2 + 1,
        angle: Math.random() * Math.PI * 2,
      });
    }

    function updateSnowflakes() {
      snowflakes.forEach((s, i) => {
        s.y += s.speed;
        s.x += Math.sin(s.angle) * 2;
        if (s.y > canvas.height) snowflakes.splice(i, 1);
      });
    }

    function drawSnowflakes() {
      snowflakes.forEach((s) => {
        ctx.beginPath();
        ctx.arc(s.x, s.y, s.radius, 0, Math.PI * 2);
        ctx.fillStyle = "gold";
        ctx.fill();
      });
    }

    function hexToRgb(hex) {
      const bigint = parseInt(hex.slice(1), 16);
      return `${(bigint >> 16) & 255}, ${(bigint >> 8) & 255}, ${bigint & 255}`;
    }

    function loop() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawParticles();
      updateParticles();
      drawSnowflakes();
      updateSnowflakes();
      if (Math.random() < 0.08) createFirework();
      if (Math.random() < 0.1) createSnowflake();
      requestAnimationFrame(loop);
    }
    loop();
    function checkAnswer() {
  const answer = document.getElementById("answer").value.trim();
  const result = document.getElementById("result");
  const button = document.querySelector("button");

  if (answer.toLowerCase() === "bông truyền than") {
    const luckyMoney = Math.floor(Math.random() * 10 + 1) * 1000;
    result.innerHTML = `🎉 Chính xác! Bạn nhận được lì xì: <strong>${luckyMoney.toLocaleString()} đ</strong>`;
    createFirework();
  } else {
    result.innerHTML = "❌ Sai rồi! Hãy thử lại!";
  }

  // Vô hiệu hóa nút trả lời và ô nhập
  button.disabled = true;
  document.getElementById("answer").disabled = true;
}
  </script>
</body>
</html>
