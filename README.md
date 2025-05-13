<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Scratch Card</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      text-align: center;
      padding: 30px;
    }
    .card {
      position: relative;
      width: 300px;
      height: 200px;
      margin: 40px auto;
      background: #ffffff;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
      border-radius: 10px;
      overflow: hidden;
    }
    .message {
      position: absolute;
      width: 100%;
      height: 100%;
      z-index: 1;
      top: 0;
      left: 0;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      background: #fff;
    }
    .message h2 {
      margin: 10px 0;
      font-size: 24px;
      color: #333;
    }
    .message p {
      font-size: 18px;
      color: green;
    }
    canvas {
      position: absolute;
      top: 0;
      left: 0;
      z-index: 2;
      cursor: grab;
    }
    .scratch-label {
      margin-top: 20px;
      font-size: 18px;
      color: #777;
    }
  </style>
</head>
<body>
  <h1>🎉 Digital Scratch Card 🎉</h1>
  <div class="scratch-label">Scratch to reveal</div>

  <div class="card">
    <!-- Hidden Message -->
    <div class="message" id="message">
      <h2>Samarth</h2>
      <p>Hurray! You won ₹11</p>
    </div>

    <!-- Scratch Layer -->
    <canvas id="scratchCanvas" width="300" height="200"></canvas>
  </div>

  <script>
    const canvas = document.getElementById("scratchCanvas");
    const ctx = canvas.getContext("2d");
    let isDrawing = false;

    // Fill canvas with gray scratch surface
    ctx.fillStyle = "#c0c0c0";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    // Optional: Add text or pattern on scratch surface
    ctx.fillStyle = "#999";
    ctx.font = "20px Arial";
    ctx.fillText("Scratch Here", 90, 105);

    // Set composite mode for scratch effect
    ctx.globalCompositeOperation = "destination-out";

    canvas.addEventListener("mousedown", () => (isDrawing = true));
    canvas.addEventListener("mouseup", () => (isDrawing = false));
    canvas.addEventListener("mouseleave", () => (isDrawing = false));

    canvas.addEventListener("mousemove", (e) => {
      if (!isDrawing) return;
      const rect = canvas.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;

      ctx.beginPath();
      ctx.arc(x, y, 15, 0, 2 * Math.PI);
      ctx.fill();
    });

    // For mobile devices
    canvas.addEventListener("touchstart", (e) => {
      isDrawing = true;
    });

    canvas.addEventListener("touchend", () => {
      isDrawing = false;
    });

    canvas.addEventListener("touchmove", (e) => {
      e.preventDefault();
      if (!isDrawing) return;
      const rect = canvas.getBoundingClientRect();
      const touch = e.touches[0];
      const x = touch.clientX - rect.left;
      const y = touch.clientY - rect.top;

      ctx.beginPath();
      ctx.arc(x, y, 15, 0, 2 * Math.PI);
      ctx.fill();
    });
  </script>
</body>
</html>
