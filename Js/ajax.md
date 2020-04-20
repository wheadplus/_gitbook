# ajax

## 是什么?

ajax 是 一种技术方案。利用XMLHttpRequest对象，发送http请求和接受http响应。实现页面不刷新情况下与服务器交互数据。



怎么做？

1. 设置请求地址
2. 监听请求成功事件
3. 发送请求

```js
var request = new XMLHttpRequest()
request.open('get','www.baidu.com')
request.onreadStateChange = () => {
    if(request.readState === 4 && requset.status === 200) {
        console.log(request.responseText)
    }
}
request.send()
```

简化版

```js
var requset = new XMLHttpRequest()
request.open('get','www.baicu.com')
request.onload(()=> { console.log(request.responseText)})
request.send()
```



## axios

添加

```js
npm install axios
```

get请求

```js
axios.get('/user?id=123').then((response)=> {
	console.log(response)
	}).catch((error)=>{
	console.log(error)
	}))
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

