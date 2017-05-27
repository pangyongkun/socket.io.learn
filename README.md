#  <center>nodejs之socke.io学习 </center>

	可用于对nodejs，npm入门学习。

##  1.初始化项目
	npm init
生成<a href='package.json'>package.json</a>,里面是项目的相关信息 
 </br> 
</br>
 
![Alt text](img/package.png)
##  2.下载依赖
	ipm install socket.io --save
![Alt text](img/install_socket_io.png)
##  3.新建<a href='server.js'>server.js</a>编写服务器代码
	//引入nodejs的http模块
	var app = require('http').createServer(handler)
	//引入socket.io模块
	var io = require('socket.io')(app);
	var fs = require('fs');
	//监听端口80
	app.listen(80);
	
	//http请求跳转到index.html页面
	function handler (req, res) {
	  fs.readFile(__dirname + '/index.html',
	  function (err, data) {
	    if (err) {
	      res.writeHead(500);
	      return res.end('Error loading index.html');
	    }
	
	    res.writeHead(200);
	    res.end(data);
	  });
	}
	
	//socke.io监听connection事件，这是默认事件
	io.on('connection', function (socket) {
	  //发送事件'news'(这是自定义事件),同时穿过去json数据
	  socket.emit('news', { hello: 'world' });
	
	  //监听自定义事件'hello'，回掉方法处理数据
	  socket.on('hello', function (data) {
	    console.log(data);
	  });
	});
****
这就实现了一个简单的socket信令服务。
##  4.启动服务器
	node server.js