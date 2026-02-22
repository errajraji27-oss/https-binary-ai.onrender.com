# https-binary-ai.onrender.com
index.html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>AI PRO SIGNAL</title>

<style>
body{
background:#0f172a;
color:white;
font-family:Arial;
text-align:center;
}

.container{
margin-top:40px;
background:#1e293b;
padding:30px;
border-radius:20px;
width:95%;
max-width:420px;
margin:auto;
box-shadow:0 0 25px #00f7ff;
}

.signal{
font-size:50px;
font-weight:bold;
margin:20px;
}

.buy{color:#00ff88;}
.sell{color:#ff004c;}

button{
padding:12px 18px;
border:none;
border-radius:10px;
background:#00f7ff;
color:black;
font-weight:bold;
margin:5px;
cursor:pointer;
}

select{
padding:8px;
border-radius:8px;
font-weight:bold;
}

.timer{
font-size:20px;
color:#facc15;
margin-top:10px;
}

.popup{
position:fixed;
top:20px;
left:50%;
transform:translateX(-50%);
background:#00ff88;
color:black;
padding:15px;
border-radius:10px;
display:none;
font-weight:bold;
}
</style>
</head>
<body>

<div class="popup" id="popup"></div>

<div class="container">

<h2>🔥 AI PRO SIGNAL</h2>

<select id="timeframe">
<option value="1">1 Minute</option>
<option value="5">5 Minutes</option>
<option value="15">15 Minutes</option>
</select>

<br><br>

<div id="pair">Loading...</div>

<div id="signal" class="signal"></div>

<div id="score"></div>

<div class="timer" id="timer">60</div>

<br>

<button onclick="getSignal()">🔄 Update</button>

</div>

<audio id="alertSound">
<source src="https://www.myinstants.com/media/sounds/notification.mp3">
</audio>

<script>

let timeLeft = 60;

async function getSignal(){

const tf = document.getElementById("timeframe").value;

const res = await fetch("https://YOUR-RENDER-LINK.onrender.com/?tf="+tf);
const data = await res.json();

if(data.pair){

document.getElementById("pair").innerText = "Pair: " + data.pair;
document.getElementById("score").innerText = "Strength: " + data.score + "%";

let signalDiv = document.getElementById("signal");
signalDiv.innerText = data.signal;
signalDiv.className = "signal " + (data.signal === "BUY" ? "buy" : "sell");

if(data.score >= 75){
showPopup("🔥 Strong Signal: "+data.signal);
document.getElementById("alertSound").play();
}

}
}

function showPopup(text){
let popup = document.getElementById("popup");
popup.innerText = text;
popup.style.display = "block";

setTimeout(()=>{
popup.style.display = "none";
},3000);
}

function countdown(){
timeLeft--;
document.getElementById("timer").innerText = timeLeft;

if(timeLeft <= 0){
timeLeft = 60;
getSignal();
}
}

setInterval(countdown,1000);
getSignal();

</script>

</body>
</html>
