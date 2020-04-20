# 同源策略&&跨域

## 背景

浏览器出于安全方面的考虑，只允许与本域下的接口交互。不同源的客户端脚本在没有明确授权的情况下，不能读写对方的资源。

本域指的是？

- 同协议：如都是http或者https
- 同域名：如都是http://baidu.com/a和http://baidu.com/b
- 同端口：如都是80端口

举个例子

http://baidu.com/a.js 和 http://baidu.com/b.php 

他们是在同源下所以可以正常访问。

不同源的例子：

- http://baidu.com/main.js 和 https://baidu.com/a.php (协议不同)
- http://baidu.com/main.js 和 http://bbs.baidu.com/a.php (域名不同，域名必须完全相同才可以)
- http://baidu.com/main.js 和 http://baidu.com:8080/a.php (端口不同,第一个是80)

但实际使用中，我们有访问不同源下的资源的需求。所以有了下面的几种方法

## 跨域的方法

### JSONP

script标签能访问其他域名资源。利用这个特性也能跨域。

```js
<script src="http://baidu.com" ></script>
```
访问时提交回调。

```html
<script src="http://baidu.com/weather.php?callback=showData"></script>
```
当服务器接受到callback回调时，返回你想要的参数。最后在页面接受参数
```js
<script>
function showData(ret){
console.log(ret);
}
</script>
<script src="http://baidu.com/weather.php?callback=showData"></script>
```

总结流程：

- 通过script标签在页面提前声明个函数，函数名通过接口传参的方式传给后台
- 后台解析到函数名后把数据包括在函数名，发送给前端。

#### 缺点

- 麻烦，每个函数都要处理
- 前后端都要处理

### CORS

跨域资源共享（CORS）是一种白名单机制，通过额外的http header 告诉浏览器，哪些跨域资源可以用。具体需要在后台发送http请求时配置。

```js
res.setHeader('Access-Control-Allow-Origin','http://localhost:8080')
//res.setHeader('Access-Control-Allow-Origin','*')
```

对于需要跨域的域名，放开权限即可。

## 总结

跨域是为了保护服务器的安全，但设计者也留了通道给服务器访问不同域的资源。

