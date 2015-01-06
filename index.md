---
layout: page
title: 李志
tagline: 游戏机
---
{% include JB/setup %}


hello

<div id="footer" style="background-color:#FFA500;clear:both;text-align:center;">
<h1>这是一个游戏机的世界</h1></div>

<h2>这是一个中古游戏机的世界</h2>
<h3>这是中古的世界</h3>

<body style="background-color:yellow;">


<form action="">
<input type="button" value="Hello world!">
</form>

<a href="http://yanjixian.com">脸萌网站</a>

<audio controls>
<source src="1.m4a" type="audio/mpeg">
您的浏览器不支持 audio 元素。
</audio>


<p>游戏机公司介绍</p>

<p>目前3大游戏硬件制作商</p>
任天堂：最老牌儿的游戏制作商，到目前为止，共有一下几种硬件：

<p>家用机：</p>
<p>1⃣️机型Family Computer（FC，红白机）</p>
<p>2⃣️Super Family Computer（SFC，超任）</p>
<p>3⃣️Nintendo64(N64,海豚)</p>
<p>4⃣️Nintendo Game Cube(NGC)</p>
<p>5⃣️Wii</p>
<p>6⃣️WiiU</p>

<p>掌机：</p>
<p>1⃣️Game Boy(黑白)</p>
<p>2⃣️Game Boy Pocket</p>
<p>3⃣️Game Boy Color</p>
<p>4⃣️Game Boy Advance</p>
<p>5⃣️Game Boy Advance SP</p>
<p>6⃣️Game Boy MICRO</p>
<p>7⃣️Nintendo Dual Screen(NDS)</p>
<p>8⃣️Nintendo 3DS</p>

<p>传奇机：</p>
<p>1⃣️VB(Virtual Boy)</p>
<p>2⃣️64DD</p>

<p>索尼：从PS时代开始的硬件游戏厂商</p>

<p>家用机：</p>
<p>1⃣️Play Station(黑白)</p>
<p>2⃣️Play Station one(PS的轻量版)</p>
<p>3⃣️Play Station 2</p>
<p>4⃣️Play Station two(PS2的轻量版)</p>
<p>5⃣️Play Station 3</p>
<p>6⃣️Play Station 4</p>

<p>掌机：</p>
<p>1⃣️Play Station Portable(著名的掌机)</p>
<p>2⃣️PSP Go</p>
<p>3⃣️PS Vita</p>


KONAMI

</p>

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

<div id="footer" style="background-color:#FFA500;clear:both;text-align:center;">
这是一个神奇的网站</div>

</div>


![老上海胭脂](2.jpg "上海")
![老上海胭脂](3.jpg "古镇")

/**
 * Created by ELatA on 14-1-26.
 */

var http = require('http');
var path = require('path');
var express = require('express');
var db = require('./db');
var flash = require('connect-flash');
var store = require('connect-mysql')(express);

var Knex = require('knex');

Knex.knex = Knex.initialize({
    client:'mysql',
    connection:{
        host: 'localhost',
        user: 'root',
        password: 'root',
        database: 'simple_signin',
        charset  : 'utf8'
    }
})

var app = express();

//all environments

app.set('port', process.env.PORT || 4000);
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');
app.use(express.favicon());
/*app.use(express.logger('dev'));*/
app.use(express.json());
app.use(express.urlencoded());
app.use(express.methodOverride());
app.use(express.static(path.join(__dirname, 'public')));

// development only
if ('development' == app.get('env')) {
    app.use(express.errorHandler());
}

//cookie and session
app.use(express.cookieParser());
var options = {config: db.options};
app.use(express.session({ secret: 'just_a_key', store: new store(options)}));
app.use(flash());

//权限控制
function authChecker(req, res, next) {
    console.log(req.path);
    if (req.path.split("/")[1] && req.path.split("/")[1]=="sign" && !req.session.user) {
        res.redirect("/user/login");
    } else {
        next();
    }
}
app.use(authChecker);

//注册路由
var routes = require('./routes');
routes(app);

//启动app
http.createServer(app).listen(app.get('port'), function(){
    console.log('Express server listening on port ' + app.get('port'));
});
