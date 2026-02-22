
<html lang="ku">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Daro.dev | ژمێریاری زەکات</title>

<style>
body{
font-family: "Noto Sans Arabic", sans-serif;
background: linear-gradient(135deg,#0f172a,#1e293b);
color:white;
margin:0;
padding:0;
display:flex;
align-items:center;
justify-content:center;
height:100vh;
}

.card{
background:#111827;
padding:30px;
border-radius:16px;
width:95%;
max-width:420px;
box-shadow:0 10px 25px rgba(0,0,0,0.4);
text-align:center;
}

.logo{
font-size:26px;
font-weight:bold;
margin-bottom:5px;
color:#22c55e;
}

.subtitle{
font-size:14px;
opacity:0.8;
margin-bottom:20px;
}

input{
width:100%;
padding:14px;
margin:8px 0;
border-radius:10px;
border:none;
font-size:16px;
}

button{
width:100%;
padding:14px;
margin-top:12px;
border:none;
border-radius:10px;
background:#22c55e;
color:#022c22;
font-size:18px;
font-weight:bold;
}

.result{
margin-top:18px;
font-size:22px;
font-weight:bold;
color:#4ade80;
}

.footer{
margin-top:15px;
font-size:12px;
opacity:0.6;
}
</style>
</head>

<body>

<div class="card">
<div class="logo">Daro.dev</div>
<div class="subtitle">ژمێریاری زەکات</div>

<input type="number" id="money" placeholder="کۆی پارە (IQD)">
<input type="number" id="gold" placeholder="بڕی ئاڵتوون (گرام)">
<input type="number" id="silver" placeholder="بڕی زیو (گرام)">

<button onclick="calc()">ئەژمارکردن</button>

<div class="result" id="result">زەکات: 0 IQD</div>

<div class="footer">© Daro.dev</div>
</div>

<script>
function calc(){
let money = parseFloat(document.getElementById("money").value)||0;
let gold = parseFloat(document.getElementById("gold").value)||0;
let silver = parseFloat(document.getElementById("silver").value)||0;

// نرخەکان (دەتوانیت بگۆڕیت)
let goldPrice = 100000; 
let silverPrice = 1200;

let total = money + (gold*goldPrice) + (silver*silverPrice);
let zakat = total * 0.025;

document.getElementById("result").innerText =
"زەکات: " + zakat.toLocaleString() + " IQD";
}
</script>

</body>
</html>
