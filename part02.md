# 运行程序	
## 创建TCP服务器
server.php
```php
//创建SERVER对象，监听127.0.0.1：9501端口
$serv = new swoole_server('127.0.0.1','9501');

//监听连接进入事件
$serv->on('connect', function ($serv, $fd) {  
    echo "Client: Connect.\n";
});

//监听数据接收事件
$serv->on('receive', function ($serv, $fd, $from_id, $data) {
    $serv->send($fd, "Server: ".$data);
});
	
//监听连接关闭事件
$serv->on('close', function ($serv, $fd) {
    echo "Client: Close.\n";
});
	
//启动服务器
$serv->start(); 
```

这里就创建了一个TCP服务器，监听本机9501端口。  
它的逻辑很简单，当客户端Socket通过网络发送一个 hello 字符串时，服务器会回复一个 Server: hello 字符串。

swoole_server是异步服务器，所以是通过监听事件的方式来编写程序的。  
当对应的事件发生时底层会主动回调指定的PHP函数。  
如当有新的TCP连接进入时会执行onConnect事件回调，当某个连接向服务器发送数据时会回调onReceive函数。	

	*  服务器可以同时被成千上万个客户端连接，$fd就是客户端连接的唯一标识符
	*  调用 $server->send() 方法向客户端连接发送数据，参数就是$fd客户端标识符
	*  调用 $server->close() 方法可以强制关闭某个客户端连接
	*  客户端可能会主动断开连接，此时会触发onClose事件回调

	

