# Love-
<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>我们的纪念日</title>
  <style>
    body {
      margin: 0;
      background: #fff;
      font-family: 'Arial', sans-serif;
      height: 100vh;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      position: relative;
    }

    .top-info {
      position: absolute;
      top: 10px; /* 调高 */
      width: 100%;
      text-align: center;
      font-size: 36px; /* 放大 */
      font-weight: 900; /* 加粗 */
      color: #d12f5b;
      background: rgba(255, 255, 255, 0.85);
      padding: 15px 25px;
      border-radius: 15px;
      z-index: 10;
      user-select: none;
    }

    .overlay {
      background: rgba(255, 255, 255, 0.7);
      padding: 30px;
      border-radius: 25px;
      text-align: center;
      z-index: 10;
      box-shadow: 0 0 15px rgba(209, 47, 91, 0.3);
    }

    .heart {
      width: 80px;
      height: 72px;
      background: red;
      position: absolute;
      transform: rotate(-45deg);
      animation: pop 0.6s ease-out forwards;
      pointer-events: none;
      z-index: 1000;
    }

    .heart::before,
    .heart::after {
      content: '';
      width: 80px;
      height: 72px;
      background: red;
      border-radius: 50%;
      position: absolute;
    }

    .heart::before {
      top: -40px;
      left: 0;
    }

    .heart::after {
      left: 40px;
      top: 0;
    }

    @keyframes pop {
      0% {
        transform: scale(0) rotate(-45deg);
        opacity: 0;
      }
      100% {
        transform: scale(1.2) rotate(-45deg);
        opacity: 1;
      }
    }

    .message {
      font-size: 22px;
      color: #d12f5b;
      margin-top: 10px;
      user-select: none;
    }

    @media screen and (max-width: 500px) {
      .top-info {
        font-size: 24px;
        padding: 10px 15px;
      }

      .message {
        font-size: 18px;
      }
    }
  </style>
</head>
<body>
  <!-- 实时纪念日时间 -->
  <div class="top-info" id="timer">我们在一起已经：计算中...</div>

  <!-- 爱心和情话区 -->
  <div class="overlay">
    <div class="message" id="message">加载中...</div>
  </div>

  <script>
    const messages = [
      "你点一下，我就心跳一下 ❤️",
      "全世界只有你最特别 💫",
      "每天醒来，最想看到的是你 😊",
      "你就是我最甜的习惯 🍬",
      "想把你藏在梦里，偷偷喜欢 🌙",
      "你笑的样子，我永远都记得 📷",
      "爱你，是我最确定的事情 💍",
      "心动，不是一瞬，是一直 💓",
      "我的宝贝有没有在想我呀？🥰",
      "他太可爱了，怎么办 😍"
    ];

    let index = 0;
    const messageEl = document.getElementById('message');
    messageEl.textContent = messages[0];

    function nextMessage(event) {
      index = (index + 1) % messages.length;
      messageEl.textContent = messages[index];

      // 生成爱心动画，位置在点击处
      const newHeart = document.createElement('div');
      newHeart.className = 'heart';

      // 计算点击位置，减去爱心大小的一半，让心心居中在点击点
      const heartWidth = 80;
      const heartHeight = 72;

      let x = event.clientX - heartWidth / 2;
      let y = event.clientY - heartHeight / 2;

      // 限制不超出窗口边界
      x = Math.min(Math.max(0, x), window.innerWidth - heartWidth);
      y = Math.min(Math.max(0, y), window.innerHeight - heartHeight);

      newHeart.style.left = x + 'px';
      newHeart.style.top = y + 'px';

      document.body.appendChild(newHeart);

      // 2秒后自动移除爱心元素
      setTimeout(() => {
        newHeart.remove();
      }, 2000);
    }

    document.body.addEventListener('click', nextMessage);

    function updateTimer() {
      const start = new Date("2024-04-14T00:00:00");
      const now = new Date();
      const diff = now - start;

      if(diff < 0){
        document.getElementById("timer").textContent = "纪念日还没到哦～";
        return;
      }

      const days = Math.floor(diff / (1000 * 60 * 60 * 24));
      const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
      const minutes = Math.floor((diff / (1000 * 60)) % 60);
      const seconds = Math.floor((diff / 1000) % 60);

      document.getElementById("timer").textContent =
        `我们在一起已经：${days} 天 ${hours} 小时 ${minutes} 分钟 ${seconds} 秒 ❤️`;
    }

    updateTimer();
    setInterval(updateTimer, 1000);
  </script>
</body>
</html>
