
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SULA.AI — Эмоции и Прозвище</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f0f4f8;
      padding: 20px;
    }
    h1 {
      color: #333;
    }
    video, canvas {
      width: 90%;
      max-width: 320px;
      border-radius: 8px;
      margin-top: 15px;
    }
    button {
      margin-top: 15px;
      padding: 10px 20px;
      font-size: 16px;
      background-color: #1e88e5;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
    #result {
      margin-top: 25px;
      font-size: 20px;
      color: #222;
      display: none;
    }
  </style>
</head>
<body>

  <h1>🤖 SULA.AI — Определение Эмоций</h1>
  <p>Включите камеру и получите прозвище от нейросети!</p>

  <video id="video" autoplay></video><br>
  <button onclick="takeSnapshot()">Сделать снимок</button><br>
  <canvas id="canvas"></canvas>

  <div id="result">
    <p><strong id="emotion"></strong></p>
    <p id="nickname"></p>
  </div>

  <script>
    const video = document.getElementById('video');
    const canvas = document.getElementById('canvas');
    const emotionEl = document.getElementById('emotion');
    const nicknameEl = document.getElementById('nickname');
    const resultDiv = document.getElementById('result');

    const emotions = [
      { emotion: "😊 Улыбка обнаружена", nickname: "Улыбашка" },
      { emotion: "😐 Нейтральное выражение", nickname: "Скучный" },
      { emotion: "😠 Легкое недовольство", nickname: "Суровый" },
      { emotion: "😂 Смех активен", nickname: "Хохотун" },
      { emotion: "😶 Без эмоций", nickname: "Кирпич" },
      { emotion: "😍 Восторг!", nickname: "Очаровашка" }
    ];

    navigator.mediaDevices.getUserMedia({ video: true })
      .then(stream => {
        video.srcObject = stream;
      })
      .catch(err => {
        alert("Ошибка доступа к камере.");
      });

    function takeSnapshot() {
      const context = canvas.getContext('2d');
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      context.drawImage(video, 0, 0, canvas.width, canvas.height);

      const selected = emotions[Math.floor(Math.random() * emotions.length)];
      emotionEl.textContent = selected.emotion;
      nicknameEl.textContent = "Ваше прозвище: " + selected.nickname;
      resultDiv.style.display = 'block';
    }
  </script>

</body>
</html>
