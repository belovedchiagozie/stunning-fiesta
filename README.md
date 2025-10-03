<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pay $10 in BNB</title>
  <style>
    body { font-family: Arial, sans-serif; background: #f5f5f5; text-align: center; padding: 50px; }
    .container { background: #fff; padding: 30px; border-radius: 10px; box-shadow: 0 0 15px rgba(0,0,0,0.1); display: inline-block; }
    h1 { color: #f3ba2f; }
    p { font-size: 18px; margin: 15px 0; }
    .wallet { font-weight: bold; font-size: 20px; color: #333; word-break: break-all; }
    .amount { font-size: 24px; font-weight: bold; color: #333; }
    button { padding: 10px 20px; font-size: 16px; margin-top: 10px; cursor: pointer; background: #f3ba2f; border: none; border-radius: 5px; color: #fff; }
    canvas { margin-top: 20px; }
  </style>
</head>
<body>
  <div class="container">
    <h1>Pay $10 in BNB</h1>
    <p>Send exactly $10 worth of BNB to this wallet:</p>
    <p class="wallet">0x18cc9a408760fc1d50a3ff9c94f14619fcdf5e0b</p>
    <button onclick="copyWallet()">Copy Wallet Address</button>
    <p>Scan QR code to pay:</p>
    <div id="qrcode"></div>
    <p>Amount: <span class="amount" id="amount">Loading...</span></p>
    <p><small>Check current BNB price to send the correct amount.</small></p>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
  <script>
    // Generate QR code
    new QRCode(document.getElementById("qrcode"), {
      text: "0x18cc9a408760fc1d50a3ff9c94f14619fcdf5e0b",
      width: 200,
      height: 200
    });

    // Function to copy wallet address
    function copyWallet() {
      const wallet = document.querySelector(".wallet").innerText;
      navigator.clipboard.writeText(wallet).then(() => {
        alert("Wallet address copied!");
      });
    }

    // Fetch current BNB price and calculate amount
    fetch('https://api.coingecko.com/api/v3/simple/price?ids=binancecoin&vs_currencies=usd')
      .then(response => response.json())
      .then(data => {
        const bnbPrice = data.binancecoin.usd;
        const amount = (10 / bnbPrice).toFixed(6); // Calculate amount for $10
        document.getElementById("amount").innerText = `${amount} BNB`;
      })
      .catch(error => {
        console.error('Error fetching BNB price:', error);
        document.getElementById("amount").innerText = 'Error fetching price';
      });
  </script>
</body>
</html>
