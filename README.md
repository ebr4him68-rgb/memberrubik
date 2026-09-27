# memberrubik
MemberRubik - Rubika membership service
```html
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Change90 | تبدیل Bitcoin به Dogecoin</title>
<meta name="description" content="Change90 - تبدیل Bitcoin به Dogecoin">

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Tahoma, Arial, sans-serif;
  background: #0b5fa5;
  color: #222;
}

header {
  background: #222;
  color: white;
  text-align: center;
  padding: 30px 15px;
}

.change90-logo {
  font-size: 30px;
  font-weight: bold;
  margin-bottom: 18px;
}

.green-light {
  width: 14px;
  height: 14px;
  background: #00ff66;
  border-radius: 50%;
  display: inline-block;
  margin-left: 7px;
  box-shadow: 0 0 12px #00ff66;
  animation: blink 1.2s infinite;
}

.blink-text {
  animation: blinkText 1.5s infinite;
}

@keyframes blink {
  0%, 45% {
    opacity: 1;
    box-shadow: 0 0 14px #00ff66;
  }

  50%, 100% {
    opacity: .25;
    box-shadow: none;
  }
}

@keyframes blinkText {
  0%, 50% {
    opacity: 1;
  }

  55%, 100% {
    opacity: .35;
  }
}

header h1 {
  margin: 0 0 20px;
  font-size: 28px;
}

.prices {
  display: flex;
  justify-content: center;
  gap: 15px;
  flex-wrap: wrap;
}

.price-box {
  background: #292929;
  border-radius: 14px;
  padding: 15px 25px;
  min-width: 210px;
}

.price-box .name {
  font-size: 15px;
  color: #ccc;
}

.price-box .price {
  font-size: 25px;
  font-weight: bold;
  margin-top: 7px;
}

.container {
  max-width: 650px;
  margin: 25px auto;
  padding: 0 15px;
}

.card {
  background: white;
  border-radius: 18px;
  padding: 25px;
  margin-bottom: 20px;
  box-shadow: 0 5px 25px rgba(0,0,0,.08);
}

h2 {
  text-align: center;
  margin-top: 0;
}

label {
  display: block;
  margin: 15px 0 7px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 10px;
  font-size: 17px;
  direction: ltr;
  text-align: left;
}

button {
  width: 100%;
  border: 0;
  border-radius: 10px;
  padding: 15px;
  margin-top: 15px;
  font-size: 17px;
  font-weight: bold;
  cursor: pointer;
  background: #f2c94c;
}

.result {
  margin-top: 20px;
  padding: 18px;
  background: #f4f5f7;
  border-radius: 12px;
  text-align: center;
}

.doge-result {
  font-size: 28px;
  font-weight: bold;
  margin-top: 8px;
}

.address {
  direction: ltr;
  word-break: break-all;
  background: #f1f2f4;
  border: 1px solid #ddd;
  padding: 15px;
  border-radius: 10px;
  text-align: center;
  font-family: monospace;
  font-size: 15px;
}

#btcQR {
  display: flex;
  justify-content: center;
  margin: 20px 0;
}

.notice {
  background: #fff7d6;
  padding: 15px;
  border-radius: 10px;
  line-height: 1.9;
  font-size: 14px;
  margin-top: 15px;
}

.hidden {
  display: none;
}

.status {
  text-align: center;
  color: #ccc;
  font-size: 13px;
  margin-top: 10px;
}

footer {
  text-align: center;
  padding: 25px;
  color: white;
  font-size: 13px;
}
</style>
</head>

<body>

<header>

  <div class="change90-logo">
    <span class="green-light"></span>
    Change90
  </div>

  <h1>₿ تبدیل Bitcoin به Dogecoin 🐕</h1>

  <div class="prices">

    <div class="price-box">
      <div class="name blink-text">
        🟢 Bitcoin (BTC)
      </div>

      <div class="price" id="btcPrice">
        در حال دریافت...
      </div>
    </div>

    <div class="price-box">
      <div class="name blink-text">
        🟢 Dogecoin (DOGE)
      </div>

      <div class="price" id="dogePrice">
        در حال دریافت...
      </div>
    </div>

  </div>

  <div class="status" id="priceStatus">
    در حال دریافت قیمت لحظه‌ای...
  </div>

</header>


<div class="container">

  <div class="card">

    <h2>🔄 تبدیل BTC به DOGE</h2>

    <label for="btcAmount">
      مقدار Bitcoin موردنظر:
    </label>

    <input
      id="btcAmount"
      type="number"
      min="0"
      step="0.00000001"
      placeholder="مثلاً 0.001"
      oninput="calculateDoge()"
    >

    <div class="result">

      <div>
        مقدار تقریبی Dogecoin دریافتی:
      </div>

      <div
        class="doge-result"
        id="dogeAmount"
      >
        0 DOGE
      </div>

    </div>

    <button onclick="continueOrder()">
      ادامه →
    </button>

  </div>


  <div
    class="card hidden"
    id="paymentCard"
  >

    <h2>📥 ارسال Bitcoin</h2>

    <div class="notice">

      مقدار Bitcoin که وارد کردید:
      <strong id="btcToSend">0 BTC</strong>

      <br><br>

      مقدار تقریبی Dogecoin:
      <strong id="dogeToReceive">0 DOGE</strong>

      <br><br>

      پس از بررسی دریافت Bitcoin،
      مبلغ DOGE به آدرس DOGE شما ارسال خواهد شد.

    </div>


    <h3>
      آدرس Bitcoin برای پرداخت
    </h3>

    <div class="address">
      1Q99GpYnEU9yELNLjiJUWopNT1HatRYQrV
    </div>

    <div id="btcQR"></div>

    <button onclick="copyBTC()">
      📋 کپی آدرس Bitcoin
    </button>


    <label for="dogeAddress">
      آدرس Dogecoin خود را وارد کنید:
    </label>

    <input
      id="dogeAddress"
      type="text"
      placeholder="آدرس DOGE"
    >

    <button onclick="submitOrder()">
      ثبت درخواست تبدیل
    </button>

  </div>


  <div
    class="card hidden"
    id="orderCard"
  >

    <h2>✅ درخواست ثبت شد</h2>

    <div
      class="notice"
      id="orderInfo"
    ></div>

    <p style="text-align:center">
      وضعیت سفارش:
      <strong>
        در انتظار بررسی پرداخت Bitcoin
      </strong>
    </p>

  </div>

</div>


<footer>
  <strong>Change90</strong>
  <br>
  BTC → DOGE
  <br>
  نرخ‌ها تقریبی و بر اساس داده بازار هستند.
</footer>


<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>

<script>

const BTC_ADDRESS =
"1Q99GpYnEU9yELNLjiJUWopNT1HatRYQrV";

let btcPrice = 0;
let dogePrice = 0;


async function loadPrices() {

  try {

    const response = await fetch(
      "https://api.coingecko.com/api/v3/simple/price" +
      "?ids=bitcoin,dogecoin&vs_currencies=usd"
    );

    if (!response.ok) {
      throw new Error("Price API error");
    }

    const data = await response.json();

    btcPrice = data.bitcoin.usd;
    dogePrice = data.dogecoin.usd;

    document.getElementById("btcPrice").textContent =
      "$" + btcPrice.toLocaleString();

    document.getElementById("dogePrice").textContent =
      "$" + dogePrice.toLocaleString();

    document.getElementById("priceStatus").textContent =
      "قیمت‌ها به‌صورت خودکار به‌روزرسانی می‌شوند.";

    calculateDoge();

  } catch (error) {

    document.getElementById("priceStatus").textContent =
      "دریافت قیمت ناموفق بود؛ دوباره تلاش کنید.";

  }
}


function calculateDoge() {

  const btc =
    parseFloat(
      document.getElementById("btcAmount").value
    );

  if (!btc || btc <= 0 || !btcPrice || !dogePrice) {

    document.getElementById("dogeAmount").textContent =
      "0 DOGE";

    return;
  }

  const doge =
    (btc * btcPrice) / dogePrice;

  document.getElementById("dogeAmount").textContent =
    doge.toLocaleString(
      undefined,
      {
        maximumFractionDigits: 2
      }
    ) + " DOGE";
}


function continueOrder() {

  const btc =
    parseFloat(
      document.getElementById("btcAmount").value
    );

  if (!btc || btc <= 0) {

    alert(
      "لطفاً مقدار Bitcoin را وارد کنید."
    );

    return;
  }

  if (!btcPrice || !dogePrice) {

    alert(
      "قیمت هنوز دریافت نشده است. چند ثانیه صبر کنید."
    );

    return;
  }

  const doge =
    (btc * btcPrice) / dogePrice;

  document.getElementById("btcToSend").textContent =
    btc + " BTC";

  document.getElementById("dogeToReceive").textContent =
    doge.toLocaleString(
      undefined,
      {
        maximumFractionDigits: 2
      }
    ) + " DOGE";

  document.getElementById("paymentCard")
    .classList.remove("hidden");

  document.getElementById("paymentCard")
    .scrollIntoView({
      behavior: "smooth"
    });

  const qr =
    document.getElementById("btcQR");

  qr.innerHTML = "";

  new QRCode(
    qr,
    {
      text: "bitcoin:" + BTC_ADDRESS,
      width: 220,
      height: 220
    }
  );
}


function copyBTC() {

  navigator.clipboard
    .writeText(BTC_ADDRESS)

    .then(function() {

      alert(
        "آدرس Bitcoin کپی شد ✅"
      );

    })

    .catch(function() {

      alert(
        "کپی خودکار انجام نشد."
      );

    });
}


function submitOrder() {

  const dogeAddress =
    document.getElementById("dogeAddress")
      .value
      .trim();

  const btc =
    document.getElementById("btcAmount").value;

  if (!dogeAddress) {

    alert(
      "لطفاً آدرس Dogecoin خود را وارد کنید."
    );

    return;
  }

  const orderId =
    "BTCDOGE-" + Date.now();

  document.getElementById("orderInfo")
    .innerHTML =

    "<strong>شماره سفارش:</strong> " +
    orderId +

    "<br><br>" +

    "<strong>Bitcoin:</strong> " +
    btc +
    " BTC" +

    "<br><br>" +

    "<strong>آدرس DOGE:</strong><br>" +
    dogeAddress +

    "<br><br>" +

    "لطفاً تراکنش Bitcoin را به آدرس اعلام‌شده ارسال کنید و TXID را برای پیگیری سفارش نگه دارید.";

  document.getElementById("orderCard")
    .classList.remove("hidden");

  document.getElementById("orderCard")
    .scrollIntoView({
      behavior: "smooth"
    });
}


loadPrices();

setInterval(
  loadPrices,
  60000
);

</script>

</body>
</html>
```
