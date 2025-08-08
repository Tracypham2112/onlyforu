<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Love Letter 💌</title>
  <style>
    body {
      background: #ffe6f0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
    }

    .container {
      position: relative;
      width: 360px;
      height: 280px; /* tăng chiều cao */
      cursor: pointer;
    }

    .envelope {
      width: 100%;
      height: 100%;
      background: #ffb6c1;
      position: relative;
      border-radius: 12px;
      box-shadow: 0 10px 20px rgba(0,0,0,0.1);
      transition: transform 1s;
      overflow: hidden;
      padding-top: 60px;
    }

    .flap {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 50%;
      background: #ff69b4;
      clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
      transform-origin: top;
      transition: transform 1s;
      z-index: 2;
    }

    .message {
      position: absolute;
      top: 60px;
      left: 0;
      width: 100%;
      padding: 10px 20px 20px;
      text-align: center;
      color: #d63384;
      font-size: 1.05rem;
      font-weight: bold;
      opacity: 0;
      transition: opacity 1s ease;
      line-height: 1.6;
    }

    .opened .flap {
      transform: rotateX(-180deg);
    }

    .opened .message {
      opacity: 1;
    }

    .typing span {
      display: inline-block;
      opacity: 0;
      animation: typing 0.05s forwards;
    }

    @keyframes typing {
      to {
        opacity: 1;
      }
    }

    .heart {
      font-size: 1.6rem;
      margin-top: 12px;
      animation: pulse 1s infinite;
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.3); }
    }
  </style>
</head>
<body>
  <div class="container" onclick="openEnvelope()">
    <div class="envelope" id="envelope">
      <div class="flap"></div>
      <div class="message">
        <div id="line1" class="typing"></div>
        <div id="line2" class="typing" style="margin-top: 12px;"></div>
        <div id="heart" class="heart" style="opacity: 0;">❤️</div>
      </div>
    </div>
  </div>

  <script>
    const text1 = "Hahaa, nothingg, i just wanna make u happy, i love u ;)))";
    const text2 = "Deseo que seas más feliz cada día";

    function typeTextByWord(elementId, text, delayStart = 0) {
      const container = document.getElementById(elementId);
      container.innerHTML = '';
      const words = text.split(' ');
      let totalDelay = delayStart;

      words.forEach((word, i) => {
        const span = document.createElement('span');
        span.textContent = word + ' ';
        span.style.animationDelay = totalDelay + 's';
        span.style.marginRight = '2px';
        container.appendChild(span);
        totalDelay += 0.2; // delay theo từ
      });
    }

    let opened = false;

    function openEnvelope() {
      const envelope = document.getElementById('envelope');
      const heart = document.getElementById('heart');
      opened = !opened;
      envelope.classList.toggle('opened');

      if (opened) {
        typeTextByWord('line1', text1, 0.3);
        typeTextByWord('line2', text2, 2.5);
        setTimeout(() => {
          heart.style.opacity = 1;
        }, 5 * 1000);
      } else {
        document.getElementById('line1').innerHTML = '';
        document.getElementById('line2').innerHTML = '';
        heart.style.opacity = 0;
      }
    }
  </script>
</body>
</html>
