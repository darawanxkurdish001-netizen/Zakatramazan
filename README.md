
<html lang="ku" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Daro.dev | ژمێریاری زەکات</title>

<style>
body{margin:0;font-family:"Noto Sans Arabic",sans-serif;background:#f3f4f6;color:#111827}
.wrapper{max-width:540px;margin:auto;padding:24px 16px 40px}
.title{font-size:28px;font-weight:700;margin-bottom:10px}
.desc{font-size:15px;color:#4b5563;line-height:1.7;margin-bottom:18px}
.prices{background:#fff;border:1px solid #e5e7eb;border-radius:10px;padding:12px 14px;font-size:14px;margin-bottom:18px;line-height:1.7}
.field{margin-bottom:16px}
label{display:block;margin-bottom:6px;font-size:14px;color:#374151}
input{width:100%;padding:14px;border-radius:8px;border:1px solid #d1d5db;font-size:16px;text-align:right}
.result{margin-top:22px;padding:16px;border-radius:10px;background:white;border:1px solid #e5e7eb;line-height:1.8;font-size:16px;text-align:right}
.ok{color:#16a34a;font-weight:600}
.no{color:#dc2626;font-weight:600}
.footer{margin-top:30px;font-size:13px;color:#6b7280;text-align:center}
</style>
</head>
<body>

<div class="wrapper">
<div class="title">ژمێریاری زەکات</div>
<div class="desc">ئەگەر ژمارەکان نووسرا نەبن، خۆکار زیاد دەبن و زەکات یاد دەکرێت.</div>

<div class="prices" id="prices">هێنانی نرخەکان...</div>

<div class="field">
<label>پارەی هەبوو (IQD)</label>
<input type="number" id="money" placeholder="3,000,000">
</div>

<div class="field">
<label>زێر (گرام)</label>
<input type="number" id="gold" placeholder="0">
</div>

<div class="field">
<label>زیو (گرام)</label>
<input type="number" id="silver" placeholder="0">
</div>

<div class="field">
<label>دۆلار (USD)</label>
<input type="number" id="usd" placeholder="0">
</div>

<div class="result" id="result">ئەنجامی ژمێریار لێرە دەردەکەوێت</div>
<div class="footer">© Daro.dev</div>
</div>

<script>
let goldPriceIQD = 100000;
let silverPriceIQD = 1200;
let usdRate = 1500;

/* هێنانی نرخەکان live */
async function loadPrices(){
try{
  let goldRes = await fetch("https://api.metals.live/v1/spot/gold");
  let goldData = await goldRes.json();
  goldPriceIQD = (goldData[0].price / 31.1035) * usdRate;

  let silverRes = await fetch("https://api.metals.live/v1/spot/silver");
  let silverData = await silverRes.json();
  silverPriceIQD = (silverData[0].price / 31.1035) * usdRate;

  let usdRes = await fetch("https://open.er-api.com/v6/latest/USD");
  let usdData = await usdRes.json();
  usdRate = usdData.rates.IQD;

  document.getElementById("prices").innerHTML =
  "نرخی زێر: " + goldPriceIQD.toFixed(0) + " IQD / گرام<br>" +
  "نرخی زیو: " + silverPriceIQD.toFixed(0) + " IQD / گرام<br>" +
  "نرخی دۆلار: " + usdRate.toFixed(0) + " IQD";

  autoCalc();

}catch(e){
  document.getElementById("prices").innerText="نەتوانرا نرخەکان بهێنرێت";
  console.error(e);
}
}

loadPrices();
setInterval(loadPrices,10*60*1000);

function autoCalc(){
  let money = document.getElementById("money").value;
  let gold = document.getElementById("gold").value;
  let silver = document.getElementById("silver").value;
  let usd = document.getElementById("usd").value;

  /* ئەگەر خالی بوو، placeholder زیاد دەکرێت */
  money = money ? parseFloat(money.replace(/,/g,"")) : 3000000;
  gold = gold ? parseFloat(gold) : 0;
  silver = silver ? parseFloat(silver) : 0;
  usd = usd ? parseFloat(usd) : 0;

  let usdIQD = usd * usdRate;
  let total = money + (gold*goldPriceIQD) + (silver*silverPriceIQD) + usdIQD;

  let nisab = 3000000;
  let zakat = total * 0.025;

  let r = document.getElementById("result");
  if(total >= nisab){
    r.innerHTML =
    "<span class='ok'>زەکات واجبە</span><br>" +
    "کۆی سامان: " + total.toLocaleString() + " IQD<br>" +
    "بڕی زەکات: " + zakat.toLocaleString() + " IQD";
  }else{
    r.innerHTML =
    "<span class='no'>نیصاب نەگەیشتووە</span><br>" +
    "کۆی سامان: " + total.toLocaleString() + " IQD<br>" +
    "نیصابی پێویست: " + nisab.toLocaleString() + " IQD";
  }
}

/* خۆکار زیادکردن placeholder + value لە load + input */
["money","gold","silver","usd"].forEach(id=>{
  const el = document.getElementById(id);
  el.addEventListener("input", autoCalc);
});

window.addEventListener("load", autoCalc);

</script>

</body>
</html>
