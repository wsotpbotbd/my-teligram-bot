<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Premium Digital Payment Gateway</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

        body {
            font-family: 'Poppins', sans-serif;
            text-align: center;
            background: linear-gradient(135deg, #00bcd4, #009688);
            color: white;
            margin: 0;
            padding: 0;
        }

        .container {
            max-width: 500px;
            margin: auto;
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.2);
        }

        h1 {
            font-size: 28px;
            font-weight: 600;
            text-transform: uppercase;
            margin-bottom: 20px;
        }

        .payment-options {
            display: flex;
            justify-content: space-between;
            gap: 20px;
            margin-top: 20px;
        }

        .option {
            cursor: pointer;
            padding: 20px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 15px;
            transition: transform 0.3s, background 0.3s;
            width: 30%;
            text-align: center;
        }

        .option img {
            width: 65px;
            height: 50px;
        }

        .option:hover {
            transform: scale(1.1);
            background: rgba(255, 255, 255, 0.4);
        }

        .hidden {
            display: none;
        }

        .payment-box {
            background: rgba(255, 255, 255, 0.2);
            padding: 25px;
            border-radius: 15px;
            margin-top: 20px;
            animation: fadeIn 0.5s ease-in-out;
        }

        input, button {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border-radius: 6px;
            border: none;
            font-size: 16px;
            text-align: center;
        }

        button {
            background: #ff9800;
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s;
        }

        button:hover {
            background: #e68900;
        }

        .back-btn {
            background: #ff4444;
        }

        .back-btn:hover {
            background: #cc0000;
        }

        .countdown {
            font-size: 18px;
            font-weight: bold;
            color: #ffeb3b;
            margin-top: 10px;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .payment-info {
            text-align: left;
            margin-top: 20px;
            font-size: 16px;
        }

        .copy-btn {
            background: #4caf50;
            color: white;
            font-size: 16px;
            cursor: pointer;
            padding: 10px;
            border: none;
            border-radius: 6px;
            margin-top: 10px;
        }

        .copy-btn:hover {
            background: #45a049;
        }

    </style>
</head>
<body>

    <div class="container">
        <h1><b>DIGITAL PAYMENT GATEWAY</b></h1>

        <div class="payment-options">
            <div class="option" id="bkash-option" onclick="selectPayment('বিকাশ', '8801318645435')">
                <img src="https://assets.onecompiler.app/42weepxyg/436yt5z5w/download%20(10).png" alt="Bkash">
                <p><b>বিকাশ</b></p>
            </div>
            <div class="option" id="nagad-option" onclick="selectPayment('নগদ', '8801855966005')">
                <img src="https://assets.onecompiler.app/42weepxyg/436yt5z5w/download%20(11).png" alt="Nagad">
                <p><b>নগদ</b></p>
            </div>
            <div class="option" id="rocket-option" onclick="selectPayment('রকেট', '8801829261192')">
                <img src="https://assets.onecompiler.app/42weepxyg/438myyrun/download%20(12).png" alt="Rocket">
                <p><b>রকেট</b></p>
            </div>
        </div>
        
        

        <div id="payment-box" class="payment-box hidden">
            <h2 id="selected-payment"></h2>
            <input type="number" id="amount" placeholder="৩০০ - ২০০০০">
            <button onclick="nextStep()">পরবর্তী</button>
        </div>

        <div id="payment-details" class="hidden">
            <h3>পেমেন্ট পাঠানোর নির্দেশনা</h3>
            <p id="payment-instruction"></p>
            <button onclick="copyNumber()">📋 কপি করুন</button>
            <input type="tel" id="sender-number" placeholder="প্রেরকের নাম্বার (১১ ডিজিট)">
            <input type="text" id="trx-id" placeholder="ট্রানজেকশন আইডি">
            <button onclick="startCountdown()">সাবমিট</button>
            <p class="countdown" id="countdown"></p>
            <p id="payment-code" class="payment-info hidden">Your Payment Code: <span id="payment-code-text"></span></p>
            <button class="copy-btn hidden" id="copy-payment-code" onclick="copyPaymentCode()">কপি করুন</button>
        </div>
    </div>

    <script>
        let selectedMethod = "";
        let selectedNumber = "";

        function selectPayment(name, number) {
            selectedMethod = name;
            selectedNumber = number;

            document.getElementById("selected-payment").innerText = `${name} পেমেন্ট নির্বাচন করেছেন`;
            document.getElementById("payment-box").classList.remove("hidden");
            
            document.querySelector(".payment-options").classList.add("hidden");
        }

        function nextStep() {
            let amount = document.getElementById("amount").value;
            if (amount < 300 || amount > 20000) {
                alert("পরিমাণ ৩০০ থেকে ২০০০০ এর মধ্যে হতে হবে!");
                return;
            }

            document.getElementById("payment-details").classList.remove("hidden");
            document.getElementById("payment-box").classList.add("hidden");

            document.getElementById("payment-instruction").innerText = `আপনার ${selectedMethod} একাউন্ট থেকে ${amount} টাকা এই নাম্বারে সেন্ড মানি করুন: ${selectedNumber}`;
        }

        function copyNumber() {
            navigator.clipboard.writeText(selectedNumber);
            alert("✅ নাম্বার কপি হয়েছে!");
        }

        function startCountdown() {
            let senderNumber = document.getElementById("sender-number").value;
            let trxId = document.getElementById("trx-id").value;

            // Check if 11 digits sender number and transaction ID are entered
            if (senderNumber.length !== 11) {
                alert("প্রেরকের নাম্বার ১১ ডিজিট হতে হবে!");
                return;
            }

            if (trxId === "") {
                alert("ট্রানজেকশন আইডি দিতে হবে!");
                return;
            }

            let count = 10;
            let countdownElement = document.getElementById("countdown");
            let timer = setInterval(() => {
                countdownElement.innerText = `♻️ পেমেন্ট প্রক্রিয়াধীন রয়েছে... ${count}s`;
                count--;
                if (count < 0) {
                    clearInterval(timer);
                    let sender = senderNumber.slice(-6);
                    let trx = trxId.slice(-5);
                    let paymentCode = sender + trx;
                    document.getElementById("payment-code-text").innerText = paymentCode;
                    document.getElementById("payment-code").classList.remove("hidden");
                    document.getElementById("copy-payment-code").classList.remove("hidden");
                    countdownElement.innerText = "✅ কোড তৈরি হয়েছে!";
                }
            }, 1000);
        }

        function copyPaymentCode() {
            let paymentCode = document.getElementById("payment-code-text").innerText;
            navigator.clipboard.writeText(paymentCode);
            alert("✅ পেমেন্ট কোড কপি হয়েছে!");
        }
    </script>

</body>
</html>
