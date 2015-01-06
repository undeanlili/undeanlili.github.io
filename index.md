
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
