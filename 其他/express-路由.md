#express-路由
#### 路由方法
路由方法源于 HTTP 请求方法，和 express 实例相关联。
下面这个例子展示了为应用跟路径定义的 GET 和 POST 请求：
```js
//GET method route
app.get('/', function (req, res) {
  res.send('GET request to the homepage');
});

//POST method route
app.post('/', function (req, res) {
  res.send('POST request to the homepage');
});
```
app.all()是一个特殊的路由方法，没有任何HTTP方法与其对应，它的作用是对于一个路劲上的所有请求加载中间件。
#### 路由路径
路由路径和请求方法一起定义了请求的端点，它可以使字符串、字符串模式或者正则表达式。

##### 使用字符串的路由路径示例：
```js
//匹配根路径的请求
app.get('/', function (req, res) {
  res.send('root');
});
//匹配/random.text路径的请求
app.get('/rendom.text', function (req, res) {
  res.send('random.text');
})
```

##### 使用字符串模式
```js
//匹配acd和abcd
app.get('/ab?cd', function(req. res) {
  res.send('ab?cd');
});
//ab + cd、ab*cd
```

##### 正则表达式的路由路径示例
```js
//匹配任何路径中含有a的路径
app.get(/a/,  funciton(req,res) {
        res.send('/a/');
});
//注意正则表达式的使用
```

#### 路由句柄
可以为请求处理提供多个回调函数，其行为类似 中间件。唯一的区别是这些回调函数有可能调用 next('route') 方法而略过其他路由回调函数。可以利用该机制为路由定义前提条件，如果在现有路径上继续执行没有意义，则可将控制权交给剩下的路径。
路由句柄有多种形式，可以是一个函数、一个函数数组，或者是两者混合，如下所示.
##### 一个回调函数处理路由
```js
app.get('/', function( req, res) {
  res.send('Hello from A!');
});
```
##### 多个回调函数处理路由
```js
app.get('/', function (req, res, next) {
  console.log('reqonse will be sent by the next function ...');
  next( );
}, function (req, res) {
  res.send('Hello from B!');
});
```

##### 回调函数数组处理路由
```js
var cb0 = function (req, res, next) {
  console.log('CB0');
  next();
}

var cb1 = function (req, res, next) {
  console.log('CB1');
  next();
}

var cb2 = function (req, res) {
  res.send('Hello from C!');
}

app.get('/example/c', [cb0, cb1, cb2]);
```
#### 响应方法
|方法|描述|
|:--|:--|
|res.download()|提示下载文件|
|res.end()|终结响应处理流程|
|res.json()|发送一个JSON格式的响应|
|res.jsonp()|发送一个支持JSONP的JSON格式的响应|
|res.redirect()|重定向请求|
|res.render()|渲染视图模板|
|res.send()|发送各种类型的响应|
|res.sendFile|以八字节流的形式发送文件|
|res.sendStatus()|设置响应状态码，并将其以字符串形式作为响应体的一部分发送|

#### express.Router
可使用 express.Router 类创建模块化、可挂载的路由句柄。Router 实例是一个完整的中间件和路由系统，因此常称其为一个 “mini-app”。
下面的实例程序创建了一个路由模块，并加载了一个中间件，定义了一些路由，并且将它们挂载至应用的路径上。
在 app 目录下创建名为 birds.js 的文件，内容如下：
```js
var express = require('express');
var router = express.Router();

// 该路由使用的中间件
router.use(function timeLog(req, res, next) {
  console.log('Time: ', Date.now());
  next();
});
// 定义网站主页的路由
router.get('/', function(req, res) {
  res.send('Birds home page');
});
// 定义 about 页面的路由
router.get('/about', function(req, res) {
  res.send('About birds');
});

module.exports = router;
```