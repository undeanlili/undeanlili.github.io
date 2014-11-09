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


<form action="">
<input type="button" value="Hello world!">
</form>

<a href="http://yanjixian.com">脸萌网站</a>

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


![老上海胭脂](2.jpg "上海")
![老上海胭脂](3.jpg "古镇")

