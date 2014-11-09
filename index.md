---
layout: page
title: 李志
tagline: 游戏机
---
{% include JB/setup %}


hello

<h1>这是一个游戏机的世界</h1>
<h2>这是一个中古游戏机的世界</h2>
<h3>这是中古的世界</h3>

<body style="background-color:yellow;">
<h2 style="background-color:red;">This is a heading</h2>
<p style="background-color:green;">This is a paragraph.</p>

<form action="">
<input type="button" value="Hello world!">
</form>


</body>

<script>
var x=document.getElementById("demo");
function getLocation()
{
if (navigator.geolocation)
{
navigator.geolocation.getCurrentPosition(showPosition);
}
else{x.innerHTML="该浏览器不支持获取地理位置。";}
}
function showPosition(position)
{
x.innerHTML="Latitude: " + position.coords.latitude + 
"<br>Longitude: " + position.coords.longitude; 
}
</script>

![帅](1.jpg "脸")


