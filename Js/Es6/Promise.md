# Promise

> Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。

> 所谓`Promise`，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。



## Promise要解决的问题

```js
function fn1(callback) {
  setTimeout(()=>{
    console.log('fn1')
    callback()
  }, 1000)
}
function fn2(callback) {
  setTimeout(()=>{
    console.log('fn2')
    callback()
  }, 1000)
}
function fn3() {
  setTimeout(()=>{
    console.log('fn3')
  }, 1000)
}

fn1(function(){
  fn2(function(){
    fn3()
  })
})
```

回调地狱，

- 层层嵌套的接口不清晰。
- 发生异常难以处理

## Promise 基本使用

```js
function AsyncFn() {
    return new Promise((resolve,reject) => {
        resolve(//成功返回结果)
        reject(//失败返回结果)
    })
}
AsyncFn().then(result => {
            //成功操作
        },response => {
            //失败操作
        }).catch(error => {
            //外层统一处理失败
        }).finally(
        	//成功失败都会执行
        )
```

promise的使用

- 创建Promise实例
- 成功通过一个参数`resolve`返回
- 失败通过第二个参数`reject`返回
- 链式调用`then(success() ,fail())`
- `.catch()`处理异常
- `.finally()`统一处理

栗子：

```js
function bigOrSmall() {
    return new Promise((resolve,reject) => {
       setTimeout(() => {
            let result = Math.floor((Math.random()*6)+1)
            if(result > 3) {
                resolve(result)
            } else {
                reject(result)
            }
        },3000)
    })
}

bigOrSmall().then(
    result => {console.log('大于3，结果: ',result)},
    response => {console.log('小于3，结果： ',response)}
).then(
    result2 => {console.log("继续游戏")},
    ()=> {}
).catch(
    error => {console.log("异常错误")}
).finally( data => {
    console.log("不管输赢，今晚吃夜宵")
})
```

##  Promise.all()

控制多个Promise实例的顺序，等所有Promise实例成功才返回。

只有所有实例都失败，Promise.all才会走失败函数。

```js
Promise.all([promise1,promise2]).all(success,fail).catch(error => {})
```

栗子

```js
var p1 = new Promise((resolve, reject) => {
  resolve('resolve  p1');
}).then(result => result)
.catch(e => e);

var p2 =  p2 = new Promise((resolve, reject) => {
  reject('reject  p2')
}).then(result => result)
.catch(e => e);

Promise.all([p1, p2])
.then(result => console.log(result))
.catch(e => console.log(e));
// ["resolve  p1", "reject  p2"]
```



##  Promise.race()竞速

控制多个Promise实例的顺序，有

- 一个Promise实例成功立刻返回，
- 失败的实例会跳过，等待其他实例。
- 所有实例都失败，才返回最后一个失败实例

```js
Promise.race([promise1,promise2]).then(success,fail).catch(error => {})
```

栗子

```js
var p1 = new Promise((resolve, reject) => {
   setTimeout(()=>{resolve('3s,resolve  p1')},3000)
}).then(result => result)
.catch(e => e);

var p2 =  p2 = new Promise((resolve, reject) => {
     setTimeout(()=>{ reject('2s,reject  p2')},4000)
}).then(result => result)
.catch(e => e);


Promise.race([p1, p2])
.then(result => console.log(result))
.catch(e => console.log(e));

// 3s,resolve  p1
```



所有都失败，返回的是最后1个实例的失败数据

```js
var p1 = new Promise((resolve, reject) => {
   setTimeout(()=>{reject('3s,resolve  p1')},3000)
}).then(result => result)
.catch(e => e);

var p2 =  p2 = new Promise((resolve, reject) => {
     setTimeout(()=>{ reject('2s,reject  p2')},4000)
}).then(result => result)
.catch(e => e);
undefined
Promise.race([p1, p2])
.then(result => console.log(result))
.catch(e => console.log(e));
// 3s,resolve  p1
```



## 优点

- 链式结构，避免回调地狱的层层嵌套

## 缺点

- 无法取消`Promise`，一旦新建它就会立即执行，无法中途取消。
- 如果不设置回调函数，`Promise`内部抛出的错误，不会反应到外部。
- 第三，当处于`pending`状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。