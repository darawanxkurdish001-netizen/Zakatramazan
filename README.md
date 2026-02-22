                    
<html lang="ku" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Daro.dev | ژمێریاری زەکات</title>

<style>
body{
margin:0;
font-family:"Noto Sans Arabic",sans-serif;
background:#0f172a;
color:#e5e7eb;
display:flex;
justify-content:center;
align-items:center;
min-height:100vh;
}

.container{
width:95%;
max-width:480px;
background:#111827;
border-radius:18px;
padding:28px;
box-shadow:0 15px 35px rgba(0,0,0,.4);
}

.logo{
font-size:28px;
font-weight:bold;
color:#22c55e;
text-align:center;
}

.subtitle{
text-align:center;
opacity:.7;
margin-bottom:22px;
}

label{
font-size:14px;
opacity:.8;
}

input{
width:100%;
padding:14px;
margin:6px 0 14px 0;
border-radius:10px;
border:1px solid #1f2937;
background:#020617;
color:white;
font-size:16px;
}

button{
width:100%;
padding:15px;
border:none;
border-radius:12px;
background:#22c55e;
color:#022c22;
font-size:18px;
font-weight:bold;
cursor:pointer;
}

button:hover{
opacity:.9;
}

.result{
margin-top:18px;
padding:14px;
border-radius:12px;
background:#020617;
font-size:18px;
line-height:1.7;
}

.ok{color:#4ade80;}
.no{color:#f87171;}

.footer{
margin-top:14px;
text-align:center;
font-size:12px;
opacity:.6;
}
</style>
</head>

<body>

<div class="container">
<div class="logo">Daro.dev</div>
<div class="subtitle">ژمێریاری زەکات</div>

<label>پارەی هەبوو (IQD)</label>
<input type="number" id="money" placeholder="0">

<label>بڕی ئاڵتوون (گرام)</label>
<input type="number" id="gold" placeholder="0">

<label>بڕی زیو (گرام)</label>
<input type="number" id="silver" placeholder="0">

<button onclick="calc()">حیسابکردن</button>

<div class="result" id="result">
زانیاری دەردەکەوێت لێرە
</div>

<div class="footer">© Daro.dev</div>
</div>

<script>
function calc(){

let money = parseFloat(document.getElementById("money").value)||0;
let gold = parseFloat(document.getElementById("gold").value)||0;
let silver = parseFloat(document.getElementById("silver").value)||0;

/* نرخەکان (دەتوانیت بگۆڕیت) */
let goldPrice = 100000; 
let silverPrice = 1200;

/* نیصاب */
let nisabGold = 85 * goldPrice;
let nisabSilver = 595 * silverPrice;
let nisab = Math.min(nisabGold, nisabSilver);

/* کۆی سامانی */
let total = money + (gold*goldPrice) + (silver*silverPrice);

/* زەکات */
let zakat = total * 0.025;

let resultBox = document.getElementById("result");

if(total >= nisab){
resultBox.innerHTML =
"<span class='ok'>✔ زەکات واجبە</span><br>" +
"کۆی سامانی: " + total.toLocaleString() + " IQD<br>" +
"بڕی زەکات: " + zakat.toLocaleString() + " IQD";
}else{
resultBox.innerHTML =
"<span class='no'>✖ نیصاب نەگەیشتووە</span><br>" +
"کۆی سامانی: " + total.toLocaleString() + " IQD<br>" +
"نیصابی پێویست: " + nisab.toLocaleString() + " IQD";
}

}
</script>

</body>
</html>
