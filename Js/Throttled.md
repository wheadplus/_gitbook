# 函数节流和防抖

## 节流

在游戏中，技能都有CD机制，也就是cd中不能使用技能。

这种机制也就是节流：

```js
function throttle(fn,delay){
    let canUse = true
    return function () {
        if(!canUse) return
        canUse = false
        setTimeout(() => {
            fn.apply(this, arguments)
            canUse = true
        },delay)
    }
}
```

节流的好处，就是防止用户无效输入给服务端。

常见于底部滚动加载。

## 防抖

防抖呢，就是触发事件时生成定时器等待，如果定时期间再次触发事件，则重新生成定时器继续等待。如果定时器过去则调用函数。像外卖小哥接了外卖，等待4分种有没有新单子，有就继续接单。没有就派送外卖。

```js
function debounce(fn, delay) {
    let timerId = null
    return function() {
        if(timerId) {window.clearTimeout(timerId)}
        timerId = setTimeout(() => {
            fn.apply(this,arguments)
            timerId = null
        },delay)
    }
}
```

防抖常见于用户输入搜索限制。

## 总结

- 节流就是CD中，只执行一次函数，防止用户多余输入。

- 防抖就是外卖小哥送外卖，等待接单，有则继续接单继续等，没有就派单。