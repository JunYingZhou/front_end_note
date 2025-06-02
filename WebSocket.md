# WebSocket

## 一、原理（请求）

![image-20240402175913341](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402175913341.png)

## 二、信息推送常见方式

![image-20240402180201914](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402180201914.png)

数据流：**源源不断的将数据给客户端**

服务器有数据变化时将数据流式传输给客户端

## 三、websocket

**基于TCP连接进行全双工的通讯协议**

全双工： 允许数据在两个方向**同时传输**  类似@provider

半双工：允许数据在两个方向上传输，但是同一个时间段只**允许一个方向传输**

轮询与websocket的区别

![image-20240402181101150](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402181101150.png)

原理：
![image-20240402181154489](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402181154489.png)

请求数据：

```js
GET ws://localhost/chat HTTP/1.1
Host: localhost
Connection:Upgrade
Upgrade: websocket
Sec-WebSocket-Version:13
Sec-WebSocket-Key:dGhlHNhbXBsZSBub25jzQ==
Sec-WebSocket-Extensions: permessage-deflate
```

响应数据：

```js
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept:s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
Sec-WebSocket-Extensions: permessage-deflate
```

## 四、websocket API

### 客户端：

websocket对象创建：

```js
let ws = new Websocket(URL)
```

![image-20240402181705240](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402181705240.png)

webs相关事件：

![image-20240402181728065](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402181728065.png)

webs对象提供的方法：

![image-20240402181905951](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402181905951.png)

eg.

```js
<script>
let ws = new WebSocket("ws://localhost/chat");
ws.onopen = function() {};
ws.onmessage = function(evt) {
//通过 evt.data 可以获取服务器发送的数据
};
ws.onclose = function() {};
</script>
```

### 服务端：

Tomcat的7.0.5 版本开始支持WebSocket,并且实现了Java WebSocket规范。
Java WebSocket应用由系列的Endpoint组成。**Endpoint 是一个ava对象，代表WebSocket链接的一端，对于服务端,我们可以视为处理具体WebSocket消息的接口。**

我们可以通过两种方式定义Endpoint:

第一种是编程式，即继承类iavax.websocket.Endpoint并实现其方法
**第二种是注解式，即定义一个POJO,并添加 @ServerEndpoint相关注解**

Endpoint实例在WebSocket握手时创建，并在客户端与服务端链接过程中有效，最后在链接关闭时结束。在Endpoint接口中明确定义了与其生命周期相关的方法，规范实现者确保生命周期的各个阶段调用实例的相关方法。生命周期方法如下。

![image-20240402182917240](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402182917240.png)

### 如何交互

![image-20240402183337082](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402183337082.png)

代码：

```java
aServerEndpoint("/chat")
aComponent
public class ChatEndpoint {
    @OnOpen
    //连接建立时被调用
    public void onOpen(Session session, EndpointConfig config) {}
    @OnMessage
    //接收到客户端发送的数据时被调用
    public void onMessage(String message) {}
    @OnClose
    //连接关闭时被调用
    public void onClose(Session session) {}
}
```

## 五、最后一啪

### 流程图：

![image-20240402183800703](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402183800703.png)

### 消息格式

![image-20240402184252152](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402184252152.png)

![image-20240402184320503](C:\Users\34975\AppData\Roaming\Typora\typora-user-images\image-20240402184320503.png)

### 代码实现

```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
```

### 编写配置类(扫描添加有@ServerEndpoint注解的Bean)

```java
@Configuration
public class WebsocketConfig {
    @Bean
    public ServerEndpointExporterserverEndpointExporter() 	{
        return new ServerEndpointExporter();
    }
}
```

### 获取HttpSession对象

