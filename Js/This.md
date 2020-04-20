# this

## this的确定

关于`this`在红皮书中或[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)中没有明确的定义。

> 在绝大多数情况下，函数的调用方式决定了`this`的值。`this`不能在执行期间被赋值，并且在每次函数被调用时`this`的值也可能会不同。ES5引入了[bind](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)方法来设置函数的`this`值，而不用考虑函数如何被调用的，ES2015 引入了支持`this`词法解析的箭头函数（它在闭合的执行环境内设置`this`的值）。

虽然没有明确定义，但总归有规律可循。这里引用[this 的值到底是什么？一次说清楚](https://zhuanlan.zhihu.com/p/23804247)的方法。因为这样很好记忆。

## this 是什么

`this`就是 `call`的第一个`call`参数.需要在它被`调用`的时候传入的参数才能确定。

##### 显式`this`

明确给`this`赋值

```js
fn.call(asThis,1,2)
fn.bind(asThis,1,2)()
obj.method.call(obj,'hi')
```

##### 隐式`this`

没有明确给`this`赋值的情况下，通过补上`call`的情况来判断`this`到底是什么？

```js
fn(1,2)
//fn.call(undefined,1,2) 需要看声明fn的环境下，this是什么，全局的话是window
obj.method('hi')
//obj.method.call(obj,'hi')
array[0]('hi')
array.[0].call(array,'hi')
```



## 测试

```js
button.onclick = function(e){
    console.log(this)
}
// this 是什么？
```

`this` 未确定，因为还没被调用。如果用户点击，那么`this`传入`button`

如果通过函数调用，如下：

```js
var f = button.onclick
f() 
// f.call(undefined)  声明环境全局所以this是window
```

所以明确this 的步骤

1. 调用没
2. 明确this的pass，不明确的通过call补全去判断 this

### 测试难度+1

```js
let length = 10
function fn(){console.log(this.length)}

let obj = {
    length: 5,
    method(fn) {
        fn()
        arguments[0]()
    }
}
obj.method(fn,1)
```

分情况讨论。fn

```js
fn()
// fn.call(undefined) 声明时全局 this.length 等于 window.length length是window的自由属性，所以let length = 10 不会覆盖 window.length  默认window.length == i 返回当前窗口中包含的框架数量(框架包括frame和iframe两种元素).

```

`arguments[0]()`的情况

```js
arguments[0]()
// arguments.0.call(arguments)  this 等于arguments
// arguments输入时两个参数，所以 arguments.length 等于 2 
```



## 总结

- this 要在调用时才能确定
- 有传this 不用讨论
- 没传this 通过补上call确定
  - `fn(1,2)`
  - 等价于`fn.call(undefined,1,2) `需要看声明fn的环境下，this是什么，全局的话是window
  - `obj.method('hi')`
  - `等价于obj.method.call(obj,'hi')`
  - `array[0]('hi')`
  - 等价于`array.[0].call(array,'hi')`







































































