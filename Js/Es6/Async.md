# Async

## 是什么？

> async 函数是什么？一句话，它就是 Generator 函数的语法糖。

它和`promise`一样是异步编程解决方案。区别就是它写成同步代码的格式。



## 怎么用？

看下例子

```js
async function timeout(ms) {
  await new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
      await timeout(ms);
      return value
}

asyncPrint('hello world', 50).then(result => {
    console.log(result)
});
```





## 处理异常

1.`try...catch`包裹` await`

```js
async function randonNum() {
    throw new Error("not input")
}

async function fn() {
    try {
        var result = await randonNum()
    } catch(e) {
        console.log(e)
    }
}
```

2.`.catch`异常处理,

```js
async function fn() {
    return new Promise((resolve,reject) => {
        reject('error ')
    })
}

async function handleError() {
    //let result = await fn().then(null,error => {console.log('z',error)})
    let result = await fn().catch(error => {console.log('z',error)})
}

handleError()
 z error 
```

## 总结

`async` 函数

- 函数前用`async` 标志

- `await`后面 处理异步代码，一般是`Promise`对象，数值直接返回

- `async` 函数返回的是`promise`对象，所以可以`then链`继续操作。

- 异常处理用`try...catch` 或`.catch()`

  

## 参考

[async 阮一峰es6](https://es6.ruanyifeng.com/#docs/async)