```java
package com.itheima.config;

import javax.servlet.http.HttpSession;
import javax.websocket.HandshakeResponse;
import javax.websocket.server.HandshakeRequest;
import javax.websocket.server.ServerEndpointConfig;

/**
 * @version v1.0
 * @ClassName: GetHttpSessionConfig
 * @Description: TODO(一句话描述该类的功能)
 * @Author: 黑马程序员
 */
public class GetHttpSessionConfig extends ServerEndpointConfig.Configurator {

    @Override
    public void modifyHandshake(ServerEndpointConfig sec, HandshakeRequest request, HandshakeResponse response) {
        //获取HttpSession对象
        HttpSession httpSession = (HttpSession) request.getHttpSession();
        //将httpSession对象保存起来
        sec.getUserProperties().put(HttpSession.class.getName(),httpSession);
    }
}
```

### 在@ServerEndPoint注解中引入配置类

```java
@ServerEndpoint(value = "/chat",configurator =GetHttpSessionConfig.class)
```

## 前端：

### 登录按钮：

```js
login() {
                axios.post("user/login",this.user).then(res => {
                    //判断登陆是否成功
                    if(res.data.flag) {
                        location.href = "main.html"
                    } else {
                        this.errMessage = res.data.message;
                    }
                });
            }
```

### 发送消息：

```js
<script>
    let ws;
    new Vue({
        el: "#app",
        data() {
            return {
                isShowChat: false,
                chatMes: false,
                isOnline: true,
                username:"",
                toName: "",
                sendMessage: {
                    toName: "",
                    message: ""
                },
                inputMessage: "",
                historyMessage: [
                    /*{toName: "李四", message: "你好,张三"},
                    {toName: "李四", message: "在吗"},
                    {toName: "李四", message: "怎么不说话"},
                    {fromName: "张三", message: "你好,李四"}*/
                ],
                friendsList: [
                   /* "李四",
                    "王五"*/
                ],
                systemMessages : [
                    /*"张三",
                    "李四"*/
                ]
            }
        },
        created() {
            this.init();
        },
        methods: {
            async init() {
                await axios.get("user/getUsername").then(res => {
                    this.username = res.data;
                });

                //创建webSocket对象
                ws = new WebSocket("ws://localhost/chat");

                //给ws绑定事件
                ws.onopen = this.onopen;
                //接收到服务端推送的消息后触发
                ws.onmessage = this.onMessage;

                ws.onclose = this.onClose;
            },
            showChat(name) {
                this.toName = name;
                //清除聊天区的数据
                let history = sessionStorage.getItem(this.toName);
                if (!history) {
                    this.historyMessage = [];
                } else {
                    this.historyMessage = JSON.parse(history);
                }
                //展示聊天对话框
                this.isShowChat = true;
                //显示“正在和谁聊天”
                this.chatMes = true;
            },
            submit() {
                this.sendMessage.toName = this.toName;
                this.historyMessage.push(JSON.parse(JSON.stringify(this.sendMessage)));
                sessionStorage.setItem(this.toName, JSON.stringify(this.historyMessage));
                ws.send(JSON.stringify(this.sendMessage));
                this.sendMessage.message = "";
            },
            onOpen() {
                this.isOnline = true;
            },
            onClose() {
                this.isOnline = false;
            },
            onMessage(evt) {
                //获取服务端推送过来的消息
                var dataStr = evt.data;
                //将dataStr 转换为json对象
                var res = JSON.parse(dataStr);

                //判断是否是系统消息
                if(res.system) {
                    //系统消息  好友列表展示
                    var names = res.message;
                    this.friendsList = [];
                    this.systemMessages = [];
                    for (let i = 0; i < names.length; i++) {
                        if(names[i] != this.username) {
                            this.friendsList.push(names[i]);
                            this.systemMessages.push(names[i]);
                        }
                    }
                }else {
                    //非系统消息
                    var history = sessionStorage.getItem(res.fromName);
                    if (!history) {
                        this.historyMessage = [res];
                    } else {
                        this.historyMessage.push(res);
                    }
                    sessionStorage.setItem(res.fromName, JSON.stringify(this.historyMessage));
                }
            }
        }
    });


</script>
```

