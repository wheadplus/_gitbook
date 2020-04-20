# 手写EventHub

## eventHub 是什么？

eventHub 是事件中转站。它提供功能：

1. 提交函数到`eventHub`中对应的事件
2. 触发`eventHub` 中对应事件的函数
3. 取消`eventHub`中对应事件的函数



```js
class EventHub {
    constructor () {
        this.cache = {}
    }
}
```

1. on（事件名，回调函数）

```js
on(eventName,fn) {
    this.cache[eventName] = this.cache[eventName] || []
    this.cache[eventName].push(fn)
}
```

2. emit(事件名，提交参数)

```js
emit(eventName,args) {
    (this.cache[eventName] || []).forEach(fn => {
        fn(args)
    })
}
```

3. off(事件名，取消函数名)

```js
off(eventName,fn) {
    let index = this.cache[eventName].indexOf(fn)
    this.cache[eventName].splice(index,1)
}
```



## 总结

合并之后，代码如下。

```js
class EventHub {
  constructor () {
    this.cache = {}
  }
  on (eventName, fn) {
    this.cache[eventName] = this.cache[eventName] || []
    this.cache[eventName].push(fn)
  }
  emit (eventName, args) { 
    (this.cache[eventName] || []).forEach( fn => {
      fn(args)
    });
  }

  off (eventName, fn) {
    let index = this.cache[eventName].indexOf(fn)
    this.cache[eventName].splice(index, 1)
  }
}

module.exports = EventHub

```



## 缺点

eventHub在数据少量的情况下，表现不错。但在多人合作，会出现多处地方提交相同事件等问题。如果需要统一管理，如vue中可以换成Vuex。