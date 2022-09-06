---
layout: post
title: javascript with websocket
tags: [持久积累, javascript, websocket]
---

# js实现webSocket客户端

# 1\. websocket

由于http请求只能由客户端发起，所有当服务器资源有变化时，客户端只能通过轮询的方式。非常浪费资源。

websocket的特点：

*   服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话，属于服务器推送技术的一种
*   建立在 TCP 协议之上，服务器端的实现比较容易

*   可以发送文本，也可以发送二进制数据

*   没有同源限制，客户端可以与任意服务器通信

*   协议标识符是ws（如果加密，则为wss），服务器网址就是 URL。如ws:localhost:8080/msg

# 2\. 简单示例

```javascript
var ws = new WebSocket("ws://localhost:8080/msg");
 
ws.onopen = function(evt) {
	console.log("Connection open ...");
	ws.send("Hello WebSockets!");
};
 
ws.onmessage = function(evt) {
	console.log("Received Message: " + evt.data);
	ws.close();
};
 
ws.onclose = function(evt) {
	console.log("Connection closed.");
};
```

# 3\. api

## 1\. websocket构造函数

用于创建一个webSocket实例，执行后，客户端就会与服务端连接

```javascript
var ws = new WebSocket("ws://localhost:8080/msg");
```

## 2. webSocket.readyState

readyState属性返回实例对象的当前状态，共有四种。

*   CONNECTING：值为0，表示正在连接。
*   OPEN：值为1，表示连接成功，可以通信了。
*   CLOSING：值为2，表示连接正在关闭。
*   CLOSED：值为3，表示连接已经关闭，或者打开连接失败

例如：if(ws.readyState ==WebSocket.CONNECTING ){}

## 3. webSocket.onopen

用于指定连接成功后的回调函数

```javascript
ws.onopen = function(evt) {
	console.log("Connection open ...");
	ws.send("Hello WebSockets!");
};
```

或者：

```javascript
ws.addEventListener('open', function (event) {
  ws.send('Hello Server!');
});
```

## 4. webSocket.onclose

用于指定连接关闭后的回调函数。

```javascript
ws.onclose = function(event) {
  var code = event.code;
  var reason = event.reason;
  var wasClean = event.wasClean;
};
 
ws.addEventListener("close", function(event) {
  var code = event.code;
  var reason = event.reason;
  var wasClean = event.wasClean;
});ws.onclose = function(event) {  var code = event.code;  var reason = event.reason;  var wasClean = event.wasClean;}; ws.addEventListener("close", function(event) {  var code = event.code;  var reason = event.reason;  var wasClean = event.wasClean;});
```

## 5. webSocket.onmessage

用于指定收到服务器数据后的回调函数

```javascript
ws.onmessage = function(event) {
  var data = event.data;
};
 
ws.addEventListener("message", function(event) {
  var data = event.data;
});
```

服务器数据有可能是文本，也有可能是二进制数据，需要判断

```javascript
ws.onmessage = function(event){
  if(typeof event.data === String) {
    console.log("Received data string");
  }
 
  if(event.data instanceof ArrayBuffer){
    var buffer = event.data;
    console.log("Received arraybuffer");
  }
}
```

除了动态判断收到的数据类型，也可以使用binaryType属性，显式指定收到的二进制数据类型

```javascript
// 收到的是 blob 数据
ws.binaryType = "blob";
ws.onmessage = function(e) {
  console.log(e.data.size);
};
 
// 收到的是 ArrayBuffer 数据
ws.binaryType = "arraybuffer";
ws.onmessage = function(e) {
  console.log(e.data.byteLength);
};
```

## 6. webSocket.send（）

send方法用于向服务器发送数据

*   发送文本

```javascript
ws.send("Hello WebSockets!");
```

*   发送Blob数据

```javascript
var file = document
  .querySelector('input[type="file"]')
  .files[0];
ws.send(file);
```

*   发送ArrayBuffer

```javascript
var img = canvas_context.getImageData(0, 0, 400, 320);
var binary = new Uint8Array(img.data.length);
for (var i = 0; i < img.data.length; i++) {
  binary[i] = img.data[i];
}
ws.send(binary.buffer);
```

## 7\. webSocket.bufferedAmount

bufferedAmount属性，表示还有多少字节的二进制数据没有发送出去。它可以用来判断发送是否结束

```javascript
var data = new ArrayBuffer(10000000);
socket.send(data);
 
if (socket.bufferedAmount === 0) {
  // 发送完毕
} else {
  // 发送还没结束
}
```

## 8. webSocket.onerror

用于指定报错时的回调函数

```javascript
ws.onerror = function(event) {
};
 
es.addEventListener("error", function(event) {
});
```
