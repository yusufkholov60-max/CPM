<!DOCTYPE html>
<html lang="tg">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CPM AUTO</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;background:#101318;color:white;
 font-family:Arial,sans-serif;
}
header{
 background:#202630;padding:20px;
 text-align:center;border-bottom:2px solid #00d68f;
}
h1{color:#00d68f;margin:5px}
.container{padding:15px;max-width:600px;margin:auto}
.card{
 background:#202630;padding:15px;
 border-radius:14px;margin:15px 0;
}
input,button,textarea{
 width:100%;padding:13px;margin:7px 0;
 border:0;border-radius:8px;font-size:16px;
}
input,textarea{background:#303946;color:white}
button{background:#00d68f;color:black;font-weight:bold}
img{width:100%;border-radius:10px}
.price{color:#00d68f;font-size:22px}
.hidden{display:none}
</style>
</head>
<body>

<header>
<h1>CPM AUTO</h1>
<p>Car Parking Multiplayer</p>
</header>

<div class="container">

<div class="card">
<h2>🚗 Мошинҳои фурӯш</h2>
<h3>Ҳамагӣ: <span id="count">0</span> мошин</h3>
</div>

<div id="cars"></div>

<div class="card">
<h2>👑 Admin</h2>
<input id="password" type="password"
placeholder="Пароли Admin">
<button onclick="login()">Даромад ба Admin</button>
</div>

<div id="admin" class="hidden card">
<h2>Иловаи мошин</h2>
<input id="name" placeholder="Номи мошин">
<input id="price" placeholder="Нархи мошин">
<input id="photo" type="file" accept="image/*">
<textarea id="info" placeholder="Маълумоти мошин"></textarea>
<button onclick="addCar()">Илова кардан</button>
<button onclick="logout()">Баромадан</button>
</div>

</div>

<script>
let cars=JSON.parse(localStorage.getItem("cars")||"[]");

function save(){
 localStorage.setItem("cars",JSON.stringify(cars));
 show();
}

function login(){
 if(document.getElementById("password").value==="YSF2026"){
 document.getElementById("admin").classList.remove("hidden");
 alert("Хуш омадӣ, Admin!");
 }else{
 alert("Парол нодуруст аст!");
 }
}

function logout(){
 document.getElementById("admin").classList.add("hidden");
}

function addCar(){
 let name=document.getElementById("name").value;
 let price=document.getElementById("price").value;
 let file=document.getElementById("photo").files[0];
 let info=document.getElementById("info").value;

 if(!name||!price||!file){
 alert("Ҳамаи маълумоти лозимиро пур кун!");
 return;
 }

 let reader=new FileReader();
 reader.onload=function(){
 cars.push({name,price,photo:reader.result,info});
 save();
 alert("Мошин илова шуд!");
 };
 reader.readAsDataURL(file);
}

function delCar(i){
 if(confirm("Мошинро нест мекунӣ?")){
 cars.splice(i,1);
 save();
 }
}

function show(){
 document.getElementById("count").innerText=cars.length;
 document.getElementById("cars").innerHTML=cars.map((c,i)=>`
 <div class="card">
 <img src="${c.photo}">
 <h2>${c.name}</h2>
 <p class="price">${c.price}</p>
 <p>${c.info||""}</p>
 <button onclick="alert('Барои фармоиш ба Admin муроҷиат кунед')">
 Фармоиш
 </button>
 <button onclick="delCar(${i})">🗑️ Нест кардан</button>
 </div>
 `).join("");
}
show();
</script>
</body>
</html># CPM
CPM Car Marketplace - Online Car Sales
