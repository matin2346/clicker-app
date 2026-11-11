<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>بازی کلیکی تلگرام</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        body {
            background-color: var(--tg-theme-bg-color, #1f2125);
            color: var(--tg-theme-text-color, #ffffff);
            font-family: Tahoma, sans-serif;
            text-align: center;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            overflow: hidden;
        }
        h2 {
            margin-bottom: 5px;
            font-size: 22px;
        }
        p {
            font-size: 14px;
            color: #b0b5bc;
        }
        #score {
            font-size: 50px;
            font-weight: bold;
            color: #f3ba2f;
            margin: 20px 0;
        }
        .coin-btn {
            background: none;
            border: none;
            cursor: pointer;
            outline: none;
            transition: transform 0.1s ease;
            padding: 0;
        }
        .coin-btn img {
            width: 160px;
            height: 160px;
            border-radius: 50%;
            box-shadow: 0 0 25px rgba(243, 186, 47, 0.5);
        }
        .coin-btn:active {
            transform: scale(0.90);
        }
        #user-info {
            margin-top: 25px;
            font-size: 12px;
            color: #8c939e;
        }
    </style>
</head>
<body>

    <h2 id="greeting">سلام، بازیکن!</h2>
    <p>روی سکه بزن و امتیاز جمع کن</p>

    <div id="score">0</div>

    <button class="coin-btn" onclick="incrementScore()">
        <img src="https://cryptologos.cc/logos/toncoin-ton-logo.png" alt="Coin">
    </button>

    <div id="user-info">در حال اتصال...</div>

    <script>
        let tg = window.Telegram.WebApp;
        tg.expand();

        let score = 0;

        if (tg.initDataUnsafe && tg.initDataUnsafe.user) {
            let user = tg.initDataUnsafe.user;
            document.getElementById('greeting').innerText = `سلام، ${user.first_name}!`;
            document.getElementById('user-info').innerText = `شناسه: ${user.id}`;
        }

        function incrementScore() {
            score += 1;
            document.getElementById('score').innerText = score;
            
            if (tg.HapticFeedback) {
                tg.HapticFeedback.impactOccurred('light');
            }
        }
    </script>

</body>
</html>
