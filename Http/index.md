# Http

## 是什么？

> **HTTP是一种能够获取如 HTML 这样的网络资源的** [protocol](https://developer.mozilla.org/en-US/docs/Glossary/protocol)(通讯协议)。**它是在 Web 上进行数据交换的基础，是一种 client-server 协议，也就是说，请求通常是由像浏览器这样的接受方发起的。一个完整的Web文档通常是由不同的子文档拼接而成的，像是文本、布局描述、图片、视频、脚本等等。**

客户端（浏览器）发给服务端的信息 叫做 `requests`

服务端响应客户端的信息叫做`response`

## 有什么用？

- 传递数据
- 控制缓存
- 开放同源限制（允许资源跨域）

目前我在日常使用过程中，都是通过`F12`中`Network`去观察接口请求的状况

- 提交参数正常否
- 服务器响应正常否

![http.png](http://ww1.sinaimg.cn/large/8afe7f49gy1gdx3mt6ws6j20kt0elgml.jpg)

## 